# Templates

Questo progetto dimostra l'uso dei **template Jinja2** in Ansible per generare file dinamici e configurazioni personalizzate per ogni macchina o gruppo di server.

## Struttura del Progetto

```bash
formazione_ansible/ 
├── ansible.cfg 
├── hosts.ini 
├── dynamic_template.yml # Playbook per configurazione dinamica per macchina 
├── group_inventory_template.yml # Playbook per elenco server del gruppo 
├── templates/ 
│ ├── machine_info.j2 # Template con informazioni macchina 
│ └── group_hosts_list.j2 # Template con elenco server del gruppo 
```

---

## 1. Deploy di un File Dinamico per Ogni Macchina

### Descrizione

Questo playbook genera un file con informazioni personalizzate per ogni macchina (hostname, indirizzo IP e sistema operativo).

### Template: `templates/machine_info.j2`

```jinja
##########################################
#  Configurazione Generata Automaticamente
##########################################

Hostname: {{ inventory_hostname }}
Indirizzo IP: {{ ansible_host }}
Sistema Operativo: {{ ansible_distribution }} {{ ansible_distribution_version }}

Generato da Ansible in data: {{ ansible_date_time.date }}
```

### Playbook: dynamic_template.yml

```yml
---
- name: Deploy di un template dinamico per ogni macchina
  hosts: all
  become: true
  tasks:
    - name: Generare file di configurazione dinamico
      ansible.builtin.template:
        src: templates/machine_info.j2
        dest: /tmp/machine_info.txt
        owner: vagrant
        group: vagrant
        mode: '0644'
```

### Comando di Esecuzione

```bash
ansible-playbook dynamic_template.yml
```

### Risultato
Su ogni macchina (web1, web2), il file /tmp/machine_info.txt conterrà:

```txt
##########################################
#  Configurazione Generata Automaticamente
##########################################

Hostname: web1
Indirizzo IP: 127.0.0.1
Sistema Operativo: Rocky 9.4

Generato da Ansible in data: 2025-01-15
```

---

## 2. Deploy di un Elenco delle Macchine di un Gruppo

### Descrizione

Questo playbook crea un file con la lista di tutti i server appartenenti al gruppo web_servers.

### Template: templates/group_hosts_list.j2

```jinja
##########################################
#  Elenco dei server nel gruppo web_servers
##########################################

{% for host in groups['web_servers'] %}
- {{ host }} ({{ hostvars[host]['ansible_host'] }})
{% endfor %}

Generato da Ansible in data: {{ ansible_date_time.date }}
```

### Playbook: group_inventory_template.yml

```yml
---
- name: Deploy dell'elenco dei server del gruppo web_servers
  hosts: all
  become: true
  tasks:
    - name: Creare file con elenco dei server del gruppo web_servers
      ansible.builtin.template:
        src: templates/group_hosts_list.j2
        dest: /tmp/web_servers_list.txt
        owner: vagrant
        group: vagrant
        mode: '0644'
```

### Comando di Esecuzione

```bash
ansible-playbook group_inventory_template.yml
```

### Risultato

Su tutte le macchine (`web1`, `web2`), il file `/tmp/web_servers_list.txt` conterrà:

```txt
##########################################
#  Elenco dei server nel gruppo web_servers
##########################################

- web1 (127.0.0.1)
- web2 (127.0.0.1)

Generato da Ansible in data: 2025-01-15
```

---

## Configurazione dell'Inventory

### File: hosts.ini

```ini
[web_servers]
web1 ansible_host=127.0.0.1 ansible_port=2222 ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/web1/virtualbox/private_key ansible_ssh_common_args='-o StrictHostKeyChecking=no'
web2 ansible_host=127.0.0.1 ansible_port=2200 ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/web2/virtualbox/private_key ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

---

## Esecuzione Completa

1. **Deploy del template dinamico per macchina:**

```bash
ansible-playbook dynamic_template.yml
```

2. **Deploy dell'elenco dei server del gruppo:**

```bash
ansible-playbook group_inventory_template.yml
```

---

## Conclusioni

In questa sezione abbiamo imparato a:

- Creare file dinamici per ogni macchina usando **template Jinja2**
- Generare un elenco dinamico dei server di un gruppo tramite Ansible
- Questi strumenti sono fondamentali per automatizzare la gestione di configurazioni su larga scala.

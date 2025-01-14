# Inventory

In questa sezione è stata configurata la gestione dell'**Inventory** di **Ansible**, definendo i server target su cui verranno eseguiti i playbook. Sono stati creati file di inventory sia in formato **INI** che **YAML** e sono state assegnate variabili specifiche ai gruppi di host.

## Struttura del Progetto

La struttura aggiornata del progetto è la seguente:
```bash
formazione_ansible/ 
├── Vagrantfile 
├── ansible.cfg 
├── hosts.ini 
├── inventory 
│   ├── group_vars 
│   │   └── web_servers.yml 
│   ├── inventory.yml 
│   └── web_servers.yml 
├── playbook.yml
```

## Creazione dell'Inventory

### Formato INI (`hosts.ini`)

È stato creato un file `hosts.ini` per definire i gruppi di host in formato INI. Questo formato permette di elencare facilmente i server e raggrupparli.

### Formato YAML (`inventory.yml`)

In parallelo, è stato creato il file `inventory.yml` in formato YAML, che fornisce una struttura più dettagliata e leggibile per ambienti complessi.

## Assegnazione di Variabili per Gruppo

Nella directory `inventory/group_vars/` è stato creato il file `web_servers.yml` per assegnare variabili specifiche al gruppo `web_servers`. Questo permette di gestire configurazioni diverse per ciascun gruppo di server.

## Inventory Avanzato con File Separati

All'interno della cartella `inventory/`, è stato inserito anche il file `web_servers.yml` per una gestione più modulare e scalabile dei gruppi.

## Comandi Utili

- Visualizzare l'inventory in formato leggibile:
  ```bash
  ansible-inventory -i hosts.ini --list
  ansible-inventory -i inventory/inventory.yml --list
  ```

- Verificare la connettività con i server:
  ```bash
  ansible -i hosts.ini all -m ping
  ansible -i inventory/inventory.yml all -m ping
  ```

## Come Iniziare

Clonare il repository:
  ```bash
  git clone https://github.com/lucacis8/formazione_ansible
  cd formazione_ansible
  ```

Verificare la configurazione dell'inventory:
  ```bash
  ansible-inventory -i inventory/inventory.yml --list
  ```

Testare la connettività tra Ansible e le VMs:
  ```bash
  ansible -i inventory/inventory.yml all -m ping
  ```

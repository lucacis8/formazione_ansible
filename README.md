# Formazione Ansible

Questa repository è un progetto di formazione su **Ansible**, un potente strumento di automazione IT. In questa repository, vengono esplorate le tecniche per l'automazione della configurazione di macchine virtuali, la gestione di inventory, la creazione di playbook, l'uso di template dinamici e la gestione degli errori. Gli esercizi sono progettati per insegnare i concetti di base e avanzati di Ansible.

## Esercizi Principali

### 1. **Creazione dell'Ambiente con Vagrant**
   In questo esercizio viene configurato un ambiente di test utilizzando **Vagrant** per creare due macchine virtuali (VMs) su cui verranno eseguiti i playbook Ansible. Vagrant automatizza la creazione delle VMs, mentre Ansible gestisce la loro configurazione.

### 2. **Gestione dell'Inventory**
   L'esercizio esplora la creazione e la gestione dell'inventory di Ansible, definendo gruppi di server, variabili e configurazioni specifiche per ogni gruppo. Sono inclusi file di inventory sia in formato INI che YAML.

### 3. **Playbooks di Automazione**
   In questa sezione vengono creati e gestiti playbook per automatizzare la configurazione dei server. Gli esercizi includono l'installazione di Apache, la gestione sicura dei dati sensibili con **Ansible Vault**, e l'esecuzione di task condizionati e in loop.

### 4. **Templates**
   Si esplora l'uso di **template Jinja2** per generare file dinamici basati su variabili e configurazioni specifiche delle macchine o dei gruppi di server. Vengono creati template per generare informazioni di sistema e un elenco di server di un gruppo.

### 5. **Gestione degli Errori**
   In questa sezione vengono esplorate le tecniche per gestire gli errori nei playbook, inclusa la verifica delle variabili obbligatorie, l'ignoranza degli errori nei task, la gestione di fallimenti condizionati, e l'uso dei blocchi `block`, `rescue`, e `always` per una gestione avanzata degli errori.

---

## Come Iniziare

1. **Clonare il repository:**
   Per iniziare, clona il repository nel tuo ambiente locale:
   ```bash
   git clone https://github.com/lucacis8/formazione_ansible
   cd formazione_ansible
   ```

2. **Creare le macchine virtuali con Vagrant:**
   Esegui il comando vagrant up per creare e avviare le macchine virtuali:
   ```bash
   vagrant up
   ```

3. **Accedere alle VMs:**
   Puoi accedere alle VMs utilizzando SSH con il comando:
   ```bash
   vagrant ssh web1
   vagrant ssh web2
   ```

4. **Esecuzione dei playbook:**
   Esegui i playbook per configurare i server e testare le funzionalità di Ansible. Per esempio:
   ```bash
   ansible-playbook playbook.yml
   ```

---

## Comandi Utili

- **Verifica l'inventory:**
   Puoi visualizzare l'inventory con il comando:
   ```bash
   ansible-inventory -i inventory/inventory.yml --list
   ```

- **Test della connettività con i server:**
   Per verificare che i server siano raggiungibili:
   ```bash
   ansible -i inventory/inventory.yml all -m ping
   ```

- **Gestione dei segreti con Ansible Vault:**
   Per creare e modificare file criptati con Ansible Vault:
   ```bash
   ansible-vault create secrets.yml
   ansible-vault edit secrets.yml
   ```

---

## Conclusioni

Questa repository è progettata per insegnare come utilizzare Ansible per automatizzare la configurazione di server e gestire l'infrastructure as code. Gli esercizi coprono una varietà di scenari che vanno dall'automazione di base alla gestione avanzata degli errori e dei dati sensibili. Ansible è uno strumento potente che semplifica la gestione di sistemi, e questa repository offre una solida base per iniziare a usarlo.

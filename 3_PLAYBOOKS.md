# Playbooks

Questa repository contiene una raccolta di playbook Ansible per automatizzare l'installazione e la configurazione di servizi su macchine remote. I playbook includono best practice per la gestione sicura dei dati sensibili e per la modularità del codice.

## Requisiti

- **Vagrant**: Per creare ambienti di test virtualizzati
- **Ansible**: Versione 2.9 o successiva
- **ansible-vault**: Per la gestione sicura di dati sensibili

---

## Sezioni dei Playbook

### 1. **Installazione di Apache**

Questo playbook installa Apache e pubblica una pagina HTML di prova.

**File coinvolti**:  
- `playbook.yml`:  
  - Installa Apache (`httpd`)  
  - Avvia e abilita il servizio  
  - Crea una pagina di test in `/var/www/html/index.html`

**Esecuzione**:
```bash
ansible-playbook playbook.yml
```

**Risultato**:
- Apache installato e in esecuzione
- Pagina web accessibile su `http://<hostname>`

---

### 2. Gestione Sicura di Dati Sensibili con Ansible Vault

Questo playbook (`secure_playbook.yml`) utilizza **Ansible Vault** per gestire dati sensibili (password, chiavi API, ecc.).

#### Come configurare Ansible Vault

1. **Creare il file criptato**:
```bash
ansible-vault create secrets.yml
```

2. **Inserire i dati sensibili**:
```bash
vault_db_password: "supersecretpassword"
vault_api_key: "1234567890abcdef"
```

3. **Visualizzare o modificare il file**:

- **Visualizza**:
```bash
ansible-vault view secrets.yml
```

- **Modifica**:
```bash
ansible-vault edit secrets.yml
```

4. **Esecuzione del Playbook**:
```bash
ansible-playbook secure_playbook.yml --ask-vault-pass
```

#### Descrizione del Playbook (secure_playbook.yml)

- Installa Apache
- Crea un file di configurazione (`/etc/httpd/conf.d/secure.conf`) con le variabili sensibili
- Avvia il servizio Apache

**Esempio di contenuto generato**:
```bash
# Configurazione con variabili sensibili
DatabasePassword: supersecretpassword
ApiKey: 1234567890abcdef
```

**Risultato**:
- Configurazione sicura grazie all’uso di variabili criptate
- Apache avviato e configurato

---

### 3. Task Condizionati

Questo playbook (`conditional_playbook.yml`) esegue task solo se vengono soddisfatte specifiche condizioni, come:
- Verifica dell’esistenza di file
- Controllo se un servizio è in esecuzione

**Esecuzione**:
```bash
ansible-playbook conditional_playbook.yml
```

**Risultato**:
- Task eseguiti solo se le condizioni sono vere.

---

### 4. Task in Loop

Questo playbook (`loop_playbook.yml`) crea file multipli in `/tmp` utilizzando un ciclo.

**File coinvolti**:
- `loop_playbook.yml`: definisce il ciclo
- `files/content.j2`: template per il contenuto dei file

**Esecuzione**:
```bash
ansible-playbook loop_playbook.yml
```

**Risultato**:
- Creazione di `/tmp/fileA.txt`, `/tmp/fileB.txt`, `/tmp/fileC.txt` con contenuto dinamico.

**Esempio di contenuto (content.j2)**:
```bash
#####################################
#  File generato automaticamente    #
#        da Ansible Playbook        #
#####################################

Questo è un file di esempio creato tramite Ansible.

- Data di creazione: {{ ansible_date_time.date }}
- Hostname: {{ inventory_hostname }}
```

---

### 5. Importazione di Task e Variabili

Questo playbook (`main_playbook.yml`) dimostra come importare task e variabili da file esterni per una gestione più modulare.

**File coinvolti**:
- `main_playbook.yml`: playbook principale
- `vars/file_vars.yml`: variabili esterne
- `tasks/create_files.yml`: task esterni

**Esecuzione**:
```bash
ansible-playbook main_playbook.yml
```

**Risultato**:
- File definiti in `file_vars.yml` creati con contenuto personalizzato.

---

## Struttura del Progetto

```bash
.
├── Vagrantfile               # Configurazione Vagrant (opzionale)
├── ansible.cfg               # Configurazione di Ansible
├── hosts.ini                 # Inventory dei server
├── playbook.yml              # Installazione di Apache
├── secure_playbook.yml       # Playbook con dati sensibili
├── conditional_playbook.yml  # Task condizionati
├── loop_playbook.yml         # Task in loop
├── main_playbook.yml         # Playbook con importazioni
├── vars/                     # Variabili esterne
│   └── file_vars.yml         # Variabili per i file
├── tasks/                    # Task esterni
│   └── create_files.yml      # Creazione file
├── files/                    # Template di file
│   └── content.j2            # Template per i file di test
└── secrets.yml               # File criptato con Ansible Vault
```

---

## Esecuzione con Vagrant

1. Avvio dell’ambiente:
```bash
vagrant up
```

2. Accesso alla macchina virtuale:
```bash
vagrant ssh
```

3. Esecuzione dei playbook:
```bash
ansible-playbook playbook.yml
ansible-playbook secure_playbook.yml --ask-vault-pass
```

---

## Conclusioni

Questa repository dimostra come Ansible può automatizzare l’installazione di servizi e gestire in sicurezza dati sensibili attraverso l’uso di **Ansible Vault**.
Ogni playbook è pensato per essere modulare e facilmente estendibile.

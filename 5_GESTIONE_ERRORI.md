# Gestione Errori

Questa sezione illustra diverse tecniche per gestire gli errori nei playbook Ansible. Gli esempi includono la verifica di variabili, la gestione degli errori nei task, il controllo condizionale degli errori e l'uso di blocchi `block`, `rescue` e `always`.

---

## Contenuto degli Esercizi

1. **Verifica delle Variabili Obbligatorie**  
   Controllare che variabili fondamentali siano definite prima dell'esecuzione.  
   **File:** `check_variables.yml`

2. **Ignorare Errori nei Task**  
   Eseguire task che potrebbero fallire senza bloccare il playbook.  
   **File:** `ignore_errors.yml`

3. **Fallimento Condizionale**  
   Far fallire un task solo se viene rilevato uno specifico output.  
   **File:** `fail_on_condition.yml`

4. **Gestione Avanzata degli Errori con block/rescue/always**  
   Utilizzare blocchi per catturare e gestire errori in modo strutturato.  
   **File:** `block_rescue.yml`

---

## Dettagli degli Esercizi

### 1. Verifica delle Variabili Obbligatorie (`check_variables.yml`)  
Questo playbook verifica se la variabile `app_port` è definita. In caso contrario, il task fallisce.  

**Comando di esecuzione:**  
```bash
ansible-playbook check_variables.yml
```

**Funzionalità chiave:**
- Utilizzo di assert per la validazione delle variabili.
- Interruzione del playbook se la variabile non è definita.

---

### 2. Ignorare Errori nei Task (`ignore_errors.yml`)
Esegue un comando rischioso ma non blocca il playbook in caso di errore, grazie a `ignore_errors: true`.

**Comando di esecuzione:**
```bash
ansible-playbook ignore_errors.yml
```

**Funzionalità chiave:**
- Uso di `ignore_errors: true` per continuare l'esecuzione anche dopo un errore.
- Gestione dell'output del task fallito.

---

### 3. Fallimento Condizionale (`fail_on_condition.yml`)
Esegue un comando e verifica l'output. Se contiene `"ERRORE_CRITICO"`, il task fallisce.

**Comando di esecuzione:**
```bash
ansible-playbook fail_on_condition.yml
```

**Funzionalità chiave:**
- Uso di `failed_when` per forzare il fallimento su condizioni specifiche.
- Controllo mirato dell'output di un comando.

---

### 4. Gestione Avanzata con block/rescue/always (`block_rescue.yml`)
Organizza i task in blocchi per gestire in modo ordinato i fallimenti e garantire sempre l'esecuzione di azioni finali.

**Comando di esecuzione:**
```bash
ansible-playbook block_rescue.yml
```

**Funzionalità chiave:**
- `block`: esecuzione di task principali.
- `rescue`: gestione degli errori in caso di fallimento.
- `always`: esecuzione di task finali indipendentemente dal risultato.

---

## Obiettivi Raggiunti

- Verifica preventiva delle variabili obbligatorie.
- Continuazione del playbook nonostante errori gestiti.
- Controllo condizionale per fallimenti specifici.
- Gestione strutturata degli errori con `block`, `rescue` e `always`.

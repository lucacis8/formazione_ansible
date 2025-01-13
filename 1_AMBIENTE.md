# Ambiente di Sviluppo

In questa sezione, abbiamo scelto di utilizzare **Vagrant** per creare e gestire due macchine virtuali (VMs) su cui verrà successivamente eseguito **Ansible** per la configurazione automatica. Il processo di creazione delle macchine virtuali è stato automatizzato tramite un **Vagrantfile**, che definisce le caratteristiche delle VMs, inclusi i loro indirizzi IP e la rete.

## 1. Creazione dell'Ambiente con Vagrant

Abbiamo utilizzato **Vagrant** per creare due macchine virtuali (VMs) basate su **Rocky Linux 9**. Vagrant fornisce un ambiente facilmente ripetibile e gestibile, che può essere avviato e distrutto tramite pochi comandi. Le macchine virtuali sono configurate per comunicare tra di loro tramite una rete **host-only**.

### File Utilizzati:
- **Vagrantfile**: Contiene la configurazione per la creazione delle macchine virtuali. Abbiamo creato due VMs, `web1` e `web2`, configurandole per utilizzare una rete **host-only** (per la comunicazione privata tra di esse) e una rete **NAT** (per l'accesso a Internet).

### Comandi Vagrant:
- `vagrant up`: Avvia e crea le macchine virtuali definite nel `Vagrantfile` (se non esistono, le crea).
- `vagrant ssh <nome_vm>`: Permette di accedere via SSH a una delle VMs (ad esempio `vagrant ssh web1` o `vagrant ssh web2`).

### Rete:
Le macchine virtuali sono configurate con due interfacce di rete:
- **NAT**: per permettere la connessione a Internet.
- **Host-only**: per consentire alle macchine di comunicare tra di loro senza essere esposte a Internet.

Gli indirizzi IP delle VMs sono stati configurati come segue:
- `web1`: `192.168.56.46`
- `web2`: `192.168.56.47`

## 2. Verifica della Rete e Connettività

Le macchine virtuali sono configurate per comunicare tra loro tramite la rete **host-only**. È stato possibile verificare la configurazione della rete con i seguenti comandi:

- **Verificare gli indirizzi IP delle VMs**:
  - `vagrant ssh web1 -c "ip a"`
  - `vagrant ssh web2 -c "ip a"`

### Accesso alle VMs:
Dopo aver avviato le VMs con il comando `vagrant up`, è possibile accedervi tramite SSH per configurare ulteriormente il sistema o eseguire comandi. 

Ad esempio, per accedere a `web1`:
```bash
vagrant ssh web1
```

e per accedere a `web2`:
```bash
vagrant ssh web2
```

### Verifica della Rete tramite Ping:
Per verificare la comunicazione tra le due VMs, è possibile utilizzare il comando `ping`:
- **Ping da `web1` a `web2`**:
```bash
ping 192.168.56.47
```

## 3. Configurazione iniziale delle VMs

Una volta avviate le VMs, è stato possibile configurarle e verificare che tutto fosse pronto per l'installazione e la configurazione tramite Ansible (che verrà trattato nella sezione successiva).

### IP delle VMs:
- `web1`: `192.168.56.46`
- `web2`: `192.168.56.47`

### Controllo della Connettività:
Le VMs sono state configurate per consentire l'accesso SSH e la comunicazione tra di loro attraverso l'IP privato assegnato.

---

### Come Iniziare:

1. Clonare il repository:
```bash
git clone https://github.com/lucacis8/formazione_ansible
cd formazione_ansible
```

2. Creare le macchine virtuali eseguendo il comando:
```bash
vagrant up
```

3. Accedere alle VMs con:
```bash
vagrant ssh web1
```

```bash
vagrant ssh web2
```

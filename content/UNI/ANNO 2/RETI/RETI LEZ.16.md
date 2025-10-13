### Conclusione del Livello di rete
## ICMP internet control message protocol
- Utilizzato da Host e router per comunicare informazioni a livello di rete
	- tipo errori o richieste
è incapsulato dentro IP, ma non viene considerato un protocollo di trasporto perché non ha quello come scopo
- i messaggi di ICMP sono nello stesso datagramma di IP
Informazioni su come è strutturato:
![[Pasted image 20250505192401.png]]
- **Tipo (8 bit)**: identifica il tipo di messaggio (es. richiesta echo, host non raggiungibile, ecc.)
- **Codice (8 bit)**: specifica il significato dettagliato del tipo.
- **Checksum (16 bit)**: per il controllo degli errori.
- **Resto dell’intestazione**: varia a seconda del tipo di messaggio.
- **Dati / intestazione IP originale**: include i primi 8 byte dei dati del datagramma IP che ha causato il messaggio, per aiutare a identificare il processo responsabile.
### Tipi di messaggi ICMP
Questi sono tutti i messaggi possibili, se scendi giù c'è un focus sui più utili

| Tipo | Codice | Descrizione                 | Utilizzo / Spiegazione                                                                             |
| ---- | ------ | --------------------------- | -------------------------------------------------------------------------------------------------- |
| 0    | 0      | Echo reply (ping)           | Risposta a una richiesta ping (tipo 8); il destinatario conferma la ricezione.                     |
| 3    | 0      | Destination unreachable     | Segnala che il pacchetto non può essere consegnato.                                                |
| 3    | 0      | Network unreachable         | Nessuna rete di destinazione raggiungibile. Potrebbe essere un router a inviarlo.                  |
| 3    | 1      | Host unreachable            | L'host specifico non è raggiungibile (es. fallimento ARP).                                         |
| 3    | 2      | Protocol unreachable        | Protocollo IP non supportato dalla destinazione.                                                   |
| 3    | 3      | Port unreachable            | Porta della destinazione non aperta (es. nessun servizio in ascolto).                              |
| 3    | 4      | Fragmentation required      | Necessaria frammentazione ma non permessa (usato da **Path MTU Discovery**).                       |
| 3    | 6      | Network unknown             | La rete di destinazione è sconosciuta (nessuna rotta).                                             |
| 3    | 7      | Host unknown                | L'host è sconosciuto (indirizzo errato o non risolvibile).                                         |
| 4    | 0      | Source quench _(deprecato)_ | Un router congestionato richiedeva all’host mittente di rallentare l’invio. Ora **non più usato**. |
| 8    | 0      | Echo request (ping)         | Richiesta ping. Usata per verificare se un host è attivo e raggiungibile.                          |
| 11   | 0      | TTL expired                 | Il pacchetto è scaduto (TTL=0); usato da **traceroute** per identificare i router sul percorso.    |
✅ **Focus pratico sui messaggi più importanti:**
#### 🔹 **Echo Request / Echo Reply (Tipo 8/0 e 0/0)**
- Usati da `ping`.
- Permettono di sapere se un host è raggiungibile e misurare il tempo di risposta (RTT).
- La risposta (tipo 0) contiene gli stessi dati della richiesta (tipo 8), utile per calcoli.
#### 🔹 **Destination Unreachable (Tipo 3)**
- Molto usato dai router o dagli host di destinazione per indicare problemi di raggiungibilità.
    - Es. tipo 3 codice 3 (porta non raggiungibile): succede quando invii UDP a una porta chiusa.
    - Tipo 3 codice 4 (fragmentation required): usato quando il pacchetto è troppo grande e il bit “don’t fragment” è attivo → utile per scoprire la MTU.
#### 🔹 **Source Quench (Tipo 4)**
- Permetteva al router di segnalare congestione → ora **deprecato** e non più supportato nei protocolli moderni (sostituito da ECN).
#### 🔹 **TTL Expired (Tipo 11)**
- Fondamentale per il comando `traceroute`: ogni hop lungo il percorso invia questo messaggio quando il TTL arriva a 0.
- Serve per “mappare” i router intermedi tra sorgente e destinazione.

#### Focus su Traceroute e ICMP
![[Pasted image 20250505192939.png]]
con Traceroute possiamo tracciare il percorso di un pacchetto
- posso inviare un pacchetto "sonda" con UDP o ICMP
- invio questo pacchetto con TTL=1 time to live=1
	- un messaggio speciale che dopo un tot di secondi o hop dei router scade
	- il router decrementa TTL di 1 poi appunto diventa expired e invia un messaggio al mittente
	- il mittente così capisce quale percorso è stato eseguito e da quali router

TTL è di tipo incrementale cioè inizia con TTL=1 poi di solito si fa incrementare finché non si raggiunge la destinazione voluta
- si fanno più tentativi prima con TTL a 1 poi 2 ecc...
Concetto di probes(prove):
- il numero di probes è il numero di pacchetti che vengono inviati tutti con lo stesso TTL
	- serve per vedere magari più casistiche di percorso

il traceroute mi serve per capire quanto RTT ho dal i-esimo router 
##### Nuova versione ICMP v6
- miglioramenti vari 
- i nuovi router non fanno più troppa frammentazione quindi viene anche reso aggiornato sotto questo punto di vista

### Gestione delle reti
Una rete è:
- un sistema formato da migliaia di componenti software e hardware che interagiscono tra loro
- al posto di rete può anche chiamarsi Sistema Autonomo

>[!warning] Gestire e creare una rete è estremamente difficile
> - serve pianificare
> - monitorare
> - gestire le risorse economiche in modo intelligente
#### Componenti che gestiscono la rete
- Server di gestione
	- È il cervello del sistema.
	- Raccoglie, elabora e analizza le informazioni inviate dai dispositivi.
	- Invia comandi per configurare o modificare il comportamento dei dispositivi.
	- Coinvolge spesso **operatori umani**.

- Dispositivi di rete gestiti
	- Sono gli **switch, router, firewall, server**, ecc.
	- Hanno componenti hardware e software **configurabili** e **monitorabili**.
	- Ogni dispositivo ha un **agente** che comunica con il server.

- Dati
	- Rappresentano gli **“stati”** del dispositivo:
		- **Configurazione**: es. indirizzo IP, assegnato dall’amministratore.
		- **Dati operativi**: es. vicini OSPF, rilevati automaticamente.
		- **Statistiche**: es. traffico, errori, uptime.

- Agente di gestione
	- È il software **installato nel dispositivo gestito**.
	- Raccoglie e fornisce i dati di stato al server di gestione.
	- Riceve e applica i comandi del server.

- Protocollo di gestione di rete
	- Serve a **scambiare informazioni** tra server e dispositivi gestiti.
	- Il server lo usa per interrogare e comandare.
	- I dispositivi lo usano per inviare aggiornamenti e notifiche.
	- Esempi di protocolli: **SNMP**, **NetConf**, **RESTCONF**.
![[Pasted image 20250505194010.png]]
### Come si gestisce una rete?
Spieghiamo diversi modi per gestire una rete 
- se sei tipo uno che lavora per modificarle ecc...
#### Con CLI(Command Line Interface)
- Metodo più diretto e tradizionale
- L'operatore accede **manualmente** al dispositivo (es. via SSH) e inserisce comandi
- Supporta anche **script automatizzati**
- Molti dispositivi offrono anche un'interfaccia web
- **Vantaggio**: controllo preciso
- **Limite**: poco scalabile in reti grandi
#### Con SNMP/MIB
(Simple Network Management Protocol / Management Information Base)

- SNMP è un protocollo standard per la gestione dei dispositivi di rete.
- I dati sono organizzati in strutture chiamate **MIB** (oggetti informativi).
	- e informazioni che descrivono lo stato, la configurazione e le statistiche di un dispositivo di rete
- Il server di controllo interroga o modifica i dati tramite SNMP
- **Vantaggio**: standard, supportato da quasi tutti i dispositivi
- **Limite**: poco adatto alla gestione di configurazioni complesse
in poche parole hai un software sul server di controllo che comanda e gestisce i tuoi dispositivi senza che devi modificarli tu singolarmente
- puoi farlo ma non conviene
- piuttosto hai una interfaccia e dal server di controllo mandi dei comandi ai dispositivi
#### Con NETCONF/YANG
- Approccio **più moderno e astratto**
- Progettato per **gestire configurazioni** in modo robusto e coerente
- **YANG** è un linguaggio di modellazione dei dati
- **NETCONF** è il protocollo per leggere/scrivere dati compatibili con YANG su dispositivi remoti
- **Vantaggio**: gestione multi-dispositivo, configurazioni strutturate e coerenti
- **Ideale per reti complesse e dinamiche**
Con questo hai proprio un linguaggio di configurazione che migliora di molto il tutto

#### IN POCHE PAROLE
- con CLI vai proprio lì manualmente pezzo per pezzo ecc...
- con SMNP+MIB aumenti l'astrazione ma comunque devi manualmente fare determinate operazioni di monitoraggio ecc solo che lo fai dal server di gestione
- con NETCONF+YANG è tutto astratto e molto meno manuale
### SNMP spiegato meglio con anche MIB 

- I **dati di un dispositivo di rete** (sia operativi che di configurazione) sono organizzati in **moduli MIB**.
- Ogni **modulo MIB** è come un “file” che descrive un certo gruppo di informazioni (es. quelle relative a UDP).
	- Ne esistono **centinaia definiti dagli standard RFC** e moltissimi altri proprietari, forniti dai produttori di hardware.
- I dati sono definiti usando un linguaggio chiamato **SMI (Structure of Management Information)**.
nella foto qua sotto puoi vedere come sono strutturate delle variabili MIB

La MIB è come un “dizionario” di tutti i dati che un dispositivo di rete può rendere disponibili o modificabili via SNMP.

![[Pasted image 20250505195919.png]]

la **MIB ha una struttura ad albero**, gerarchica:
- Gli oggetti sono **nidificati** in rami (es. `system` → `sysDescr`, `sysUpTime`, ecc.).
- Ogni voce è **indicizzata da un OID** (Object Identifier), ad esempio `.1.3.6.1.2.1.1.1` per `sysDescr`.
Questo vuol dire che quando chiedi un dato a un dispositivo con SNMP, **gli indichi un OID** per sapere esattamente quale parametro vuoi leggere o modificare.
📍 Esempio: per sapere il nome del dispositivo, potresti chiedere `.1.3.6.1.2.1.1.5` (che corrisponde a `sysName`).
![[Pasted image 20250505204310.png]]
- usa per il trasporto UDP
	- vuole essere rapido

#### Tipi di messaggio SNMP
questi messaggi quindi vengono usati tipo per dire
"Dimmi quanti pacchetti UDP hai ricevuto"

|Tipo|Da... → A...|A cosa serve|
|---|---|---|
|GetRequest|Manager → Agente|Leggere un valore specifico|
|GetNextRequest|Manager → Agente|Navigare nella MIB|
|GetBulkRequest|Manager → Agente|Ottenere più dati in un colpo solo|
|SetRequest|Manager → Agente|Scrivere/aggiornare valori|
|Response|Agente → Manager|Rispondere a una richiesta|
|Trap|Agente → Manager|Segnalare un evento inaspettato|

#### Formati dei messaggi SNMP
![[Pasted image 20250708130045.png|400]]
![[Pasted image 20250505204432.png]]
come è fatto un **messaggio SNMP** (PDU – Protocol Data Unit), cioè cosa si invia realmente tra server e dispositivi:

✅ Tipi di messaggi 0,1,2,3 (per get/set):
- **Request ID**: per abbinare richiesta e risposta.
- **Error Status e Index**: indicano se qualcosa è andato storto (es. oggetto inesistente).
- **Name / Value**: la variabile da leggere o scrivere, con il suo valore.

🔔 Tipo 4 (Trap):
- Usato dai dispositivi per **inviare messaggi spontanei** al server (eventi).
- Include info come:
    - tipo di trap
    - **OID dell’evento** (es. “link down”)
    - **indirizzo IP dell’agente**
    - **timestamp**
    - **variabili coinvolte**
📌 Le trap sono fondamentali per **monitoraggio in tempo reale**: avvisano il server quando accade qualcosa (es. porta di rete disconnessa).


### NETCONF spiegato meglio
- Serve per gestire in modo attivo i dispositivi sulla rete
- Funziona tramite comandi come:
	- `retrieve` (recupera configurazioni o dati operativi),
	- `set`, `modify`, `activate` (modifica e attiva configurazioni).
- Supporta il **commit atomico**: 
	- tutte le modifiche vengono applicate **insieme**, oppure **nessuna viene applicata** se c’è un errore.
	- Può anche **interrogare statistiche**, ricevere **notifiche**, ecc.
- Usa il **modello RPC (Remote Procedure Call)**: 
	- il server invia richieste XML → il dispositivo risponde con `<rpc-reply>`.
- usa come protocollo di trasporto affidabile
	- SSH o TLS
#### Operazioni tipiche di NETCONF

| Operazione              | Funzione                                                                     |
| ----------------------- | ---------------------------------------------------------------------------- |
| `<get-config>`          | Legge la configurazione corrente (es. quella in esecuzione, detta `running`) |
| `<get>`                 | Legge i dati **operativi** (es. traffico, stato delle interfacce)            |
| `<edit-config>`         | Modifica una parte della configurazione                                      |
| `<lock>` / `<unlock>`   | Blocca/sblocca la configurazione per evitare conflitti da altre fonti        |
| `<create-subscription>` | Permette di ricevere notifiche automatiche (`<notification>`)                |

##### Esempio di scambi NETCONF in XML

Il dialogo tipico tra server e dispositivo segue questi passaggi:
1. `<hello>`: scambio iniziale di capability.
2. Scambio di richieste `<rpc>` e risposte `<rpc-reply>`.
3. Ricezione eventuale di `<notification>` (es. eventi, cambiamenti).
4. Chiusura della sessione con `<close-session>`.
![[Pasted image 20250505205227.png]]
➡️ Tutti i messaggi sono in formato XML.


##### Esempio concreto in XML
![[Pasted image 20250505205406.png]]

##### YANG (usato con netconf) spiegato meglio
(Yet Another Next Generation)**
Come abbiamo detto i comandi di NETCONF sono in XML ma le strutture dati che contengono i dati utili sono spesso in YANG
- è un linguaggio di modellazione dei dati, 
	- pensato appositamente per le reti. 
	- Serve a **descrivere la struttura, il tipo e i vincoli** dei dati che si possono gestire tramite NETCONF.
- **Definisce le strutture dati** che rappresentano configurazioni o stati operativi (interfacce, hostname, MTU, ecc.).
- Permette di generare automaticamente la struttura XML dei messaggi NETCONF.
- Garantisce **validità e coerenza** dei dati con vincoli tra campi (es. range, obbligatorietà, relazioni tra elementi).
- Come lo SMI (usato con SNMP), **YANG descrive i dati**, ma in modo **più ricco e moderno**.
![[Pasted image 20250505205702.png|400]]


###### Esempio vero e proprio di YANG+NETCONF
![[Pasted image 20250505205735.png]]
con yang:
- **definisce la struttura dei dati** che il dispositivo può accettare o restituire.
- È come dire: _“Nella configurazione del dispositivo ci sarà una sezione chiamata `system`, che contiene `login`, che a sua volta contiene un campo `message` (di tipo stringa)”_.
su netconf:
- Significa: _"Nel blocco system, nella sezione login, il messaggio da visualizzare al login è 'Good morning'"_.

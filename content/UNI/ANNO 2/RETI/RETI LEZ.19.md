#### LAN
sta per Local Area Network
- indica una zona di network limitata a una area ristretta come
	- una casa
	- una scuola
	- un ufficio
Ci sono due tecnologie principali che la usano:
- Ethernet 
- Wi-Fi
#### Indirizzi MAC
per identificare un determinato device abbiamo già nominato gli
- indirizzi IP a 32 bit con IPv4 oppure 128 con IPv6
- Essi vengono usati per effettuare inoltri al livello di rete
	- un esempio è tipo 128.119.40.136
poi ci sono gli indirizzi MAC che sostanzialmente hanno la funzione di identificare le interfacce per effettuare uno scambio dei frame tra interfacce connesse fisicamente, tipo stessa sottorete
- il MAC è a 48 bit ed è memorizzato nella ROM della NIC 
	- ovvero la memoria della scheda di rete del dispositivo
	- NIC = Network Interface Card
ad esempio:
- 1A-2F-BB-76-09-AD
Ciascuna interfaccia in una LAN ha un suo indirizzo MAC e indirizzo IP
- entrambi univoci

![[Pasted image 20250521180754.png]]

## Come vengono scelti gli indirizzi IEEE
- L’**IEEE** (ente internazionale) si occupa di **gestire lo spazio degli indirizzi MAC** per garantire che siano **univoci** nel mondo.
- I **produttori di schede di rete (NIC)** comprano dei “blocchi” di indirizzi MAC da IEEE.
    - In pratica, ogni produttore riceve un **prefisso identificativo univoco**, che userà per assegnare gli indirizzi ai suoi dispositivi.
Mentre gli indirizzi IP possono variare rispetto a quale rete siamo connessi, gli indirizzi MAC invece sono univoci e portabili

#### Come posso sapere l'indirizzo MAC di una interfaccia se so solo quello IP?
Utilizzo un protocollo chiamato ARP che ha una tabella chiamata ARP 
- in questa tabella
	- Ogni nodo IP sulla LAN ne ha una per ciascuna interfaccia
	- Questa tabella ha una corrispondenza tra Indirizzo IP e MAC e anche il rispettivo TTL
		- `<indirizzo IP,indirizzo MAC, TTL>`
		- il TTL rappresenta il (Time To Live) ovvero dopo quanto questa mappatura verrà dimenticata nella tabella
			- di solito 20 min

#### Questo protocollo in azione
![[Pasted image 20250521214402.png]]
1. A invia un messaggio in broadcast chiedendo chi è B
![[Pasted image 20250521214436.png]]
2. B risponde e invia il suo indirizzo MAC
![[Pasted image 20250521214459.png]]
3. A può popolare la sua tabella 

#### ARP SPOOFING o POISONING
- Un attaccante **invia risposte ARP false** (contraffatte) a dispositivi della rete.
- Queste risposte fanno credere a un nodo che **un certo IP è associato a un MAC sbagliato** (cioè quello dell’attaccante).
- Il nodo aggiorna **senza controllare** la sua cache ARP → qui nasce la vulnerabilità.
- Il protocollo ARP è **senza stato**: ogni nodo **accetta qualsiasi risposta ARP ricevuta**, anche se **non l’ha chiesta**.
Un attaccante ora può:
1. attacchi DoS
- Associa **tanti indirizzi IP allo stesso MAC (il suo)** → **sovraccarica** la scheda di rete, che si blocca.
    
1. Man in the Middle
- L’attaccante fa in modo che **il traffico destinato a un nodo passi prima da lui**:
    - Può **intercettare**, **modificare** o **registrare** i dati,
    - Poi **li inoltra al vero destinatario**, così nessuno si accorge dell'attacco.
##### Scenario dove voglio inviare il datagramma a un nodo esterno della sottorete
![[Pasted image 20250521220219.png]]
- DHCP era quel server che prevedeva che appena un dispositivo si connette a una rete gli viene assegnato un indirizzo IP ecc...
![[Pasted image 20250521220227.png]]
![[Pasted image 20250521220234.png]]
![[Pasted image 20250521220242.png]]
![[Pasted image 20250521220253.png]]
![[Pasted image 20250521220301.png]]
## Ethernet
- Utilizzata per le reti LAN cablate
- nel tempo si è evoluta e ora può raggiungere fino a 400 Gbps
##### Come sono topologicamente disposti i dispositivi che usavano una Ethernet
- a bus
	- era popolare fino alla metà degli anni 90 
	- tutti i nodi erano nello stesso dominio con collisione
- topologia a stella con hub
	- popolare fino ai 2000
	- i nodi sono interconnessi da un hub che rimandava il segnale a tutti
	- stesso dominio di collisione
- commutata con switch
	- usata oggi
	- uno switch di livello 2 al centro
	- ognuno ha un suo protocollo ethernet, i nodi non si scontrano tra loro
![[Pasted image 20250522154942.png]]
#### Un frame ethernet
Quando un dispositivo (es. un PC) vuole inviare dati (es. un datagramma IP), **la scheda di rete incapsula quei dati in un frame Ethernet**, con queste sezioni:
![[Pasted image 20250522155625.png]]


| **Campo**            | **Dimensione** | **Contenuto**                       | **Funzione**                                                        |
| -------------------- | -------------- | ----------------------------------- | ------------------------------------------------------------------- |
| **Preambolo**        | 8 byte         | `7×10101010` + `1×10101011`         | Sincronizza il ricevente e segnala l'inizio del frame               |
| **MAC destinazione** | 6 byte         | Indirizzo MAC del destinatario      | Indica a chi è diretto il frame                                     |
| **MAC sorgente**     | 6 byte         | Indirizzo MAC del mittente          | Indica chi ha inviato il frame                                      |
| **Tipo**             | 2 byte         | Es. `0x0800` (IPv4), `0x0806` (ARP) | Specifica il tipo di protocollo incapsulato nei dati                |
| **Dati (Payload)**   | 46–1500 byte   | Datagramma IP, pacchetto ARP, ecc.  | Dati del livello superiore; se <46 byte viene aggiunto padding      |
| **CRC**              | 4 byte         | Codice di controllo                 | Verifica errori di trasmissione con algoritmo di ridondanza ciclica |

- Il **frame minimo (senza preambolo)** è di **64 byte**
	- Il **massimo è 1518 byte** (senza estensioni tipo jumbo frame)
- Il **preambolo non fa parte del conteggio del frame Ethernet vero e proprio**, ma è comunque trasmesso
Quando qua sopra si parla di padding si intende
- una **sequenza di byte aggiunti artificialmente** alla fine del campo **dati (payload)** **per raggiungere una lunghezza minima** del frame Ethernet.
##### Ethernet e la sua sicurezza
Essa è senza handshake
- quando si connette alla scheda di rete non effettua nessun controllo e i dati vengono trasmessi e basta sperando che arrivino
- se un frame vene perso o scartato non esistono ACK o NACK per segnalarlo
Infatti vengono usati i servizi soprastanti ad esso come il TCP che consente le varie ritrasmissioni ecc...
Anche qui abbiamo un MAC ovvero un Media Access Control(non l'indirizzo)
- che spesso usa la CSMA/CD per gestire più dispositivi connessi allo stesso cavo senza però collisioni e anche
- **Unslotted** = **non ci sono slot di tempo** predefiniti.
	- I dispositivi **possono provare a trasmettere in qualsiasi momento**.
#### Gli standard del livello Ethernet
- Tutti gli standard Ethernet **usano lo stesso frame Ethernet**.
- Cambiano:
    - **Velocità**: da 2 Mbps a 100 Gbps
    - **Mezzo fisico**: cavo coassiale, doppino, fibra ottica
    - **Limiti di distanza** e propagazione
	    - sostanzialmente il cavo in base alla sua lunghezza presenta delle limitazioni
	    - i cavi ethernet si dividono in categorie chiamate cat
Vi è anche il concetto di dominio di collisione
- una zona della rete dove si può verificare una collisione tra vari frame ethernet
- se vi è un ritardo troppo grande tra andata e ritorno il sistema che controlla le collisioni potrebbe perdere lo slot time e quindi andare alla prossima interfaccia e fregarsene di eventuali errori
in questa foto possiamo vedere come ci sono degli standard al livello fisico che si differenziano in base al tipo di doppino in rame o fibra
mentre invece nella parte di collegamento viene tutto visto come un unico frame
![[Pasted image 20250522163855.png]]
### Tempi di rilevazione delle collisioni
Nella rete Ethernet, le collisioni sono rilevabili solo **entro un certo tempo massimo**. Questo limite è di **512 bit time**, che equivale a:
- 512 bit / 100 Mbps = **5,12 microsecondi** (cioè il tempo per trasmettere 512 bit)
Per calcolare se la collisione viene rilevata per tempo vengono presi da questa tabella
- i cavi con un ritardo 111.2 bit time
- due adattatori TX/FX con ritardo 127
- un margine di sicurezza per tenere conto di altre fonti
- eventuali ripetitori con un ritardo di 140
- sommando tutto possiamo vedere che fa sotto i 512 bit time quindi va bene
NOTA: i bit time indicano quanto tempo ci vuole a inviare un solo bit
![[Pasted image 20250522165448.png]]

![[Pasted image 20250522164909.png]]
#### Nella tabella sopra abbiamo detto che
un cavo di 100m UTP(**Unshielded Twisted Pair**) cat.5 ha un round trip delay di 111.2 bit time dimostriamolo con un po' di calcoli
- per round trip delay si intende che se un cavo é di 100m allora il tempo di andata e di ritorno del cavo è su 200m
![[Pasted image 20250522165949.png|400]]

![[Pasted image 20250522170111.png]]
### Switch Ethernet
il router lavora sul livello di rete mentre invece lo switch lavora sul livello di collegamento
- esso ha un ruolo attivo:
	- memorizza e inoltra frame Ethernet
		- detto anche store and forward
	- legge l'indirizzo MAC di destinazione e lo inoltra a quest'ultimo
	- sfruttando anche algoritmi come il CSMA/CD per gestire accessi ai canali
inoltre:
- **è Trasparente**: gli host collegati **non si accorgono** della sua presenza.
- **Supporta collegamenti eterogenei**: diverse velocità, diversi tipi di cavi (rame, fibra...).
- **è Plug and play + autoapprendimento**:
    - Non devi configurarlo manualmente.
    - Lo switch **impara automaticamente** quali MAC sono collegati a quali porte.
Gli host hanno ognuno una connessione dedicata a questi switch
- lo switch mette su un buffer questi pacchetti 
- il protocollo Ethernet è presente su ogni collegamento e vi sono due sostanziali differenze
##### Full duplex o Half duplex
sostanzialmente per Full duplex si intende quando un dispositivo può sia inviare che ricevere contemporaneamente mentre invece è Half quando può fare una sola cosa per volta
- nel caso di Half è necessario regolare il tutto con gestione di collisioni
![[Pasted image 20250522172116.png]]
in questa foto le due A possono parlare senza collisioni e anche le due B
invece A-> A' e C-> A' non può avvenire perché avverrebbe una collisione
![[Pasted image 20250522172142.png]]
#### Come fa lo switch a sapere quali nodi sono raggiungibili a quale interfaccia?
![[Pasted image 20250522172336.png]]
#### Lo switch impara da solo le varie tabelle(infatti è pul-and-play)
![[Pasted image 20250522172406.png]]

### Filtraggio e inoltro dei frame dallo Switch
Cosa fa lo switch quando riceve un frame:
1. Salva il MAC sorgente della porta che lo ha inviato
2. Aggiorna quindi la Switch Table
3. Cerca sulla tabella se già sa dove inviarlo
4. se il destinatario è sulla stessa porta del mittente non serve inviarlo di nuovo perché sicuramente è arrivato anche al destinatario senza uso dello switch quindi lo scarta
5. se è da un'altra porta lo inoltra facendo lo switching selettivo
6. se non lo conosce fa una operazione di flood, invia a tutte le porte tranne quella del mittente per dire "chi sei?"
#### Esempio di autoapprendimento fatto dal prof
![[Pasted image 20250522173215.png]]
![[Pasted image 20250522173221.png]]
![[Pasted image 20250522173255.png]]
### Switch vs Router
- Entrambi lavorano in modalità store and forward
	- uno si interfaccia con i dispositivi del livello di rete
	- uno con quelli di collegamento
- Entrambi hanno tabelle di inoltro
	- uno usa algoritmi di instradamento e indirizzi IP
	- l'altro usa autoapprendimento e la tabella di Switching con indirizzi MAC e flooding
Topologia della rete:
- i router possono gestire i cicli della rete grazie ai vari protocolli e al campo TTL time to live presente nei pacchetti IP, evita che circolino all'infinito
- gli switch devono essere collegati senza presenza di cicli logici 
- oppure devono usare il protocollo **Spanning Tree Protocol (STP)** per evitare **loop di frame broadcast** che non possono essere fermati (perché i frame Ethernet non hanno TTL).
Numero di nodi:
- i router usano instradamento di tipo gerarchico, gestiscono grandi nodi in modo efficiente grazie ad aggregazioni di indirizzi IP
- gli switch devono memorizzare ogni indirizzo MAC nella tabella di commutazione, troppi dispositivi=tabelle troppo grandi
Isolamento del traffico:
- i router non fanno broadcast tra reti diverse, inoltrano pacchetti indirizzati solo se la rete è conosciuta nella tabella di routing, le reti quindi sono isolate e più sicure
- gli switch se non conoscono l'indirizzo MAC di destinazione inviano frame in modalità broadcast su tutte le porte, questo crea problematiche come connessioni a effetto valanga se ci sono altri switch collegati
![[Pasted image 20250522173427.png]]
#### VLAN

Cosa succede se i dispositivi di una rete LAN aumentano e sono solo collegate da uno switch?
- tutti i dispositivi sono su un unico dominio di broadcast, se avviene un broadcast tutti lo ricevono
- decrescita della sicurezza e della privacy
![[Pasted image 20250522174522.png]]
Soluzione: Le VLAN
- le Virtual Local Area Network permettono
- di rimanere nella stessa rete
	- ma creare delle indipendenze logiche usando switch diversi
- Questo semplifica la gestione con più dispositivi e concede maggiore flessibilità
![[Pasted image 20250522174934.png]]
### VLAN basate sulle porte
Gli switch che supportano le funzionalità VLAN possono essere configurati per definire più LAN virtuali ma su una unica infrastruttura fisica, usando un singolo switch come se però ce ne fosse più di uno
- questo concede isolamento del traffico e le varie porte possono essere assegnate in modo dinamico
- **due dispositivi su VLAN diverse non possono comunicare direttamente**, nemmeno se collegati allo stesso switch: serve **un router (o uno switch di livello 3)** che si occupi di instradare i pacchetti tra le due VLAN, proprio come se fossero due reti distinte.
![[Pasted image 20250522175052.png]]
### VLAN su più switch
connettere tra di loro due reti che appartengono alla stesa VLAN ma non presenta troppa scalabilità perché ogni switch che colleghiamo toglie una porta allo switch principale
![[Pasted image 20250522175240.png]]
Una **porta trunk** è una porta speciale che collega **due switch** e permette loro di:
- **scambiarsi frame Ethernet appartenenti a più VLAN diverse**
- mantenendo l’informazione su **quale VLAN appartiene ogni frame**
### ID VLAN
Di default i frame ethernet non hanno come dettaglio l'ID VLAN
- identificativo che dice a quale VLAN stai
- esso viene aggiunto da un protocollo che aggiunge al frame un tag VLAN che dice proprio a quale ID appartiene un determinato frame
- il frame ora si chiama VLAN 802.1Q
![[Pasted image 20250522175930.png]]

#### EVPN
![[Pasted image 20250522180154.png]]
È una **tecnologia di tunneling** che permette di:
- **Collegare reti Layer 2 (Ethernet)** che si trovano in luoghi fisicamente diversi (es. data center a Sunnyvale e a Bangalore).
- Usare una **rete IP Layer 3 preesistente** (chiamata _underlay_) come mezzo di trasporto.
##### Come funziona
1. I **frame Ethernet** (Layer 2) vengono **incapsulati** dentro pacchetti **IP** (Layer 3).
2. Questi pacchetti IP viaggiano attraverso una rete Layer 3 (come Internet o una WAN).
3. Quando arrivano a destinazione, il frame Ethernet originale viene **estratto** e consegnato allo switch remoto, come se provenisse da una rete locale.
serve per:
- **Allungare reti Layer 2 su distanze geografiche**.
- **Unificare VLAN remote** (utile in ambienti cloud, datacenter, multi-sito).
- **Separare logicamente** più clienti o dipartimenti usando **VLAN over IP**.


- Come inviare un datagramma a un nodo non adiacente nella rete
1. **Verifica della destinazione** -> se il destinatario si trova in un'altra sottorete, il frame va instradato tramite un router gateway,
2. **Creazione del datagramma IP + Incapsulamento in un frame** -> i vari IP (sorgente e destinatario), i vari MAC (sorgente e destinatario) e il MAC del router si ottiene tramite ARP,
3. **Ricezione e analisi da parte del router** -> il router riceve il frame, estrare il datagramma e si accorge che l'IP di destinazione non è il suo,
4. **Instradamento verso la rete di destinazione** -> il router incapsula di nuovo il datagramma e spedisce il frame alla giusta interfaccia e quindi poi al giusto destinatario
### LIVELLO APPLICAZIONE
- **definizione di internet**
	- <font color="#f79646">Infrastruttura</font> composta da un insieme di reti interconnesse tra loro
- **Host**
	- ospitano le applicazioni di rete
	- si trovano ai bordi di internet
	- comunicano attraverso pacchetti di dati
	- inoltrati da altri dispositivi come router e switch
- **ISP**
	- organizzazioni che offrono l'accesso a internet a utenti o varie aziende
	- sono interconnessi tra loro per garantire il corretto funzionamento della rete
	- se locali sono nei margini della rete
	- se globali sono nel nucleo della rete
- **Commutazione di una rete**
	- Tecniche di scambio di pacchetti seguendo determinate regole
	- Commutazione di pacchetto
		- Il singolo messaggio viene diviso in pacchetti di L bit
		- viene inviato il singolo pacchetto senza flussi di bit
	- Commutazione di circuito
		- viene dedicato un collegamento tra mittente e destinatario e vengono inviati i bit in sequenza
- **Lan o Wan**
	- Local Area Network
	- Wide Area Network
- **Nucleo di rete**
	- È un insieme di commutatori di pacchetti e link tra i vari host che sono poi collegate alle varie periferie di rete
	- gli utenti non ci accedono direttamente
	- azioni:
		- inoltro
			- attraverso una tabella di inoltro, invia i pacchetti a una determinata interfaccia
		- instradamento
			- indica il percorso che viene fatto da una serie di router per arrivare a destinazione da una radice
			- fatto attraverso algoritmi
	- viene calcolato instradamento e poi inoltro
![[Pasted image 20250705102609.png]]
- **sicurezza di internet**
	- una interfaccia di rete, quindi collegata alla rete
		- può vedere tutti i pacchetti che ci passano
		- wireshark
	- ip spoofing
		- fingo di avere un'altro indirizzo IP nella rete
- **protocolli**
	- insieme di regole che definiscono i metodi per la comunicazione tra dispositivi nella rete
- **Divisione in livelli della TCP/IP pila protocollare**
	- *Applicazione*
		- supporto alle applicazioni di rete con protocolli come HTTP che inviano <font color="#f79646">messaggi</font>
	- *Trasporto*
		- Trasferimento di <font color="#f79646">segmenti</font> tra processi come UDP e TCP
	- *Rete*
		- trasporto di <font color="#f79646">datagrammi</font>, pacchetti di rete tra host con indirizzo IP e protocolli IP
	- *Collegamento*
		- Trasferimento di <font color="#f79646">frame</font> tra dispositivi vicini
	- *Fisico*
		- Trasferimento di bit veri e propri su link
- **incapsulamento dei dati tra i vari livelli**
![[Pasted image 20250705103837.png]]




### Livello di applicazione
- **definizione**
	- È un livello nella pila protocollare
	- interagisce con l'utente o con le applicazioni di rete
		- fornendo i servizi di rete ad essi
- **architetture**
	- client server chi sono?
		- sono due attori detti host all'interno della rete che comunicano tra loro scambiandosi messaggi
		- server
			- deve essere sempre attivo e deve rispondere alle richieste degli host
			- indirizzo IP noto dai client 
		- client
			- comunica con i server inviando richieste 
	- peer-to-peer
		- architettura che prevede un insieme di host che fanno sia da client che da server, sono detti peer
			- ogni peer condivide i file che ha già scaricato ai peer candidati più vicini
			- utilizza determinate tecniche per ottimizzare lo scambio tra peer
		- *torrent*
			- file che ha tracker dei i vari peer
		- peer-to-peer vs client server
			- Client server
				- lineare senza variazioni
			- peer-to-peer
				- dipende da il numero di utenti che condividono i dati e che li scaricano
		- *tit for tat*
			- tecnica di ottimizzazione del peer-to-peer
			- in un intervallo di secondi vengono ogni volta definiti i peer che sono destinati a scambiare i chunk
				- ogni tanto ne viene scelto uno a caso per vedere se era candidato e utile
- **processi**
	- sono un programma in esecuzione su un host
		- accedono alla rete tramite il livello di trasporto
		- ma per comunicare con il livello di applicazione dove abbiamo le varie applicazione di rete vengono usate le socket
			- sono interfacce software, permettono di comunicare con i processi che lavorano al livello di trasporto, quindi fanno da tramite con il livello di applicazione
			- sono identificate da una coppia formata da
				- *IP*
					- identifica l'host
				- *Porta*
					- identifica l'applicazione 
					- alcune porte sono già standardizzate per alcune applicazioni
![[Pasted image 20250318133006.png|400]]

- **protocollo del livello di applicazione**
	- si dividono in 2 tipi
		- proprietari
			- non sono noti e vengono usate da applicazioni private tipo skype
		- pubblici
			- sono noti e standardizzati tipo HTTP
	- vertono su
		- sicurezza
			- i livelli di trasporto non garantiscono chissà che sicurezza ma quelli di applicazione la possono migliorare con cifrature tipo TLS
		- troughput minimo garantito
		- perdita di messaggi
		- sensibilità al fattore tempo
	- applicazioni che usano protocolli di trasporto
		- HTTP usa TCP
		- SMTP usa TCP
		- Giochi interattivi TCP e UDP
		- VoIP usa UDP
- **HTTP**
	- alla base delle applicazioni web
		- sfrutta il paradigma client server
		- presente sulla porta 80
		- consente lo scambio di messaggi di richiesta HTTP 
		- vengono scambiare risorse 
	- passaggi che compongono una richiesta HTTP
		- il client tenta di aprire una connessione TCP al server sulla porta 80, creando una socket, successivamente il server la riceve e accetta o meno la connessione, il client invia una richiesta HTTP al server, il server fornisce la risorsa, viene chiusa la connessione TCP
	- MESSAGGIO HTTP
		- è composto da
			- riga di richiesta
				- versione HTTP, URL richiesto, metodo HTTP usato(get put...)
			- intestazione
				- informazioni riguardo chi effettua la richiesta, formato, se ci sono cookie o meno ecc...
			- corpo del messaggio
				- contiene i dati inviati dal server
	- Metodi HTTP
		- POST
		- GET
		- HEAD
		- PUT
	- Versioni a grandi linee
		- 1.0
			- ogni connessione creata TCP era uno scambio di un solo messaggio
			- non persistenti, quindi la connessione termina, gli altri sono persistenti
		- 1.1
			- consentiva di fare GET multiple di dati con politica FIFO
		- 2.0
			- senza richieste venivano inviati più messaggi ma con priorità non FIFO
			- i messaggi venivano inviati alternati tra loro divisi in frame, invio interlacciato
		- 3.0
			- usa UDP con QUIC al livello di applicazione per gestire problemi di sicurezza e perdita dei messaggi
![[Pasted image 20250318183006.png|400]]

- **RTT**
	- tempo che impiega un pacchetto per andare dal client al server e dal server al client
	- variabile in base a eventuali congestioni ecc...
![[Pasted image 20250318151455.png]]

- **Codici di stato**
	- per ogni errore esiste un codice di stato che si trova nell'intestazione dei messaggi
	- 1xx messaggi informativi,
	- 2xx successo, 
	- 3xx risorsa spostata, 
	- 4xx errore, 
	- 5xx errore server
- **I cookie**
	- il protocollo HTTP è stateless, quindi login non funzionano ad esempio
	- per salvare eventuali client vengono o salvati gli stati in memoria sui due dispositivi client e server oppure si usano i cookie
		- i cookie sono codici identificativi per client
		- i cookie dopo la prima connessione effettuata vengono scambiati nell'header delle richieste HTTP
		- essi vengono salvati in un database dei server e vengono forniti al client, il client salverà il proprio cookie ad esempio nel browser
![[Pasted image 20250318185425.png|300]]

- **Web Cache**
	- intermediario tra client e server
	- se ha già una risorsa di una eventuale richiesta HTTP la fornisce senza interpellare il server effettivo
	- ogni risorsa ha un TTL time to live
	- può essere locale, interna al host client oppure un server come i proxy che fanno da client
	- vengono usate per migliorare l'efficienza dei server e evitare congestioni
![[Pasted image 20250318192553.png|400]]

- **Posta elettronica**
	- applicazione che simula lo scambio di lettere attraverso user agent e mail server
		- tra server di posta avviene uno scambio attraverso SMTP
		- uno user agent per inviare una mail la invia al suo server mail attraverso il protocollo SMTP, a sua volta questo server lo invia al server mail del destinatario attraverso il protocollo SMTP, per prelevare le mail viene usato IMAP dallo user agent
		- perché SMTP non può fare pull
	- passaggi SMTP
		- usa il protocollo TCP
			- effettua prima di tutto il TCP handshake con la richiesta TCP che viene accettata
			- successivamente viene effettuato un handshake SMTP per presentare le due parti
			- viene inviato il messaggio, come corpo ha il contenuto della mail
	- HTTP VS SMTP
		- HTTP è di tipo pull, il client riceve dei dati solo se li richiede
		- SMTP è di tipo push, il client riceve dei dati anche se non li richiede(server mail del destinatario)
![[Pasted image 20250321183245.png|500]]

- **DNS**
	- Servizio di rete decentralizzato(con più server) che consente la conversione di indirizzi URL in IP attraverso un Database 
	- Ci sono 3 server noti di tipo DNS
		- root
			- indirizza a quale server TLD riferirsi
		- Top Level Domain
			- forniscono la parte finale dei domini e rimandano a quelli autoritativi che sono meno generici, hanno solo .com ecc...
		- Autoritativi
			- Server DNS che contengono indirizzi IP completi richiesti
	- richiesta DNS può essere
		- ricorsiva
			- i server DNS a partire da quello locale si risolvono da soli interrogandosi a vicenda
		- iterativa
			- il server DNS locale interroga i vari Server DNS personalmente
![[Pasted image 20250321190924.png]]
![[Pasted image 20250321192921.png]]

- **URL**
	- indirizzo che contiene sito di riferimento che poi dovrà essere convertito in IP
	- risorse di riferimento richieste dopo lo /
- **streaming video**
	- streaming invio di sequenze di dati che vengono riprodotte
	- sequenza di immagini codificate per ottimizzare il peso
	- bitrate
		- unità di misura che indica quanti bit vengono trasmessi al secondo
		- fisso o variabile
	- viene usato TCP per evitare perdite
		- con HTTP può essere scelta la qualità scegliendo la determinata risorsa
	- CDN
		- server nel mondo che hanno stessi contenuti video per rispondere alle eccessive richieste
### LIVELLO DI TRASPORTO
### Livello di trasporto
- **introduzione breve**
	- livello che consente la comunicazione tra processi su host differenti mediante protocolli e segmenti
- **tecniche di smistamento dei dati mediante IP+porta**
	- multiplexing 
		- effettuato al lato mittente
		- i segmenti di ciascun processo vengono compattati e inviati, differenziati poi da una intestazione
	- demultiplexing
		- effettuato al lato destinatario
		- tramite le intestazioni dei singoli segmenti viene definito a quale processo socket destinare quel determinato segmento
		- si divide in 
			- con connessione
				- vengono creare socket passive
			- senza
				- è sufficiente IP+porta
![[ms-teams_hVpBKBk0sN.png|300]]
![[ms-teams_j0jUvWaTsw.png|300]]

##### UDP
- **definizione**
	- Protocollo di trasporto veloce senza handshake, con ritrasmissione
- **utilizzi**
	- DNS
	- DHCP
	- HTTP/3 con QUIC
- **struttura del segmento**
	- Intestazione, in cui abbiamo porta di origine, porta di destinazione, lunghezza, checksum
		- origine serve solo se si vuole inviare eventualmente una risposta
	- dati dell'applicazione
- **checksum**
	- spazio di dati all'interno di UDP con lo scopo di rilevare errori e eventualmente ritrasmettere 
	- il mittente calcola la checksum e la invia al destinatario
	- il destinatario calcola a sua volta la checksum e la confronta con quella inviata dal mittente
		- se tutti i bit sono a 1 allora non vi sono errori
![[Pasted image 20250406160244.png]]

##### Modello teorico RDT
![[Pasted image 20250406162511.png]]

- **affidabilità con RDT**
	- RDT Reliable Data Transfer, modello astratto che indica come gestire un canale inaffidabile per garantire la corretta trasmissione dei dati è diviso in versioni 
		- esso venne poi usato come idea per TCP
	- 1.0
		- canale affidabile, mittente e destinatario devono solo aspettare di essere interpellati per inviare o ricevere dati
	- 2.0
		- canale inaffidabile ma con segmenti che vengono inviati in ordine, vengono introdotti ACK e NAK 
		- il mittente prima di rimettersi in attesa di inviare un nuovo segmento attende uno di questi due segnali
		- il destinatario invia ACK o NAK se i dati ricevuti sono ok oppure corrotti
		- problematiche:
			- i segnali possono essere anche essi corrotti
			- nel dubbio viene inviato ma presenterebbe delle duplicazioni
	- 2.1
		- introduce numero di sequenza per evitare duplicazioni
		- il numero di sequenza viene usato tra mittente e destinatario per capire se sono sullo stesso numero di sequenza
		- il mittente invia un pacchetto con un numero di sequenza 0 o 1, si aspetta un ACK con lo stesso numero dal destinatario se è differente allora ci sono problematiche
		- sono ancora usati ACK e NAK
	- 2.2
		- rimuove i NAK, se invio un ACK non corrispondente è come se sto inviando un NAK
	- 3.0
		- aggiunge RTT, ovvero una soglia di tempo per attendere un segnale necessario per effettuare una ritrasmissione
		- usata per gestire perdite e non solo errori
- **trasferimento dati con stop and wait  vs pipeline**
	- <font color="#f79646">stop and wait</font> viene inviato un segmento e si attende un riscontro per esso
	- <font color="#f79646">pipeline</font>, vengono inviati in sequenza i segmenti e poi vengono accumulati su una pipe i rispettivi ACK, nel caso del mittente, per il destinatario i veri e propri segmenti
![[Pasted image 20250406184132.png|500]]

- **GBN**
	- protocollo teorico che prevede utilizzo di finestre 
		- per tenere conto dei segmenti confermati, in attesa di conferma, ancora da inviare
		- se in una sequenza di N segmenti un segmento non viene confermato, il mittente dovrà, dopo il timeout rinviare tutti da quel segmento in poi
![[Pasted image 20250406185245.png]]

- **con ripetizione selettiva**
	- migliora la GBN
	- ogni segmento è una istanza a se numerata, non devo reinviare tutta la sequenza ma solo il singolo interessato
![[Pasted image 20250406193400.png]]
#### TCP
- **introduzione**
	- protocollo di trasporto affidabile basato su connessione tra gli host e correzione di errori
- **dettagli sul segmento MSS e MTU**
	- MSS rappresenta la massima dimensione di un segmento, escludendo l'intestazione
	- MTU rappresenta la massima dimensione di un datagramma del protocollo IP che racchiude anche il segmento
![[Pasted image 20250408124654.png|300]]

- **segmento PDU del TCP**
	- si divide in 
		- intestazione
			- numeri di porta origine e destinazione checksum, ack, numero di sequenza, receive window
		- corpo, i dati effettivi
![[Pasted image 20250408130449.png]]

- **numero di sequenza e ACK**
	- ogni byte è numerato sequenzialmente
	- il campo numero di sequenza include il primo byte di sequenza
	- il campo ACK include l'ultimo byte a essere confermato
- **RTT Round Trip Time**
	- soglia di tempo che deve attendere un mittente prima di effettuare un reinvio se non si ricevono segnali 
	- viene stimato calcolando una media degli ACK ricevuti
- **Controllo e gestione del flusso**
	- TCP permette al mittente di gestire il flusso di dati che può ricevere il buffer  del destinatario, per evitare saturazioni del buffer
	- receive window
		- campo dell'intestazione TCP per definire quanti byte può ancora ricevere il buffer del destinatario
![[Pasted image 20250408135957.png|400]]

- **TCP con handshake**
	- procedura che instaura un collegamento sicuro tra due host 
	- malgrado aumenti l'overhead dovuto a questa procedura diminuisce notevolmente la perdita di dati attraverso segnali di ACK scambiati tra le due parti
	- 2 vie
		- il mittente invia una richiesta di collegamento al destinatario
		- il destinatario manda una conferma con un segnale di ACK
		- la connessione è stabilita e i due possono comunicare fino alla chiusura
		- problemi: perdita del segnale di ACK o di richiesta 
	- 3 vie
		- come quello a 2 vie solo che adesso anche il mittente deve inviare a sua volta un ACK dell'ACK del destinatario e per iniziare la sincronizzazione viene usato un Synbit che deve essere uguale tra i due
			- questi ACK sono identificati da 
			- ACKbit 
				- semplice ACK 1=NAK       0=ACK
			- ACKnum
				- indica fino a quale sequenza di byte ha ricevuto i dati
		- Bit di reset 
			- in caso di errori è possibile terminare repentinamente la connessione stabilita
		- Chiusura connessione TCP
			- Viene inviato un Finbit=1
			- il destinatario invierà un Finbit=1+ACK
			- il mittente invia un ACK e basta
![[Pasted image 20250408142333.png]]
![[Pasted image 20250408142831.png]]

- **attacco Syn flood**
	- vengono inviate molteplici richieste di handshake per far crashare un server
	- si risolve con i cookie
		- il client dovrà rispondere con il cookie assegnato altrimenti non alloca memoria
#### Congestione
- **definizione**
	- fenomeno che avviene quando il carico da inviare supera la capacità di risorse che supporta la rete
- **scenario 1**
	- breve descrizione
		- router con buffer illimitato, ogni coppia mittente/destinatario ha il suo collegamento al router
		- se aumenta il troughput più di R/2 si presentano rallentamenti
![[Pasted image 20250410175431.png]]
- **scenario 2**
	- breve descrizione
		- buffer del router limitato 
		- ritrasmissioni presenti al livello di trasporto non di applicazione
		- si divide in 3 sotto-scenari
			- caso 1 ideale, buffer libero
				- i pacchetti vengono inviati regolarmente
				- il mittente sa quando il buffer è pieno
			- caso 2, buffer pieno e conoscenza meno perfetta della situazione
				- vengono scartati pacchetti e ritrasmissioni
			- caso 3, timeout prematuro
				- timeout non impostato correttamente
				- duplicazioni
![[Pasted image 20250410180557.png]]
![[Pasted image 20250410181647.png]]
- **scenario 3**
	- breve descrizione
		- 4 host 
		- percorsi multi hop
		- timeout e ritrasmissioni
	- problematiche
		- host adiacenti a router prendono tutta la banda possibile
![[Pasted image 20250410182434.png]]

- **controllo della congestione 2 approcci**
	- *end-to-end*
		- il controllo della congestione è *demandato solo al mittente*, che effettuerà dei calcoli
			- della finestra di ricezione prende solo ed esclusivamente il cwnd, ovvero i byte che devono ancora essere ACK e anche quelli non inviati
			- calcolando poi cwnd/RTT riesce a definire circa il tasso di invio
			- non preciso
	- *assistito dalla rete*
		- il router invia dei *pacchetti informativi detti choke* al destinatario, lui li rimanda il mittente insieme a eventuali ACK
		- informano del loro stato di congestione
		- usato in TCP ECN
- **gestione del tasso di invio.**
	- concetto di AIMD
		- Additive increase Multiplicative Decrease
		- questo concetto regola dinamicamente gli MSS
		- Maximum Segment Size, ovvero regola quanti segmenti può inviare prima di attendere una ricezione
		- inizia da 1 aumenta additivamente ad ogni RTT e appena avviene un fault gli cwnd vengono dimezzati
![[Pasted image 20250411162431.png]]

- **fasi di gestione del tasso di invio**
	- *slow start*
		- si inizia piano e poi ad ogni RTT cwnd si raddoppia
	-  *congestion avoidance*
		- viene usata una variabile`sstresh` che definisce un limite per cui si smette di crescere esponenzialmente(slow start) ma linearmente
	- *gestione errori*
		- se non si ricevono ACK(timeout)
			- entra in timeout e dimezza `sstresh` e cwnd=1
		- se riceve 1 o 2 ACK duplicati
			- prova semplicemente a ritrasmetterli
		- se invece ne riceve 3 duplicati
			- aumenta notevolmente cwnd per aumentare il tasso di trasmissione
			- poi entra in fast recovery
	- *fast recovery*
		- quando si verifica una perdita, triplo ACK duplicato si entra in fast recovery
		- questa fase dura 1RTT per attendere l'ack del pacchetto perso 
		- quindi si entra in congestion avoidance partendo da 
			- $cwnd=cwnd \ del \ blocco \ precedente+3 \ tutto \ fratto \ 2$
- **evoluzioni TCP**
	- TCP Reno
		- implementazione di TCP che utilizza un algoritmo con fast recovery e dimezzamento di 1 MSS quando si ha un ACK
	- TCP Cubic
		- utilizza $W_{max}$, dimensione della finestra nel momento in cui avviene una congestione
			- successivamente a una congestione viene ogni volta dimezzata la velocità di trasmissione  e viene settata una variabile $K$ nei pressi di $W_{max}$
			- prima di $K$ si cresce velocemente in un valore compreso tra $K$ e $W_{max}$ meno velocemente
			- ogni volta viene causata la congestione
	- TCP Vegas
		- evoluzione di CUBIC
		- calcola una stima e vede ogni volta se viene rispettata effettivamente
	- ECN
		- presente in alcune implementazioni di TCP
		- vengono usate due variabili
			- ECN
				- il router le invia per segnalare congestioni
					- 10 non c'è
					- 11 c'è
			- ECE
				- le invia il destinatario al mittente
				- 1 se c'è
				- 0 se non c'è
![[Pasted image 20250411183520.png|500]]
- **fairness di TCP e UDP**
	- TCP è fair perché il troughput è dato da $R/K$
		- ovvero il numero la capacità del collegamento fratto il numero delle connessioni
	- TCP paralleli
		- se dallo stesso host faccio più socket con più richieste TCP non diventa più fair
	- UDP non è fair perché non può controllare il tasso di trasmissione 
- **Evoluzioni protocolli di trasporto**
	- QUIC
		- usa UDP e al livello di applicazione implementa le varie sicurezze e migliorie
		- tipo TCP ha HOL(Head Of Line blocking) QUIC no
		- essendo più recente è meno supportato
#### LIVELLO DI RETE

### LIVELLO DI RETE
- **Introduzione***
	- il livello di rete si occupa di trasportare datagrammi da un host mittente a un host destinatario che possono trovarsi anche su reti differenti
- **Descrizione protocollo IP***
	- protocollo fondamentale del livello di rete, si occupa del vero e proprio trasferimento dei datagrammi attraverso una rete di dispositivi
	- È **BEST EFFORT**, non da garanzie dei servizi che offre ma fa del suo meglio
		- servizi che vuole offrire la rete:
			- servizi per il **singolo datagramma**
				- consegna garantita
				- consegna con ritardo ridotto
			- servizi per **datagrammi multipli**(flussi)
				- consegna in ordine
				- banda di trasferimento minima garantita
				- frammenti che arrivano a intervalli regolari
	- **DATAGRAMMA IP**
		- intestazione con indirizzi IP sorgente e destinazione, lunghezza totale del datagramma versione e TTL, protocollo usato al livello superiore, checksum
		- corpo dati
![[Pasted image 20250418131749.png]]
- **FRAMMENTAZIONE DATAGRAMMI**
	- se un datagramma supera la MTU(Maximum Transmission Unit)
	- viene frammentato con stesso identificatore 
		- flag che indica se è l'ultimo del suo blocco, 
		- offset per indicare dove si inserisce nel datagramma totale
	- seguendo questi campi viene riassemblato nel destinatario finale
	- **PMTUD** (Path Maximum Transmission Unit Discovery)
		- obiettivo: scoprire quanto deve essere grande al massimo la MTU in 2 modi
			- 1. ICMP invia un datagramma con obbligo di non frammentazione, se riceve una segnalazione dal router che da un obbligo di frammentazione allora bisogna modificare la MTU con quella suggerita da parte del router
			- 2. Mitigazione durante l'handshake, insomma viene accordato prima
- **funzioni chiave del livello di rete**
	- **inoltro**
		- si occupa dell'effettivo invio dei datagrammi
		- si divide in:
			- basato sulla <font color="#f79646">destinazione</font>
				- usa indirizzo IP e la tabella di inoltro 
			- <font color="#f79646">generalizzato</font>
				- guarda altri campi come il protocollo e il servizio
				- usato su reti più complesse
				- tipo Match+Action
	- **instradamento**
		- processo che calcola i percorsi nella rete serve per effettuare un inoltro dei datagrammi coerente con l'infrastruttura di rete

- **classful addressing**
	- utilizzo di classi prima dell'invenzione di CIDR per definire indirizzi IP
- **come trovare Ip nell'inoltro basato sulla destinazione**
	- i router hanno un sacco di IP sulla tabella di inoltro
		- come capire l'IP di input a quale appartiene?
			- **CIDR** standard di formattazione che divide IP in 2 parti indirizzo subnet e indirizzo host
				- funziona tipo indirizzo/16, indica che i primi 16 bit sono della subnet e i successivi 32-16 sono dell'host
			- potremmo avere più IP simili in termini di bit, viene effettuata una ricerca della corrispondenza sulla tabella fino ai bit meno significativi, l'indirizzo con più informazioni viene selezionato
	- **TCAM+ priority encoder**
		- usata per *rappresentare* le *tabelle di inoltro*
		- TCAM è una memoria speciale che permette di trovare la riga con l'IP adeguato in un tempo ridotto
		- quando ci sono più indirizzi IP simili, entra in gioco il *priority encoder* che sceglierà quello con la priorità più alta
![[Pasted image 20250418125759.png]]

- **divisione in 2 del livello di rete**
	- *piano dei dati*
		- funzione locale dei router che decide come inoltrare un datagramma
	- *piano di controllo*
		- si occupa della logica globale della rete
![[Pasted image 20250417214312.png]]
- **SDN(Software-Defined Networking)***
	- architettura dove il *piano di controllo è centralizzato* in un unico *server* per tutta la rete 
		- router esecutori il controller calcola lui le *tabelle di inoltro*
	- posizionamento di SDN
		- abbiamo il *piano dei dati* con i vari router e le AS
		- poi a un livello *intermedio* abbiamo le SDN con il controller
		- ancora sopra abbiamo *il piano di controllo* con le varie *applicazioni* di gestione della rete
![[Pasted image 20250503150640.png]]
- come è fatto il controller delle SDN
	- è diviso in
		- *Livello di interfaccia* con le applicazioni
			- Livello che si collega alle app del piano di controllo, attraverso varie **API north-bound** fornisce a loro dell informazioni 
		- *Gestione dello stato di rete*
			- **Database** che contiene le varie info sulla rete, router, link, host e switch
		- *Comunicazione con i dispositivi che controlla*
			- Attraverso protocolli come **Open Flow** comunica con i vari dispositivi della rete come switch ecc...
			- questo **insieme di protocolli** è detto **Southbound API**
![[Pasted image 20250503150921.png|400]]

![[Pasted image 20250417214551.png]]



- **Router***
	- dispositivi di rete che hanno il compito di instradare datagrammi
	- se non c'è la SDN si divide in 
		- **piano di controllo**
			- via software
		- **piano dati**
			- hardware
		- **struttura di commutazione**
			- componente del router che permette di instradare i datagrammi da una porta di ingresso a una di uscita
		- **porte di ingresso**
			- interfacce destinate all'ingresso dei datagrammi ai router
			- ogni porta deve ricevere e processare un datagramma in modo veloce
			- è divisa in step
				- <font color="#00b050">terminazione di linea</font>
					- riceve i bit grezzi e li passa al successivo step
				- <font color="#00b050">elaborazione al livello di collegamento</font>
					- interpreta il frame e decapsula il datagramma
				- <font color="#00b050">ricerca e inoltro</font>
					- guarda il datagramma e capisce a quale struttura di commutazione inoltrarlo
		- **porte di uscita**
			- prende input da un commutatore e poi esegue gli step inversi delle porte di ingresso
		- **accodamento in entrata e in uscita**
			- in entrata potrei avere problemi di HOL 
			- in uscita potrei avere problemi di buffer troppo pieno e quindi scarti
![[Pasted image 20250417215033.png]]

- **Commutazione***
- componente del router che permette di instradare i datagrammi da una porta di ingresso a una di uscita
	- <font color="#00b0f0">centralizzata</font>
		- tutto passa per una cpu unica del router
	- <font color="#00b0f0">decentralizzata</font>
		- ogni porta del router ha una sua piccola cpu che elabora a quale porta di uscita mandare il pacchetto
	- **3 strutture** 
		- 1 <font color="#9bbb59">memoria</font>
			- tutte le porte hanno una memoria condivisa
			- i datagrammi vengono copiati dentro essa e le porte di uscita copiano il tutto
			- lento
		- 2 <font color="#9bbb59">bus</font>
			- bus tra le porte di entrata e uscita
				- problemi di congestione del bus
		- 3 <font color="#9bbb59">interconnessione</font>
			- parallelismo
			- si divide in
				- <font color="#c00000">crossbar</font>
					- matrice di bus
				- <font color="#c00000">multistage</font>
					- piccoli switch tra le due porte che indirizzano il tutto
![[Pasted image 20250706171108.png]]


- **Gestione del buffer***
	- troppo buffering causa aumenti di RTT facendo allocare troppi pacchetti nella rete
	- **3 politiche di scarto**
		- *tail drop*
			- viene scartato l'ultimo che arriva
		- *priorità*
			- i pacchetti hanno una priorità
		- *marcatura*
			- prima di scartare invia dei segnali come ECN per avvisare che il buffer è pieno
	- **3 algoritmi di scheduling** per decidere quali mandare prima
		- *FCFS first come first served*
			- il primo che arriva è il primo ad uscire
		- *con priorità*
			- ogni pacchetto viene classificato con una sua priorità e viene definito in quale ordine inviarli
			- **starvation**: una delle code potrebbe non essere mai selezionata
		- *RR Round Robin*
			- sempre diviso in classi ma si invia un po di tutto
		- *WFQ Weighted Fair Queuing*
			- ogni priorità ha un suo spazio di banda per mantenere le cose fair

![[Pasted image 20250418131504.png]]

#### Indirizzi IP e gestioni varie
- **Sottorete**
	- definizione
		- insieme di dispositivi che possono comunicare tra loro senza dover passare per un router ma uno switch si
- **DHCP(Dynamic Host Configuration Protocol)**
	- definizione 
		- è una alternativa al sistema manuale dove bisognava scrivere gli indirizzi IP in fase di inizializzazione della macchina
		- in DHCP è presente un server che assegna ai nuovi host in ingresso un IP dinamico che può variare nel tempo
			- questo server si trova di solito interno ai router
	- 4 step del DHCP
		- 1. *Discover*
			- l'host che entra nel server manda un broadcast per trovare se ci sono DHCP disponibili
		- 2. *Offer*
			- il DHCP offre un indirizzo IP all'host 
		- 3. *Request*
			- l'host conferma l'IP offerto al DHCP
		- 4. *Ack*
			- il DHCP invia un Ack di assegnazione dell'IP
	- non serve solo per IP
		- suggerisce quale Server DNS usare
		- Router First-Hop da usare
			- ovvero router gateway, colui che si collega ad altre reti non interne facendo da tramite
![[Pasted image 20250418153930.png]]

- **Come si ottengono IP pubblici/privati da condividere con la tua rete**
	- ISP ha un grande blocco di indirizzi che assegnerà a sua volta ad ogni rete che ne richiede
		- un ISP ha magari `indirizzoIP/x` 
			- questo significa che ho i primi x bit fissi e gli altri posso usarli per definire IP di rete da condividere con i richiedenti
			- se x=20 posso dare $2^{32-20}$ indirizzi IP
	- *Route aggregation*
		- è una tecnica di aggregazione di indirizzi IP per alleggerire la tabella di instradamento condivisa tra i vari ISP/grandi router
		- ognuno scrive sulla tabella solo il blocco di indirizzi senza precisarli tutti
		- se un indirizzo IP specifico passa a un'altra rete quella determinata rete deve fornire più dettagli di quell'indirizzo IP
			- ricordiamo che viene data la precedenza alle corrispondenze migliori
- **ICANN**
	- organizzazione centrale che gestisce gli indirizzi IP al livello mondiale
		- fornisce questi indirizzi IP a 5 grandi fornitori RR
			- questi 5 RR forniscono poi i vari blocchi di indirizzi agli ISP
- **NAT(Network Address Translation)**
	- definizione
		- gli indirizzi IPv4 sono limitati 
		- è una tecnica che riduce gli indirizzi IPv4
		- per ovviare a questo problema esistono ad esempio dei router NAT che consentono di utilizzare solo un indirizzo IP pubblico per tutta la rete che gestiscono
		- i dispositivi della rete avranno un indirizzo IP privato
		- il router NAT dovrà ogni volta cambiare le varie intestazioni dei datagrammi mettendo l'IP pubblico, i dispositivi esterni alla rete vedranno solo il router NAT come dispositivo nella rete e poi dovrà essere lui a condividere i datagrammi corretti nella rete interna al dispositivo corretto
		- per ricordarsi a chi deve condividere quel datagramma utilizza una tabella NAT con salvate le varie occorrenze
![[Pasted image 20250421191015.jpg]]

- **IPv6**
	- descrizione
		- Nasce per aumentare i possibili IP
		- è a 128 bit non a 32
	- tunneling
		- non è retrocompatibile ma ci sono router misti che usano entrambi gli IP
			- lavorano su reti miste con router Dual Stack
			- ho un datagramma IPv6 che deve passare in una rete IPv4, per farlo incapsulo IPv6 in IPv4 e poi de capsulo il tutto
	- cosa avviene nella frammentazione
		- frammentazione non presente, scopro la MTU del datagramma IPv6 con PMTUD 
![[Pasted image 20250421193837.jpg]]

- **Tabella dei flussi o di inoltro**
	- per capire dove inoltrare i vari datagrammi esiste questa tabella
	- per gli inoltri **di tipo generalizzato** avevamo detto che non era sufficiente un indirizzo IP e basta
		- vengono usati dei dati interni al datagramma ricercati con la funzione Match
		- che poi forniscono le informazioni per una determinata Action che deve fare il router
			- inoltro, scarto, modifica e se siamo in un SDN può essere inviato al controller
		- da qui nasce Match+ Action che è la vera e propria tabella
		- se due Match hanno due action diverse viene data una priorità alle Action  vince quella con priorità maggiore
![[Pasted image 20250421201640.jpg]]

- **Open flow**
	- concetto
		- rappresenta uno standard che caratterizza la struttura delle reti a SDN, dove il piano di controllo è demandato a un controller
		- OpenFlow ha una tabella che contiene
			- Match, è diviso in livelli perché l'informazione potrebbe stare su quello di collegamento, di rete, di trasporto
			- Action azioni che si possono fare come blocchi
			- Priorità, per Match con più Action
			- Contatore dei byte o dei pacchetti, che tiene conto di quelli che hanno usato una certa regola
	- protocollo
		- protocollo utilizzato dai dispositivi OpenFlow come router ecc... che permette di comunicare con il server controller della SDN
![[Pasted image 20250503151241.png]]

- **Load Balancing**
	- caratteristica dell'inoltro generalizzato
	- consente di spalmare il carico su più porte per instradare più pacchetti che vanno a uno stesso indirizzo IP
- **MiddleBox**
	- dispositivi che forniscono servizi all'interno della rete e che non sono router
	- come i firewall o i NAT o i DHCP
### Algoritmi di instradamento
- **definizione**
	- Algoritmi che si occupano di riempire la tabella di instradamento, cercando un percorso migliore con la distanza minore possibile tra i vari dispositivi nella rete
- **tipologie**
	- *Globale*
		- ha una visione ampia della rete
	- *Non globale*
		- non ha bisogno di avere una visione ampia
	- *Centralizzato* 
		- calcolo dei percorsi centralizzato
		- conoscenza globale della rete
	- *Decentralizzati* (link-state)
		- ogni dispositivo deve calcolare i percorsi
		- inizialmente il router conosce solo i costi dei dispositivi adiacenti
- inoltre anche
	- *statici*
		- cambiano raramente
		- richiedono aggiornamenti manuali
	- *dinamici*
		- si aggiornano automaticamente al variare dei costi dei vari collegamenti tra nodi
- **Dijkstra**
	- algoritmo Globale *link-state* che consente di trovare il percorso migliore ha un funzionamento iterativo
- **Vector Distance**
	- È di tipo decentralizzato
	- Si basa sull’equazione di Bellman-Ford e funziona così: ogni router sa quanto costa raggiungere le reti vicine, e scambia informazioni con i router vicini per scoprire nuovi percorsi. Nel tempo, ogni router costruisce una tabella che indica: la distanza verso ogni rete e da quale router passare per raggiungerla nel modo più economico.
	- cambio dei costi
	- problema di conteggio infinito
		- inversione avvelenata
#### AS (Autonomous System)
- definizione
	- insieme di router scalabili interconnessi tra loro che si trovano nella stessa ISP o amministrazione di rete
	- strategia per gestire in modo scalabile l'instradamento
- differenza tra
	- *intra-AS*
		- tutti i router che si trovano nella stessa AS e condividono gli stessi protocolli 
	- *inter-AS*
		- insieme dove deve essere effettuato un routing tra AS differenti, attraverso dei router gateway che appunto li collegano tra di loro

![[Pasted image 20250503124817.png]]
- protocolli usati nell'*intra-AS*
	- RIP
	- EIGRP
	- *OSPF*
		- definizione
			- di tipo *Link-State*, i router si scambiano tra loro le varie informazioni di instradamento in broadcast(flooding) e aggiornano così la mappa di instradamento
			- il messaggio usa protocollo TCP e algoritmi di Dijkstra per effettuare i calcoli
		- è divisa in 2 livelli ma riguarda comunque tutta la intra-AS
			- *Area Locale*
				- sottoinsieme della rete senza router gateway
			- *Backbone*
				- Dorsale che collega tutti i dispositivi della stessa area intra-AS
		- estensioni associate
			- per reti senza SDN viene usato *OSPF*, permettendo di scambiare informazioni utili per effettuare instradamenti corretti senza uso di SDN
			- MPLS-TE protocollo che consente di evitare congestione

![[Pasted image 20250503131511.png]]
#### BGP protocollo usato nella inter-AS
- definizione
	- permette di far comunicare tra loro i vari router gateway si divide in due modalità
- *i-BGP*
	- modalità che consente di inviare informazioni alla intra-AS riguardo le cose che vengono inviate dalla inter-AS
- *e-BGP*
	- modalità che consente lo scambio di informazioni tra AS esterne
	- funziona attraverso annunci
- *sessione BGP*
	- è una *connessione TCP* semi permanente tra i router gateway detti <font color="#4bacc6">peers</font>
- *messaggi BGP*
	- servono per stabilire e mantenere la connessione TCP tra peer
		- <font color="#f79646">keepalive</font>
			- serve per mantenere la connessione attiva
		- <font color="#f79646">open</font>
			- avvia connessione tra due peer
		- <font color="#f79646">update</font>
			- annuncia nuove rotte o ritira vecchie rotte
		- <font color="#f79646">notification</font>
			- segnalazione di errori
- concetto di <font color="#00b0f0">rotta BGP</font>
	- insieme di informazioni inviate tra AS che indicano il percorso da seguire
		- *prefisso*
			- indica la rete di destinazione con il vero e proprio indirizzo
		- *attributi*
			- informazioni sul percorso per evitare cicli oppure trovare facilmente il primo router di salto
		- *AS-PATH*
			- indica il vero e proprio percorso, la successione di AS
		- *Next-Hop*
			- rappresenta il router gateway 
- Esempio con o senza percorsi multipli
	- solo i router gateway possono modificare router di next hop per indicare "se volete inviare ad altre AS passate per me"
	- un router che lavora in inter-AS annuncia anche l'<font color="#00b0f0">AS-PATH</font> ovvero il percorso che deve seguire per raggiungere quella determinata destinazione
	- su percorsi multipli è simile solo che vengono seguite delle policy
- *Criteri* usati da router BGP *per riempire tabella di instradamento*
	- 1.**Next Hop modificato**
		- i router gateway modificano il Next-Hop su loro stessi così i dispositivi nella intra-AS devono solo raggiungerlo seguendo un percorso nella inter-AS mediante OSPF
	- 2.**Next Hop non modificato**
		- il router gateway non modifica il Next-Hop e lascia quello da lui raggiungibile di un'altra AS, i dispositivi interni devono capire che devono passare per il router gateway
	- 3.**Instradamento a patata bollente**
		- se ci sono più percorsi simili prende quello meno costoso mandando il pacchetto nella inter-AS meno costosa per far passare il traffico il più velocemente possibile
	- 4.**Forzare percorsi tramite annunci**
		- annuncio=azione di inviare un messaggio update tramite BGP
		- per non intasare il traffico della sessione BGP vengono inviati solo gli annunci più utili
		- se ad esempio so che un AS può raggiungerne un altro senza passare per un determinato AS, esso sceglie di non annunciare il proprio percorso
#### IP ANYCAST
- definizione
	- più server con stesso indirizzo IP pubblico, il client avrà scambi con quello più vicino
	- offrono stessi contenuti o servizi
![[Pasted image 20250503143925.png]]
#### Ingegneria del traffico
- definizione
	- insieme di tecniche che consentono di modulare e ottimizzare il traffico della rete
#### Concetto di IBN(Intent-Based-Networking)
- definizione
	- sistema dichiarativo che funziona attraverso intenti per modificare la struttura della rete in modo automatizzato
	- es: voglio ridurre la latenza tra due router, spiego l'intento e essi verranno configurati in tal maniera
	- colui che effettua queste modifiche è il controller SDN
#### ODL e ONOS
- definizioni
	- due tipi di controller 
	- *ODL*
		- usa API per comunicare con applicazioni
	- *ONOS*
		- controller che usa nel pratico il concetto IBN con gli intenti
#### ICMP(Internet Control Message Protocol)
- cosa è
	- protocollo incapsulato nel protocollo IP consente di scambiare messaggi utili per la gestione tra host e router
- messaggio ICMP
	- composto da 
		- tipo
		- codice
		- checksum
		- altri dati
- tipi di messaggio
	- 1.*Echo Request(0) o Reply*
		- permettono di capire se un host è raggiungibile e con quale distanza
	- 2.*Destination Unreachable(3)*
		- utilizzato per segnalare Host non raggiungibili
	- 3.*Source Quench*
		- permetteva di segnalare congestioni ora deprecato
	- 4.*TTL expired(8)*
		- serve per quando imposti un determinato limite di hop utilizzando un contatore TTL che decrementa ad ogni hop
		- se arriva a 0 invia questo segnale
![[Pasted image 20250505192401.png]]

- **Traceroute**
	- strumento di diagnostica per capire quanti hop deve effettuare un pacchetto sonda per raggiungere un determinato punto di destinazione
	- di volta in volta si incrementano i TTL
![[Pasted image 20250505192939.png]]

- **nuova versione ICMPv6**
	- adattato ai nuovi router che non fanno troppa frammentazione
#### Gestione delle reti
- descrizione e componenti
	- per **gestire una rete adeguatamente** si ha bisogno di
		- *server di gestione*
			- server che raccoglie dati e invia comandi per configurare i dispositivi della rete
		- *dispositivi di rete da gestire*
			- router switch ecc...
		- *dati*
			- dati utilizzati per gestire la rete come statistiche varie
		- *agente di gestione*
			- Software di gestione della rete 
		- *protocollo di gestione di rete*
			- protocolli utilizzati per comunicare ai dispositivi i vari cambiamenti
- metodi per gestire una rete
	- *CLI*
		- linea di comando manuale
		- metodo diretto ma non scalabile anche se prevede uso di eventuali script automatizzati
	- *SNMP/MIB*
		- interfaccia server che usa come protocollo di comunicazione per i dispositivi SNMP 
		- i dati raccolti sono organizzati in MIB
		- non propriamente automatizzato
	- *NETCONF/YANG*
		- YANG è un linguaggio astratto che consente di configurare delle reti
		- la configurazione e la modifica di questi YANG per poi cambiare i dispositivi remoti sono mediante un protocollo NETCONF
		- consente commit atomici
		- ideale per reti complesse, dinamiche e centralizzate
#### LIVELLO DI COLLEGAMENTO
### LIVELLO DI COLLEGAMENTO
- **introduzione**
	- il livello di collegamento si occupa di trasferire i datagrammi da un nodo a quello fisicamente adiacente lungo il percorso
		- ha una visione più dettagliata su dispositivi come switch
	- il livello di collegamento si serve di frame, con al loro interno i datagrammi incapsulati
- **servizi del livello di collegamento**
	- *Framing*
		- processo di incapsulamento dei datagrammi che provengono dal livello di rete aggiungendo intestazione e trailer che servono a delimitare la singola unità
	- *Accesso al collegamento*
		- effettuare un accesso al mezzo di trasmissione condiviso tra dispositivi si usano protocolli MAC(Medium Access Control)
		- per identificare i dispositivi che condividono questo stesso mezzo di trasmissione si usano gli indirizzi MAC che identificano univocamente la scheda di rete del dispositivo, è statico a differenza degli IP che lavorano sul livello di rete
	- *Consegna affidabile tra nodi adiacenti*
		- servizi che rilevano errori, usati soprattutto in reti wireless dove ci sono errori più frequenti
	- *Controllo del flusso*
		- Regola la velocità di trasmissione del singolo collegamento
	- *Rilevazione degli errori e correzione*
		- Ogni protocollo di collegamento ha controllo sui vari errori e possono essere risolti con o senza ritrasmissioni
			- **ARQ**(Automatic Repeat <font color="#00b050">reQuest</font>) con ritrasmissioni
			- **FEC**(Forward Error Correction) senza ritrasmissioni
- tipi di trasmissione
	- **Half duplex**
		- La trasmissione non può essere simultanea da entrambe le direzioni
			- Wifi
	- **Full duplex**
		- La trasmissione è simultanea per entrambe le direzioni
			- Ethernet
- **Livello di collegamento negli host**
	- come componenti del livello di collegamento gli host hanno la scheda di rete detta
		- NIC(Network Interface Card) che fa da intermediario sia del livello fisico che quello di collegamento
	- **Come è fatto un host**
		- *mittente*
			- il mittente sfrutta il controller nella scheda di rete per 
				- incapsulare il datagramma dentro un frame
				- aggiungere vari bit di controllo
				- gestire flusso trasferimento affidabile ecc...
			- la CPU dell'host consente di costruire i dati e interagisce con la NIC(Network Interface Card) per assemblare il pacchetto
		- *destinatario*
			- il controller della scheda di rete
				- verifica eventuali errori nei bit ricevuti
				- gestisce anche lui trasferimento affidabile e flusso
				- estrae il datagramma dal frame
			- la CPU in questo caso prende i dati e li passa ai livelli superiori rete trasporto ecc...
![[Pasted image 20250508223125.png]]

#### Rilevazione degli errori
- introduzione alla rilevazione degli errori
	- per rilevare errori si usano tecniche come l'utilizzo di un codice EDC(Error Detection and Correction)
		- quando vengono inviati dei dati $D$ viene aggiunto questo codice $EDC$ 
		- questo codice EDC viene generato a partire da una funzione applicata sui dati $D$
		- una volta generato viene inviato al destinatario
		- il destinatario adesso riceve questi dati $D$ ci riapplica la funzione e vede se corrisponde a EDC precedente 
		- non é super affidabile e in più c'è overhead 
![[Pasted image 20250508224352.png]]

- 3 tecniche utilizzate per fare controllo sugli errori migliori di EDC
	- *Bit di parità*
		- Obbiettivo
			- vengono presi i dati in bit e vengono aggiunti eventuali bit per rendere il numero di 1 totali pari
			- dopo aver inviato il tutto se il numero di bit a 1 compreso quello di parità sono dispari, errore
			- unico problema se ho errori su un numero di bit pari ritornerei comunque a una sequenza pari quindi non rileverei errori
			- vengono spesso usate matrici di bit per verificarli
			- parità bidimensionale
				- creare una matrice per calcolare parità su righe e colonne
				- comprende anche un bit globale
		- *Checksum*
			- Obbiettivo
				- Il checksum è un meccanismo di controllo dell'integrità dei dati che viene usato principalmente a livelli superiori come quello di trasporto con UDP TCP ecc... oppure anche sul livello di rete come IP
					- il mittente prende il contenuto del pacchetto come una sequenza di interi, la somma facendo il complemento a 1
						- ovvero la somma con i suoi bit normali e la sua controparte in complemento a 1
					- il risultato viene a sua volta complementato a 1 e lo inserisce nel campo checksum
				- il ricevente somma tutto compreso checksum 
					- controlla se il risultato sono tutti 1 per vedere se non ci sono errori
		- *CRC*
			- Sistema estremamente affidabile per rilevare errori 
			- il mittente tratta i dati come una lunga sequenza di bit e li divide per un polinomio binario predefinito
				- il resto della divisione CRC viene allegato al frame
			- il destinatario svolge la stessa divisione e verifica il resto 
				- se è 0 i dati sono probabilmente corretti altrimenti c'è stato un errore nella trasmissione
#### Collegamenti e accesso multiplo
- **Punto a Punto**
	- collegamento di tipo punto a punto
	- composta da un trasmittente e un ricevente
- **Broadcast**
	- canale di collegamento che comprende più nodi che trasmettono e piu nodi che ricevono
	- presentano problemi di accesso multiplo da risolvere
#### Gestione accesso multiplo
- Iniziamo con la spiegazione di un protocollo *ideale* *MAC*
	- Multiple Access Channel
	- in modo ideale è previsto che se in un collegamento ho più nodi ho trasmissione pari a R/M
	- se invece ho solo un dispositivo avrò velocità R totale
	- inattuabile
#### Tipi di protocolli ad accesso multiplo reali
- si dividono in
	- *Channel Partitioning*
		- con canale suddiviso
		- ogni nodo ha una sua fetta del canale
		- le fette rimanenti sono inutilizzate
	- *Random Access*
		- il canale presenta collisioni e per risolverle vengono fatte ritrasmissioni e operazioni di recover
	- *Taking Turns*
		- i nodi usano il canale a turno
		- i nodi con maggiore priorità potrebbero avere il turno più duraturo
			- tipo i nodi con più materiale da inviare
- Quelli a *Channel Partitioning*
	- **TDMA**
		- il canale viene suddiviso per istanti temporali fissi
			- detti time slot
			- ogni nodo ha il suo timeslot
			- in quel timeslot ha accesso completo
			- gli slot inutilizzati si dicono idle
![[Pasted image 20250521112454.png]]
- **FDMA**
	- il canale viene suddiviso in spettri di frequenze diverse interna un cavo FDM
	- ogni nodo trasmette sulla sua frequenza non alla massima velocità
![[Pasted image 20250521112857.png]]

- Quelli ad *Accesso casuale*
	- **SLOTTED ALOHA**
		- l'uso del collegamento è diviso in slot temporali
		- ogni nodo che vuole inviare qualcosa accede attende il prossimo slot temporale libero e vi accede
			- se viene occupato prima da qualche altro nodo avviene una collisione e deve attendere il time slot successivo
		- ogni nodo decide in autonomia quando trasmettere
		- possono esserci collisioni frequenti o inutilizzi di slot temporali
		- i nodi devono essere sincronizzati
		- un nodo può utilizzare il canale in modo efficace con una probabilità del 37% del tempo
![[Pasted image 20250521114843.png]]
- **UNSLOTTED ALOHA**
	- senza sincronizzazione tra nodi 
		- trasmettono finché non avviene una collisione 
		- i nodi non aspettano il time slot successivo
	- diminuisce probabilità di efficienza arrivando al 18%
- **CSMA**
	- il nodo prima di trasmettere ascolta il canale e vede se è libero o occupato
	- possono comunque esserci collisioni dovute a ritardi di propagazione
- **CSMA/CD**
	- miglioria di CSMA con una detection delle collisioni
	- il nodo che trasmette rimane in ascolto di eventuali collisioni
	- se avviene smette di trasmettere così non viene sprecata banda per un frame che andrebbe perso
		- non funziona bene via wireless
	- funzionamento
		- un nodo sta trasmettendo nel collegamento, allo stesso tempo si mette in ascolto per vedere se ci sono collisioni in atto
		- se un nodo prova a collegarsi il nodo che trasferiva i dati lo rileva
		- si interrompe la trasmissione dei nodi coinvoli nella collisione
		- viene segnalata
		- e poi viene assegnato un tempo casuale di accesso ad ogni nodo coinvolto e si riprende così il tutto
![[Pasted image 20250521120825.png]]

- Quelli a *Taking Turns*
	- **POLLING**
		- è presente un controllore centralizzato che dice ai nodi quanti frame possono trasmettere al massimo per un dato turno
		- il fatto che ci sia un controllore aumenta il ritardo ma allo stesso tempo si riducono collisioni o slot inutilizzati
		- usato nel Bluetooth
![[Pasted image 20250521122639.png]]
- **Token Passing**
	- Token che viene passato per ogni nodo, chi lo ha può usare il collegamento
![[Pasted image 20250521122744.png]]

- Gestione via cavo di 
	- *downstream*
		- vengono usati canali FDM in broadcast
	- *upstream*
		- viene usato il sistema ad accesso casuale
	- per mettere d'accordo i vari modem via cavo viene usato uno standard DOCSIS che precisa quali tipologie di politiche di accesso devono essere usate
#### LAN
- Definizione
	- **Local Area Network**
	- indica una area ristretta come una casa o una scuola
- spesso si usano Ethernet o Wifi
#### Indirizzi MAC
- descrizione
	- Per identificare un dispositivo di rete ad esempio una scheda di rete per effettuare uno scambio dei frame abbiamo bisogno di un indirizzo MAC, è a 48 bit ed è memorizzato nella ROM della NIC Network Interface Card
- **come vengono scelti IEE**
	- ente internazionale che ha lo scopo di gestire e fornire indirizzi MAC ai vari produttori di NIC
![[Pasted image 20250521180754.png]]
- **Da IP a MAC**
	- Viene utilizzato un protocollo ARP che ha una tabella ARP dove sono presenti 
		- Ogni nodo IP nella LAN con le sue interfacce e il suo Indirizzo MAC con anche un TTL per la validità dell'informazione
- **Protocollo ARP**
	- Come funziona Se la tabella non presenta il MAC di un dato IP
		- se un nodo nella rete vuole avere il MAC di un dispositivo usa il protocollo ARP che invierà un broadcast di richiesta con quel determinato indirizzo IP
		- il dispositivo corretto risponde
		- ora potrà essere popolata la tabella ARP
	- **Attacco ARP SPOOFING o POISONING**
		- viene inviata una risposta ARP falsa fingendosi di avere un'altro indirizzo IP
		- fai confluire il traffico verso di te puoi intercettarlo oppure puoi fare un attacco Dos associando 1000 indirizzi IP allo stesso MAC
- **Come inviare un datagramma a un nodo non adiacente nella rete**
	- Se il destinatario si trova su un'altra sottorete allora bisogna instradare il frame a un router gateway
	- viene creato un frame con all'interno il datagramma IP con le varie informazioni
	- il router riceve il frame e lo decapsula, vede il datagramma che l'IP è da inoltrare a un altro dispositivo 
	- re incapsula il tutto e lo invia alla interfaccia dello switch corretta con il giusto destinatario
#### ETHERNET
- cosa è 
	- Standard di comunicazione utilizzato per le reti LAN cablate
- **frame ethernet**
	- composto da
		- *preambolo*
			- sincronizza il ricevente e segnala quando un frame inizia
		- *Mac di destinazione*
		- *MAC di sorgente*
		- *Tipo di protocollo incapsulato* nel payload per poi de capsularlo e vedere cosa c'è
		- *Dati*
		- Codici di controllo errori *CRC*
	- Tutti gli standard di Ethernet usano stesso frame 
![[Pasted image 20250522155625.png]]
- **sicurezza di ethernet**
	- è senza handshake 
	- vengono gestiti accessi multipli come ad esempio con CSMA/CD
	- le altre sicurezze varie vengono gestite ai livelli superiori
- *Concetto di dominio di collisione*
	- punto in cui si condivide stesso mezzo di trasmissione
	- si può verificare una collisione tra vari frame ethernet se si trasmette insieme
	- si consiglia di ridurre i dispositivi collegati a un singolo collegamento
#### Switch Ethernet
- Cosa sono
	- Lo switch è un dispositivo che lavora sul livello di collegamento
	- ha il compito di memorizzare e inoltrare i frame Ethernet
- Caratteristiche
	- è *plug and play* non devi configurarlo
- **Tabella di commutazione degli Switch**
	- Ogni switch ha una sua tabella di commutazione con un 
		- *indirizzo MAC del nodo*
		- *interfaccia che conduce al nodo*
		- *TTL*
	- lo switch auto riempie le varie tabelle
		- ogni volta che riceve un frame aggiunge alla tabella il mittente 
- *Cosa fa lo switch quando riceve un frame*
	- Aggiorna la Switch table mettendo il mittente
	- se il mittente ha stessa porta del destinatario allora non serve che ci sia questo passaggio per lo switch e scarta il pacchetto
	- se è su un'altra porta lo inoltra facendo lo switching
	- se non ha nella tabella il destinatario fa una operazione di flood per trovarlo
- **Differenze con i router**
	- gli switch lavorano sul livello di collegamento i router no
	- gli switch possono lavorare con pochi dispositivi perché usano una tabella normale
![[Pasted image 20250522173215.png]]

#### VLAN
- cosa sono
	- Se si ha bisogno di utilizzare il concetto e la comodità delle LAN su reti di grandi dimensioni senza però dover ricorrere a un solo Switch che non garantirebbe privacy e problemi di dimensioni della tabella
	- esistono le VLAN
		- si possono usare switch differenti per rimanere sulla stessa rete ma allo stesso tempo creare flessibilità di gestione
- **versione basata sulle porte**
	- un singolo switch viene usato come due switch differenti per mantenere la sicurezza
	- uno switch viene diviso a metà virtualmente
![[Pasted image 20250522175052.png]]

- **versione con più switch**
	- viene usata una porta trunk per collegare in serie più switch 
	- una volta collegato il tutto possono comunicare tra loro gli switch
- **EVPN**
	- tecnologia di tunneling che consente di creare una rete locale anche se si hanno due reti di livello 2 quindi con switch su luoghi differenti
		- viene collegato il router allo switch e viene incapsulato il frame ethernet che poi verrà passato dall'altra parte con un altro router e switch
- le VLAN hanno un loro ID per comunicare tra loro e riconoscersi
	- quest'ultimo é definito dallo standard 802.1Q
#### LE RETI WIRELESS
- **significato di wireless**
	- *Tecnologia* di collegamento senza l'uso di fili ma attraverso frequenze
- **significato di mobilità**
	- *proprietà* dell'infrastruttura di rete che consente al client di muoversi cambiando punti di accesso
- **Handover**
	- Processo che consente a un dispositivo mobile di cambiare collegamento wireless senza problemi
- Componenti che compongono una rete wireless
	- *Host wireless*
		- dispositivi che eseguono operazioni e hanno un collegamento wireless
		- si dividono in fissi o stazionari
	- *Collegamento wireless*
		- Utilizzato per collegare un host wireless alla stazione base oppure un altro host wireless
	- *Stazione base* 
		- elemento che funge da ripetitore
		- di solito connessa a una rete cablata
		- dispositivo di relay al livello di collegamento
- a una determinata velocità di banda varia il raggio di copertura
#### 2 Tipi di infrastrutture
- **con infrastruttura**
	- Sono presenti stazioni base che hanno il compito di offrire servizi di rete
	- avvengono operazioni di handoff, quando un dispositivo si sposta dall'area di copertura e cambia punto di accesso
![[Pasted image 20250528104430.png|400]]

- **senza infrastruttura**
	- reti senza stazione base con host che comunicano tra di loro
	- devono provvedere da se per fornire servizi di instradamento
![[Pasted image 20250528105453.png]]
#### Caratteristiche dei collegamenti wireless
##### Concetto di attenuazione
- il **segnale** può essere *assorbito* o *attenuato* a seconda della presenza di determinati ostacoli o anche solo dalla distanza
- l'attenuazione con spazio libero si calcola con 
	- $(frequenza⋅distanza)^2=(fd)^2$
	- Più **alta** è la frequenza o più **lontano** è il ricevitore, più **rapidamente** si perde il segnale.
![[Pasted image 20250528111841.png]]

##### Tempo di coerenza
- Tempo che ci indica se all'arrivo di un segnale ne possono arrivare *degli altri uguali* a causa di possibili *riflessioni* a distanza di un determinato tempo
	- questo tempo è **detto di coerenza**
##### interferenze da altre sorgenti
- Il **fenomeno fisico** di interferenza può anche verificarsi a causa di altri dispositivi che lavorano su frequenze simili
	- per definire il segnale e la frequenza su cui lavoriamo usiamo il **SNR(Signal-To-Noise-Ratio)**
		- rappresenta un rapporto tra il segnale e il rumore di fondo
		- un SNR alto consente di estrarre le informazioni facilmente
	- Il **BER**  **(Bit error rate)** rappresenta la probabilità che un bit sia ricevuto in errore
- **Bilanciamento di rete**
	- aumentare la potenza del segnale aumenta la SNR e riduce i BER
		- ma non è proprio facile da attuare dovuto a consumi eccessivi
		- i dispositivi wireless si adattano automaticamente modulando la frequenza e la velocità di trasmissione
		- così da avere maggiore stabilità
- **Terminali nascosti**
	- I terminali nascosti sono nodi che non possono vedere altri nodi perché sono fuori dalla loro portata ma possono comunque causare collisioni che li riguardano
		- ad esempio con un nodo intermedio che vede entrambi
- **Accesso multiplo**
	- *CDMA*
		- protocollo che permette di condividere stessa frequenza di comunicazione con più utenti
		- ogni utente ha un suo *codice unico* chiamato **chipping sequence** per identificarli
		- il loro segnale è codificato su questo
##### Standard Reti Wi-Fi 802.11
- rappresenta un **insieme di protocolli** che consentono la comunicazione wireless tra più dispositivi
- Architettura delle LAN 802.11
	- gli host wireless comunicano con una stazione base detta anche **Access Point**
	- le singole infrastrutture wireless sono dette *BSS* e hanno vari host punto di accesso ecc...
![[Pasted image 20250528123119.png]]

- **Divisione dei canali**
	- *tecnica* che consente la *modulazione di frequenze* per creare una divisione dei canali di comunicazione
	- ciò comunque non riduce a zero le interferenze
	- questi canali vengono scelti dal *AP admin*
![[Pasted image 20250528123601.png]]

- **ingresso di un dispositivo nella rete**
	- un host in arrivo su una BSS deve essere associato a un AP e per farlo si hanno due modalità
		- *scansione attiva*
			- il dispositivo che si collega deve mandare un **frame sonda** in **broadcast** per trovare l'AP corretto
		- *passiva*
			- gli AP a intervalli regolari inviano questi **frame beacon** per essere rilevati dai dispositivi che vogliono accedervi
				- al loro interno hanno un MAC e un identificativo dell'AP il SSID
	- dopo aver instaurato questo collegamento con accessi sicuri attraverso ad esempio WPA2
	- l'host può inviare un DHCP discover che sarà passato all'AP e poi al server DHCP
![[Pasted image 20250528124155.png]]

- **collisioni nelle reti wireless**
	- *CSMA/CA*
		- per gestire accesso multiplo nelle reti WiFi non si possono usare CD ovvero collision Detection perché con le reti wireless è complesso e inutilizzabile vengono usate variabili
		- **DIFS**
			- variabile che indica l'intervallo di tempo che bisogna aspettare per vedere se un canale è libero
			- se lo è il mittente trasmette
			- sennò aspetta un tempo backoff casuale
		- **SIFS**
			- variabile che indica un intervallo di tempo che deve aspettare il destinatario prima di inviare un ACK di ricevuta dei dati
	- *Meccanismo di prenotazione*
		- vengono usati segnali **RTS(Request to Send)**
			- per prenotare il canale di comunicazione
				- vengono inviati ai vari AP
			- possono avvenire collisioni di prenotazione
- quando un frame viene passato a un AP ha come destinazione l'indirizzo MAC dell'AP
	- quando un frame deve passare per un router viene incapsulato in un altro frame che avrà come mittente il MAC dell'AP e come destinatario il MAC del router
#### Tecnologie wireless
- **Bluetooth**
	- definizione
		- *Tecnologia wireless* che consente un collegamento di tipo *PAN(Personal Area Network)*
	- **piconet**
		- nome che prende una *singola rete Bluetooth* che consente fino a 8 dispositivi compreso 1 master controller
	- **bootstrapping**
		- *processo* di *accesso* a una *piconet* di un dispositivo client
		- si divide in 2 modalità possibili
			- **Neighbor discovery**
				- il master invia dei messaggi in broadcast detti inquiry 
				- il dispositivo in ascolto lo rileva e instaura così una connessione
			- **Paging**
				- il master invita un dispositivo specifico a entrare quando lo conosce
					- viene successivamente comunicato l'indirizzo di partecipazione e altre informazioni utili
![[Pasted image 20250529120105.png|300]]

- **Reti 4G/5G**
	- definizione
		- *Tecnologia funzionale* che consente il *collegamento* wireless su *WAN*
		- attraverso **Access Point**
	- similarità e differenze con internet cablato
		- Usano stessi protocolli e sono reti globali
		- tecnologie radio da parte delle reti 4G
		- supporto alla mobilità nativa da parte delle reti 4G/5G
	- **architettura 4G**
		- composta da 
			- *Mobile device(UE)User Equipment*
				- dispositivi mobili connessi alle base station 
				- ha un IMSI ovvero un suo identificativo 
			- *Base station(eNode-B)*
				- dispositivo che condivide le informazioni ai mobile Device
					- coordinandoli tra loro e gestendo le varie celle di collegamento
				- gestione di handover per mobilità dei device
			- *MME(Mobility Management Entity)*
				- Servizio che
				- conosce la posizione dei vari dispositivi 
				- fa da intermediario con i dispositivi e i P-GW
				- identifica i dispositivi usando l'HSS
			- *HSS(Home Subscriber Server)*
				- memorizza le informazioni degli utenti con le varie chiavi di autenticazione
				- Serve per identificare i dispositivi con ad esempio il loro piano dati
			- *S-GW*
				- router gateway interno alla rete che instrada i dati da parte delle UE verso i P-GW
			- *P-GW*
				- router gateway che porta a internet i dati che vengono dalle S-GW attraverso il tunneling 
				- router connesso alla vera e propria rete globale
	- **migliorie del 5G**
		- maggiore velocità
		- potrebbero esserci *problemi* di *distanza di banda*
![[Pasted image 20250529180732.png]]

- **Rete LTE**
	- definizione
		- *Standard di comunicazione* wireless con delle modifiche alle reti 4G soprattutto nella fase di tunneling dei dati è diviso in 2
	- **piano di controllo**
		- gestisce la *mobilità e la sicurezza*
			- non trasporta i dati effettivi
	- **piano di dati**
		- trasportare il vero e proprio *traffico dati*
	- **pila protocollare LTE**
		- ogni comunicazione LTE ha una sua pila protocollare che si differisce in 2 punti
			- 1. quando avviene lo *scambio dal UE al first hop* nella base station abbiamo un incapsulamento complesso che vuole garantire sicurezza e affidabilità nella gestione dei segnali radio
			- 2. una volta raggiunto invece il *passaggio di tunneling* dove i dati passano tra i vari Gateway attraverso un tunnel
				- la comunicazione avviene attraverso u n protocollo *GTP-U*
				- che impacchetta i dati in un pacchetto **UDP** per poi spedire i dati al P-GW passando per l'S-GW
![[Pasted image 20250529190918.png]]

- **problema della mobilità**
	- definizione
		- quando un dispositivo si muove bisogna *rinstaurare una connessione* a una base station con la copertura adatta e che magari è collegata a un router differente
	- **Home agent**
		- definizione
			- *Nodo nella rete* che rappresenta il riferimento per la ricezione dei dati del dispositivo UE
	- **approcci di routing**
		- 1.il router della base station differente *annuncia* agli altri che il *dispositivo ha effettuato questo cambiamento* e viene aggiornata la tabella di routing
			- con **troppi dispositivi non funziona**
		- 2.viene sfruttato il concetto di *Home agent*, 
		- si divide in 2 altri sottopunti
			- 1.**ROUTING INDIRETTO**
				- l'*home Agent* *invia* i dati che riceve per quel determinato UE *al nuovo router* della nuova base station
					- è **lento** e vengono fatti giri troppo lunghi
			- 2.**ROUTING DIRETTO**
				- i mittenti che vogliono mandare i messaggi all'UE non inviano più le informazioni all'Home agent ma *al nuovo router della base station*
					- **veloce ed efficiente** ma i mittenti devono capire il tutto

![[Pasted image 20250530164917.png]]

- **Le reti si dividono in**
	- *home network*
		- rete **gestita dall'operatore** con cui si ha un contratto
	- *visited network*
		- **rete gestita da altri operatori**
		- viene concessa attraverso il **roaming**
![[Pasted image 20250601113458.jpg]]

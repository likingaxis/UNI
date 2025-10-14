## Relazione tra livello di trasporto e rete
Un protocollo a livello di trasporto **mette a disposizione** una comunicazione logica tra processi che comunicano su host diversi.
Un protocollo a livello di rete fornisce comunicazione logica tra host.
###### ESEMPIO
- Il **protocollo di rete (IP)** si occupa di far arrivare il pacco **al suo indirizzo di casa**.
- Il **protocollo di trasporto (TCP/UDP)** si occupa di far arrivare il pacco **alla persona giusta nella casa**.

I protocolli di trasposto vengono eseguiti nei sistemi periferici
- LATO INVIO: scinde (se necessario in caso di messaggi troppo grandi) il messaggio dell'applicazione inserendo un'intestazione per identificare a quale messaggio ricondurre questo "pezzo"
- LATO RICEZIONE: riassembla il messaggio rimuovendo le intestazioni e lo invia all'applicazione

I router non si preoccupano dei segmenti, ma guardano solo l'intestazione del datagramma IP per capire dove deve andare il pacchetto (tipo i corrieri).

![[ms-teams_SIDRVEjMKW.png]]

### Due metodi per la comunicazione
#### UDP (User Datagram Protocol)
Un protocollo molto leggero, semplice e veloce pensato per mandare dati in fretta, senza concentrarsi troppo sulla perfezione.
È un protocollo però inaffidabile, in quanto senza connessione e con il rischio che i dati possano perdersi o arrivare fuori ordine.
Viene utilizzato spesso per
- streaming video/audio
- giochi online
- chiamate vocali (dove conta più la velocità che la perfezione)

#### TCP (Transmission Control Protocol)
Si basa su un "accordo" di connessione tra i due host comunicanti ed è quindi più affidabile.
TCP si occupa di
- assicurarsi che ogni pacchetto arrivi
- metterli nell'ordine giusto (anche se potrebbero comunque arrivare sfasati)
- ritrasmettere i pacchetti persi
- regolare la velocità di trasmissione per non intasare la rete
Viene usato prediligendo la perfezione alla velocità.

>[!tip] Entrambi hanno dei servizi non garantiti
>- non garantiscono che i dati arrivino in un tempo specifico (es. ogni due secondi)
>- non garantiscono che la connessione abbia una certa velocità minima (es. sempre 100 $\frac {Mb} s$) 


### Multiplexing e Demultiplexing
Quando si parla di livello di trasporto è importante soffermarsi su come vengano organizzati i dati in partenza e di come vengano smistati una volta arrivati.

##### Multiplexing (lato mittente)
Quando un host invia dati, può avere più applicazioni attive nello stesso momento (es. browser, videogioco, Spotify) e tutte queste applicazioni vogliono inviare dati attraverso la stessa comunicazione di rete.
Il livello di trasposto allora deve
- raccogliere i dati di ciascun processo (attraverso le socket)
- aggiungere un'intestazione per indicare la provenienza del dato
Questo è il multiplexing.
![[ms-teams_hVpBKBk0sN.png]]
##### Demultiplexing
All'arrivo dei dati, questi devono essere smistati ai giusti destinatari.
Il livello di trasporto ha ora un nuovo compito: deve leggere le intestazioni e capire a quale processo (socket) consegnarli.
![[ms-teams_j0jUvWaTsw.png]]
##### Funzionamento effettivo
Ogni pacchetto è un datagramma IP, che contiene dentro di sé un segmento del livello di trasporto (TCP o UDP) e in questo segmento ci sono due informazioni fondamentali
- indirizzo IP del mittente e destinatario
- numero di porta del mittente e destinatario
	- questo è molto utile perché identifica il processo che invia e riceve i dati

Quindi, una volta che il pacchetto arriva:
1) il livello di rete consegna il datagramma IP al livello di trasporto
2) il livello di trasporto estrae il segmento TCP/UDP e guarda l'intestazione (quindi indirizzo IP e numero di porta)
3) capisce a quale socket (applicazione attiva) consegnare i dati

>[!tip] Socket
>Socket è una interfaccia software che permette a un processo di inviare e ricevere messaggi
>- funziona come una porta comunicante per cui il mittente può inviare il messaggio e avere una struttura dati che finirà nelle mani del destinatario
>- I livelli fino a quello di trasporto sono gestiti dal SO
>- i livelli di applicazione sono controllati dallo sviluppatore dell'applicazione

#### Demultiplexing con UDP (senza connessione)
Vengono inviate le stesse identiche informazioni di un Demultiplexing normale, solo che quando un pacchetto arriva viene controllato solo il numero di porta e l'IP del destinatario (in questa fase quelli del mittente non contano).

>[!question] E allora perché IP e porta del mittente vengono comunque inviati?
>Servono esclusivamente per far sì che il destinatario possa rispondere se necessario.

![[Pasted image 20250331193731.png]]

#### Demultiplexing con TCP
Qui abbiamo una connessione e quindi la trasmissione diventa più "complessa" ma molto più sicura.
Qui viene controllata la **quadrupla** formata da
1) **IP di origine**
2) **Porta di origine**
3) **IP di destinazione**
4) **Porta di destinazione**
Quando un pacchetto arriva, viene controllato sia il destinatario ma anche il mittente, per poter identificare esattamente quale connessione è attiva tra due processi.

##### 🛠 Cosa succede sul server?
1) Il server crea una **socket passiva**, ossia una (unica) socket passiva per "ascoltare" le richieste dei vari client. 
	Questo significa: "chiunque voglia connettersi, mi mandi un segnale qui."
2) Quando un utente si connette a questa socket invia una richiesta di connessione.
3) Il server accetta la connessione e crea una nuova socket "connessa" (privata con il client).
	Questa nuova socket ha
	- stesso IP e porta locali del server
	- IP e porta remoti diversi (del client)

4) se un altro client invia una richiesta viene creata una nuova socket con le stesse caratteristiche dell'altra

>[!tip] NOTA BENE
>Anche se entrambe le connessioni vanno allo stesso IP e porta del server, il server le distingue grazie alla quadrupla.


![[Pasted image 20250331193757.png]]

### Differenza tra URI URL e URN
🔹 URI — **Uniform Resource Identifier**
- li indica tutti
🔸 URL — **Uniform Resource Locator**
- dice dove è localizzata una risorsa
🔸 URN — **Uniform Resource Name**
- indica il nome identificativo univoco della risorsa ma non dice dove sta

![[Pasted image 20250327164800.png|400]]

### Architettura Peer-to-peer
architettura che si basa su più dispositivi che fungono sia da client che da server
per avere la definizione perfetta vai a vederti [[RETI LEZ.4#peer-to-peer|questo]] 
#### Esempio Distribuzione file client server P2P
Se ho <font color="#4f81bd">N</font> peer quanto impiego a trasferire un file di dimensione <font color="#c0504d">F</font>?
![[Pasted image 20250327165158.png]]
## Client-server vs P2P
### Esempio con Client-Server
![[Pasted image 20250327165442.png|400]]
Il server: Deve inviare N copie in sequenza con
- un tempo per singola copia di $F/u_s$ 
- tempo per N copie $N*F/u_s$ 
il client: Ogni utilizzatore del servizio deve scaricare una copia del file con:
- $d_{min}$= quantitativo di banda non fissa
- tenere ben presente un dato 
	- la banda minima di un determinato client segnata da $F/d_{min}$
Quindi avremmo:
![[Pasted image 20250327165929.png|400]]

### Esempio con P2P
Trasmissione via server: Esso deve inviare almeno una copia così che entri in circolo tra i client con un tempo di
- $F/u_s$
client: ogni client deve scaricare la copia una volta con tempo
- $F/d_{min}$
i client dopo aver scaricato: loro devono caricare $NF$ bit
- con una capacità di upload che è $u_s+\sum u_i$ 
![[Pasted image 20250327170707.png]]


## Grafico P2P VS Client-server
![[Pasted image 20250327172614.png|400]]
## tracker e torrent
possiamo innanzitutto dire che i file sono divisi in(chunk) che vengono scambiati tra peer
- Per sapere la lista dei peer a me vicino utilizzo il tracker che tiene traccia di tutti i peer che partecipano al torrent
-  Per torrent si indica il gruppo di peer che partecipano alla distribuzione di un file
	- Quindi quando scarichi un file .torrent hai tutti i metadati che ti rimandano al tracker e sai la dimensione e il nome dei chunk e dei file
### Esempio nella prospettiva di un peer
![[Pasted image 20250327171936.png]]
### Richiesta e invio di chunk file(BitTorrent)
##### Come avviene la richiesta dei chunk:
c'è innanzitutto da precisare che ogni peer di solito non ha la totalità dei chunk bensì una parte
- Alice quando vuole fare una richiesta andrà a chiedere ai peer vicini una lista dei chunk in loro possesso
- Alice andrà a scaricare i più rari per fare in modo che vadano in circolo prima e che essi siano più accessibili a tutti
- inizialmente può richiedere un blocco casuale perché così lo condivide subito ma poi, quando ha quasi finito di scaricare il file può adottare la strategia end game ovvero:
	- chiede quegli ultimi chunk rimanenti a più peer possibili così da soddisfare la richiesta il prima possibile
##### Come avviene l'invio dei chunk(tit-for-tat):
- Alice invia i chunk ai quattro peer a lei vicini che le inviano i chunk con la velocità più alta(sono detti unchoked)
	- rivaluta i posti ogni 4 secondi per definire chi saranno quelli choked e chi unchoked
- Ogni 30 secondi ne sceglie uno a caso tra i vicini e gli inizia a inviare i chunk 
	- esso è detto optimistically unchoked
	- esso può rientrare nella top 4
![[Pasted image 20250327173213.png|500]]
# Streaming e Video CDN
Lo streaming video rappresenta circa l'80% del traffico Internet. I video in genere sono registrati e memorizzati su server a disposizione degli utenti su richiesta on demand.

### Cosa sono i video
i video sono una sequenza di frame(immagini) visualizzate a tasso costante(fps)
### Cosa sono le immagini
sono un array di pixel dove ogni pixel è rappresentato da bit
### Codifica 
Esistono codifiche per ridurre la ridondanza di informazioni all'interno di immagini, ciò ci consente di ridurre quindi la dimensione in bit
- ad esempio se ho una schermata nera non mi conviene scrivere nero per ogni pixel ma scrivere che ogni pixel è nero e poi decodificarlo
Esiste la:
codifica spaziale: vale per la singola immagine
temporale: si applica tra più immagini
![[Pasted image 20250327173806.png|400]]
## Gestione del bitrate nei video 
CBR - Constant Bit Rate 
- Bitrate fisso, usa sempre la stessa quantità di dati per ogni secondo di video. 
VBR – Variable Bit Rate 
- Il bitrate varia in base al contenuto del video. 
    - Scene complesse = più bitrate 
    - Scene semplici = meno bitrate 

| **Formato** | **Dove si usa** | **Bitrate tipico**   |
| ----------- | --------------- | -------------------- |
| MPEG-1      | CD-ROM          | ~1.5 Mbps            |
| MPEG-2      | DVD             | 3–6 Mbps             |
| MPEG-4      | Internet/stream | da 64 kbps a 12 Mbps |
### Quindi come funziona lo streaming video(in modo semplice)
Semplicemente abbiamo un server video che ha il video registrato e che attraverso internet invia i contenuti al client
bisogna però tenere conto di 2 complicazioni principali:
- la larghezza di banda tra server e client varia nel tempo a causa di eventuali congestioni della rete
- scarsa qualità del video o ritardi del video
![[Pasted image 20250327174235.png]]
In teoria il tempo di invio del server dovrebbe essere costante verso il client così che il contenuto può essere visto in maniera fluida, ciò però è impossibile perché potrebbero esserci dei jitter(ritardi di rete), perciò il client dovrà utilizzare dei buffer per immagazzinare un po' le informazioni per avvantaggiarsi
Altri problemi potrebbero essere legati al fatto che:
- il client può muoversi avanti indietro mettere in pausa andare alla fine ecc..
- pacchetti persi da dover ritrasmettere al client

![[Pasted image 20250327174541.png]]
Qui possiamo notare tutte le varie compensazioni per ridurre questi problemi
- abbiamo un buffer video
- andiamo a riprodurre leggermente in ritardo sul client(caricamento)
	- in questo modo il client avrà una riproduzione costante anche se
	- possiamo vedere che la linea nera non lo è affatto
## Vari tipi di streaming
### Streaming UDP
- in questo caso il protocollo abbiamo visto che se ne frega di eventuali controlli e di congestioni
- possiamo dunque dire che i pacchetti verranno inviati a una frequenza simile a quella del bitrate del video stesso
- il client riceverà le informazioni e le salverà su un buffer piccolo perché tanto arrivano in tempi ristretti
- il controllo da parte del client è su una connessione separata 
	- controllo inteso come pausa play avanti ecc...
- Se la banda peggiora il video si interrompe perché il buffer è troppo piccolo
### Streaming HTTP
- il server invia alla massima velocità possibile
	- il fenomeno per cui il buffer continua a riempirsi anche se il client sta vedendo il video si chiama prefetching
- quando il buffer si riempie la velocità rallenta e si adatta alla velocità di consumazione del dato da parte del client
- gestisce molto meglio le variazioni di banda
- per fare il controllo si usa una riga di intestazione chiamata range che dice al server quale punto del video inviare
### Streaming dinamico adattivo HTTP
- Il client può **scegliere tra diverse qualità del video** (es. 480p, 720p, 1080p) **anche durante la visione**, in base alla rete disponibile in quel momento.
Questo è il metodo usato da piattaforme come YouTube e Netflix.

### Streaming multimediale DASH
sta per Dynamic Adaptive Streaming over HTTP
il lato server:
- divide il file in più chunk
- ogni chunk ha diverse versioni con bitrate diversi
- ogni versione è in un file diverso
- i file sono replicati in nodi CDN(vedi dopo)
- esiste un file manifesto che fornisce gli URL per andare a prendere i diversi chunk
il lato client:
- fa una stima periodica della banda che c'è tra client e server
- attraverso il manifesto richiede chunk di volta in volta 
	- in base alla versione del bitrate più sostenibile per la banda corrente
	- può cambiare bitrate quando vuole
	- è intelligente perché 
		- può determinare quando prendere un chunk
		- che encoding rate richiedere 
		- dove richiedere il chunk in un server vicino
Lo streaming video in sostanza è formato da
$$codifica+DASH+buffering\ di\ riproduzione$$ 
## Le CDNs
sta per Content Distribution Networks e risponde alla sfida di dover condividere milioni di video a milioni di utenti in modo simultaneo

#### Ci sono due opzioni
##### Opzione 1
Prevede un unico grande data center ciò causa problemi di:
- in caso di rottura non ho fonti di recupero
- creo congestione su un unico punto
- potrei essere lontano da alcuni client
- poco scalabile
##### Opzione 2
Memorizzo più copie video in punti diversi distribuiti geograficamente
- (enter deep)installo server della CDN in profondità di molti reti di accesso
	- così sono più vicino agli utenti
- (bring home) pochi ma grandi cluster di server in IXP vicino alle reti di accesso
Akamai è una azienda che conta centinaia di migliaia di server

##### Esempio con BOB
![[Pasted image 20250401121556.png]]

#### Esempio con NETFLIX
![[Pasted image 20250401121619.png]]
![[Pasted image 20250401121629.png]]

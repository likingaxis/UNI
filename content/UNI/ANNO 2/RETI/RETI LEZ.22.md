RICORDIAMO CHE:
- HSS 
	- si trova nella rete home dove hai il tuo abbonamento
	- è un database che ha i tuoi dati crittografati ecc...
- MME
	- è vicino a te in quel momento, si connette con l'HSS per avere i tuoi dati
	- e inoltre sa anche dove ti trovi per farti collegare con una BS adeguata
#### Compiti di mobilità principali delle reti 4G
I passi che avvengono quando un dispositivo si connette a una rete
1. Il dispositivo mobile deve fornire l'IMSI alla stazione base
	- IMSI serve per identificare in modo univoco l’utente
		- inoltre serve anche per far riconoscere la rete domestica a cui è collegato in modo contrattuale
2. la MME dialoga con l'HSS per dire la nuova posizione del dispositivo
	- la rete domestica ora saprà dove si trova 
3. MME ora deve configurare il tunnel per inoltro dei dati
	- tunnel che passa dal dispositivo al **P-GW** (Packet Gateway) della home network, passando eventualmente dal **S-GW** (Serving Gateway) della visited network.
4. Quando il dispositivo si sposta (es. cambia cella), viene eseguito l’**handover**, cioè il cambio del punto di connessione alla rete.
![[Pasted image 20250604191904.png|600]]

#### Configurazione degli elementi del piano di controllo LTE
Il piano di controllo è il “cervello” della rete, responsabile dell’autenticazione, del tracciamento del dispositivo, e della configurazione dei percorsi dati.

- il dispositivo mobile comunica con la MME attraverso un canale del piano di controllo
	- quel canale che consente di inviare segnali del piano di controllo
	- questo canale avviene attraverso la BS
- l'MME sfrutta IMSI per capire la rete domestica del dispositivo, MME contatta HSS per informare la home network dove si trova il dispositivo e per scoprire le informazioni crittografiche che ha solo HSS
- La BS e il dispositivo mobile si metteranno d'accordo per definire i parametri radio tra i due
	- definisci frequenze ecc...
![[Pasted image 20250604193433.png]]

#### Configurazione dei tunnel del piano dati per un cellulare
Prima abbiamo visto quelli del piano di controllo ora per i veri e propri dati
- Abbiamo un tunnel di comunicazione tra la stazione base e la S-GW
	- La S-GW invia informazioni all'indirizzo IP della stazione base
- un altro da S-GW a P-GW 
	- questo tunnel serve per instradare i dati dalla rete dove siamo alla Home network anche se ci troviamo in una rete ospite
		- tutti i nostri dati andranno sempre nella nostra Home network anche se ci troviamo in Giappone
		- meccanismo di instradamento indiretto
- incapsulamento attraverso GTP GPRS Tunneling Protocol
	- ma come facciamo a capire poi a quale device va inviato?
		- GTP incapsula i pacchetti del dispositivo dentro un altro pacchetto
			- al suo interno avremo il vero e proprio UDP che dentro avrà a sua volta IP
			- GTP ci permette di indirizzare adeguatamente i dati al nostro dispositivo mobile sempre in movimento
![[Pasted image 20250604194108.png]]
### processo di Handover tra BS nella stesa rete cellulare
cosa succede quando un dispositivo si sposta da una cella all'altra **senza cambiare rete**
il processo di Handover serve proprio a gestire casi come questi
- il dispositivo si sposta ma rimane connesso alla rete
#### Fase prima dell'handover
![[Pasted image 20250604194535.png|500]]
##### Richiesta di Handover e completamento dal dispositivo
![[Pasted image 20250604194638.png|400]]
- 1) La source BS si accorge che il segnale dal dispositivo sta degradando questo perché:
	- Le BS hanno varie statistiche come
		- quante celle hanno libere
		- il dispositivo con cui comunicano quanto va veloce ecc
- 2) Contatta la **target BS** inviando un messaggio di _“Richiesta di handover”_.
	- la target BS si prepara ad accogliere un dispositivo in più tenendo
		- una frequenza libera
		- una cella libera
	- invia poi un ACK alla BS source con le info necessarie per il collegamento.
- 3) La source BS informa adesso il dispositivo del nuovo BS target
	- A questo punto, **dal punto di vista del dispositivo**, l’handover è **già avvenuto**: comincia a inviare e ricevere dati dalla nuova **target BS**.
##### Se la vedono i BS
- 4) ora la source BS inoltra tutti i pacchetti che ancora gli arrivavano alla target BS
	- per non interrompere la connessione 
- 5)target BS informa l'MME che è la nuova BS
	- L’**MME aggiorna la S-GW**, ordinando di cambiare il **punto finale del tunnel** verso la nuova BS
- 6) La target BS invia un ACK finale alla source BS così che possa chiudere il canale radio e liberare la banda.
Tutti i nuovi pacchetti ora fluiscono **direttamente** dal **P-GW → S-GW → target BS → dispositivo**, senza passare dalla BS precedente.
![[Pasted image 20250604195159.png|400]]
![[Pasted image 20250604195328.png|400]]
- 7)Tutti i nuovi pacchetti ora fluiscono **direttamente** dal **P-GW → S-GW → target BS → dispositivo**, senza passare dalla BS precedente.
![[Pasted image 20250604195348.png|400]]

esse potrebbero fare un operazione di handover per staccare quel dispositivo per farne cercare uno migliore
Il dispositivo adesso si connetterà a una nuova BS target 
- ora i dati della S-GW verranno inviati alla nuova BS-target
	- attraverso...
##### Mobile-IP
È un tipo di architettura che serve per mantenere la mobilità nei dispositivi e quindi funzionare sempre
- agli inizi non si usava
presentava delle caratteristiche:
- 1) il traffico IP viene sempre instradato nella Home Network come nelle reti indirette
- 2) Home agent è un nodo nella home network che funge da punto di riferimento per il device 
- 3) Foreign agent invece è un nodo nella rete visitata, gestisce la rete quando il dispositivo è fuori casa
I protocolli di Mobile IP usavano **estensioni ICMP** (simili a “ping”) per:
- Rilevare la presenza di home/foreign agent,
- **Registrare la posizione** del dispositivo nella home network.
##### Wireless e mobilità, che impatto hanno su protocolli a livelli superiori?
Si riflette su protocolli di livelli superiori come TCP e UDP che sono protocolli fissi
- come funzionano con la mobilità?
##### Livello logico
al livello logico non cambia nulla perché sono sempre "best effort"
i protocolli si possono ancora usare perché si usano le Base Station e i vari nodi che lavorano su una rete fisica, è solo alla fine che viene usata una rete wireless
##### Livello prestazionale
qui peggiora tutto:
- il fatto che sia wireless aumenta drasticamente i ritardi ecc... soprattutto con gli handover dove si possono perdere molti pacchetti
	- ciò comporta scarti e ritrasmissioni
- Il protocollo **TCP interpreta ogni perdita come segnale di congestione**, quindi **riduce la velocità di invio**
	- quindi si peggiora la velocità di volta in volta
- essendo il traffico condiviso possono esserci problemi 
	- più utenti = meno banda per ciascuno

Soluzioni:
- al livello 2 si cercano di implementare ritrasmissioni affidabili così da far fare ritrasmissioni al protocollo TCP solo se strettamente necessario 
- Se il mittente sa che è su un collegamento wireless, può **gestire meglio le perdite** (es. distinguere errori da congestione).
- Dividere la connessione TCP in due parti:
    - Una tra client e access point.
    - L’altra tra access point e destinazione finale.
	- Questo **isola la parte wireless** dal TCP end-to-end.

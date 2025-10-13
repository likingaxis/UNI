### Differenza tra wireless e mobilità
- wireless
	- la comunicazione effettiva su un collegamento di tipo senza fili
- mobilità
	- azione del cliente che spostandosi cambia punti d'accesso a cui è connesso
### Componenti di una rete wireless
- Host wireless
	- laptop, smartphone ecc...
	- esegue operazioni e ha un collegamento wireless
	- eseguono le applicazioni
	- possono essere fissi o stazionari
- Collegamento wireless
	- utilizzato per collegare un host wireless alla stazione di base oppure un altro host wireless
	- di tipo condiviso, tutti potrebbero condividere stessa banda di frequenze
		- potrebbero esserci collisioni quindi i vari protocolli di accesso multiplo sono fondamentali
- Stazione base
	- elemento che funge da ripetitore, relay al livello di collegamento
	- di solito essa è connessa ad una rete cablata
	- es: access point o tower delle reti cellulari
![[Pasted image 20250528104430.png|400]]

### Differenze tra raggio di copertura e velocità dei collegamenti wireless su una tabella
![[Pasted image 20250528104630.png]]
##### Modalità differenti
si dividono principalmente in 2 tipologie
- con infrastruttura
	- vengono forniti dei servizi di rete 
		- grazie alle stazioni base su cui si connettono gli host wireless
	- handoff
		- azione che avviene quando un host si sposta dall'area di copertura e cambia punto di accesso con una rete più ampia
		- può addirittura cambiare sottorete
![[Pasted image 20250528104430.png|400]]
- Reti ad hoc, senza infrastruttura
	- senza stazioni base
	- gli host condividono solo ad altri nodi entro la loro copertura
	- gli host provvedono da se per fornire servizi di instradamento e altro ancora
![[Pasted image 20250528105453.png]]

###### Tassonomia delle due modalità differenti
tabella con hop multipli e non
![[Pasted image 20250528110720.png]]

#### Caratteristiche dei collegamenti wireless
##### Concetto di attenuazione
- Il segnale può essere assorbito o attenuato a causa dei diversi ostacoli
- anche solo semplicemente esso può essere attenuato dalla dispersione del segnale nella distanza
	- quando c'è uno spazio libero questa attenuazione si chiama di spazio libero
		- free space path loss
si può derivare una piccola formula
$(frequenza⋅distanza)^2=(fd)^2$
- Più **alta** è la frequenza o più **lontano** è il ricevitore, più **rapidamente** si perde il segnale.
![[Pasted image 20250528111841.png]]

##### Propagazione wireless su cammini differenti
- quando un segnale viene riflesso su diversi elementi che ci circondano, possono modificarne il loro tempo di arrivo o addirittura possono arrivare stessi pacchetti con tempi diversi
![[Pasted image 20250528112517.png|400]]
Per questo viene aggiunto il tempo di coerenza
- è un tempo per cui all'arrivo di un impulso ne possono arrivare altri da eventuali riflessi
- i tempi di coerenza non possono sovrapporsi quindi questo fa variare le velocità di trasmissione
![[Pasted image 20250528113426.png|400]]


##### Interferenze da parte di altre sorgenti
potrebbero esserci interferenze anche da altre frequenze come quelle Bluetooth oppure rumori elettromagnetici ambientali

- concetto di rapporto segnale-rumore (signal-to-noise-ratio) SNR
	- un SNR più grande facilita chi riceve il segnale ad estrarre il segnale trasmesso rispetto al rumore di fondo
	- infatti avremo un numeratore più grande dell'altro
- tasso di errore sui bit (bit error rate) BER
	- probabilità che un bit sia ricevuto in errore
##### Bilanciamento 
1. **Aumentare la potenza → aumenta SNR → riduce BER**
    - Ma consuma **più energia** (problema per smartphone, sensori, ecc.)
    - E **aumenta il rischio di interferenze** con altre comunicazioni
Poiché lo SNR cambia continuamente (mobilità, ostacoli, interferenze), i dispositivi wireless **adattano automaticamente**:
- La **modulazione**
- La **velocità di trasmissione**
Questo garantisce:
- Qualità accettabile
- Consumo energetico controllato
- Minori errori
L'immagine qua sotto fa vedere diverse tipologie di modulazioni
![[Pasted image 20250528120030.png]]

#### Terminali nascosti dei collegamenti delle reti wireless
A e C possono mandare a B ma non si comunicano tra di loro quindi non si sa se ci sono collisioni
ci sono due scenari dove abbiamo un terminale nascosto
![[Pasted image 20250528120217.png]]

### Protocollo di accesso multiplo per le reti wireless

#### CDMA (Code Division Multiple Access)
è un protocollo che permette di condividere lo stesso canale di comunicazione con più utenti senza troppe interferenze
Ogni utente ha un **codice unico** (una sequenza chiamata _chipping sequence_):
- Tutti gli utenti trasmettono **sulla stessa frequenza** e **allo stesso tempo**
- Ma il loro segnale è **"codificato"** con un codice specifico
ad esempio si possono applicare codici ortogonali con segnali che non si disturbano a vicenda
(es. $\vec{c}_1 \cdot \vec{c}_2 = 0$)

quindi per fare questa codifica:
- Si rappresentano i bit:
    - 0 → -1
    - 1 → +1
- Ogni bit $d_i$ è moltiplicato per la sequenza del codice c⃗ , ottenendo $d_i \cdot \vec{c}$ 
    - Se il codice ha lunghezza **M**, il bit viene "espanso" in M valori
invece poi per fare la decodifica chi riceve il segnale deve
- Il ricevitore riceve la somma dei segnali di tutti gli utenti
- Per estrarre i dati di un utente specifico:
    1. Divide i dati ricevuti in blocchi di M
    2. Calcola il **prodotto scalare** con il codice dell’utente
    3. Divide per M → ottiene il bit originale
![[Pasted image 20250528122813.png|500]]
![[Pasted image 20250528122827.png|500]]
>[!tip]- dimostrazione del perché funziona
>![[Pasted image 20250528122901.png]]
>


## Reti Wi-Fi con uno standard chiamato (802.11)
#### 802.11 Canali utilizzati
![[Pasted image 20250528123002.png]]
#### 802.11 architettura di queste LAN
qui gli host wireless comunicano con la stazione base come un access point
Una BSS è una infrastruttura che contiene:
- host wireless
- punto di accesso AP
- modalità ad hoc in cui i dispositivi comunicano tra loro direttamente 
![[Pasted image 20250528123119.png]]

#### Canali del 802.11 ovvero il Wi-Fi
- i canali sono la suddivisione di questo spettro di frequenze differenti
	- l'access point admin sceglie le frequenze per il punto di accesso
	- potrebbero esserci interferenze
		- un altro AP la vicino può scegliere lo stesso canale

![[Pasted image 20250528123601.png]]
#### 802.11 Associazione
- un host in arrivo nella BSS deve essere associato a un AP per farlo deve
	- scansionare gli AP vicini prendendo i vari frame beacon, ovvero quei frame che mandano periodicamente gli access point per farsi rilevare
		- contengono MAC address dell'AP e l'SSID( nome della rete)
	- l'host deve sceglierne uno e accedervi rispettando le varie protezioni come WPA2
	- Una volta associato e autenticato, l’host invia un messaggio **DHCP Discover** per ottenere un indirizzo IP.
	- Questo messaggio passa **attraverso l’AP**, che lo inoltra nella sottorete.
![[Pasted image 20250528123942.png]]
#### Scansione attiva vs passiva
![[Pasted image 20250528124155.png]]
#### Wi-Fi con accesso multiplo
Abbiamo bisogno di un protocollo per evitare collisioni nell'uso della rete Wi-Fi
- In questo caso ne vedremo uno con accesso casuale
	- non elimina collisioni ma le gestisce
#### CSMA/CA (Carrier Sense Multiple Access)
- ascolto il canale e vedo se qualcuno sta già trasmettendo
	- nella Ethernet era con collision detection CD Collision Detection
- invece qui abbiamo la CA, quindi senza rilevamento delle collisioni
	- Quindi si cercano di evitare, Collision Avoidance
	- Con il Wi-Fi per motivi hardware non si possono rilevare collisioni
##### CSMA/CA da parte del mittente
- DIFS(Distributed Inter Frame Space) è un intervallo di tempo per cui devo vedere per quanto tempo il canale deve essere libero prima di inviare i dati
- SIFS(Short Inter Frame Spacing) è più corto del DIFS e serve come intervallo di tempo per gli ACK e altre cose
- backoff: tempo del vero e proprio contatore dell'host

1. controllo se il canale è inattivo per DIFS, se lo è trasmetto il frame per intero senza Collision Detection
2. se invece è attivo bisogna trasmettere in differita
	- si sceglie un valore di ritardo casuale usando la binary exponential backoff
	- quando il timer backoff non è a zero allora aspetto che il canale sia libero per DIFS
	- il backoff decrementa, ogni volta che uno slot di tempo si libera
- quando il timer raggiunge lo zero allora si può accedere al canale se libero e si trasmette il frame per intero
- se non si riceve l'ACK si ripete il punto 2 incrementando intervallo di backoff 
- Se riceve ACK e ha altri dati da trasferire resetta intervallo backoff e ripete il punto 2
###### Da parte del destinatario
Invia un ACK dopo un intervallo SIFS 
IMPORTANTE: non entro nel canale appena si libera ma aspetto il tempo di backoff, perché non ci sono CD, le collisioni possono comunque esserci
![[Pasted image 20250528144451.jpg|300]]
### Ricapitolando
nelle reti wireless non posso avere Collision Detection, questo perché è tutto su frequenze alterne e oltretutto non tutto è visibile da tutti allo stesso modo
- inoltre la potenza di segnale trasmessa è sicuramente più forte di quella che dovresti sentire per rilevare se il canale è libero o meno
quindi quello che succede davvero è:
- Il nodo ascolta il canale.
- Se è occupato: aspetta che si liberi.
- Quando si libera: attende un tempo fisso (**DIFS**), poi parte un **backoff casuale**.
- Questo evita che più nodi trasmettano **esattamente nello stesso istante**.
Le collisioni possono comunque avvenire:
- **🕳️ Terminale nascosto**:
    - Due nodi non si vedono tra loro, ma entrambi vedono il destinatario.
    - Trasmettono pensando che il canale sia libero → collisione **sul destinatario**.
- **⏱️ Timer simili**:
    - Due nodi scelgono numeri di backoff **simili**.
    - Entrambi iniziano a trasmettere quasi contemporaneamente → collisione.
Per risolvere queste collisioni è stato ideato un meccanismo con prenotazioni per usare la rete
##### Meccanismo di prenotazione
il mittente deve prenotare il canale
- viene inviato un RTS al AP per prenotare l'uso del canale
	- potrebbero verificarsi collisioni con l'invio del RTS ma essendo pacchetti piccoli ciò non è un problema
- viene inviato poi dal AP un segnale di tipo CTS a tutti i nodi per dare pulizia
	- sostanzialmente tutti i nodi ricevono questo pacchetto Clear To Send dopo che un nodo ha inviato un pacchetto Request To Send
	- tutti gli altri dovranno rimandare eventuali trasmissioni
Foto esempio:
![[Pasted image 20250528144419.jpg]]
1. **A → AP: RTS (Request To Send)**  
    Il nodo **A** invia un messaggio RTS per “prenotare il canale”.
2. **B → AP: RTS (collisione!)**  
    Anche il nodo **B** prova a inviare un RTS nello stesso momento → **collisione della prenotazione** (niente dati ancora persi!).
3. **AP → A e B: CTS (Clear To Send)**  
    L’**Access Point risponde a A** con un CTS. Tutti i nodi che **sentono il CTS**, incluso **B**, **tacciono** per il tempo specificato.
4. **A → AP: trasmette DATA**  
    Solo A trasmette, perché ha ricevuto il CTS.
5. **AP → A e B: ACK**  
    L’AP invia conferma della ricezione del frame.

#### 802.11 i frame in particolare l'indirizzamento
![[Pasted image 20250528124604.png]]


#### Come cambia il frame da Ethernet a Wi-Fi?
Viene aggiunto l'indirizzo MAC dell'AP
![[Pasted image 20250528124717.png]]
Il router R1 **non sa** che H1 è collegato via Wi-Fi
quando il passaggio invece è da Wi-Fi a Ethernet si ha il contrario
![[Pasted image 20250528124918.png|500]]

##### Frame di indirizzamento con dei dettagli su
- la durata della trasmissione
- il numero di quel determinato frame
- il campo frame control si divide nei campi della foto sotto
- con tipologia del frame
![[Pasted image 20250528125140.png]]
#### Mobilità nella stessa sottorete 
- quando un host si sposta da un AP a un altro però mantenendo stesso indirizzo IP
	- inevitabilmente per avere stesso indirizzo IP sono collegati tutti e due dallo stesso switch
- come fa lo switch a capire da quale AP raggiungere H1
	- con auto-apprendimento
		- riceve un frame da H1 e si ricorderà quale porta usare per raggiungerlo
		- il nuovo AP invia un frame in broadcast con mittente H1 per far vedere allo switch dove si trova
		- lo standard 802.11f definisce un protocollo inter-AP per affrontare questi tipi di problemi e tanti altri
![[Pasted image 20250528125422.png]]

#### Funzionalità avanzate del 802.11
- la stazione base e la stazione mobile possono cambiare dinamicamente il tasso trasmissivo
	- la stazione mobile si sposta e cambia SNR
- gestione dell'energia
	- un host può dire di entrare in stato dormiente all'AP 
	- host si riattiverà solo quando l'AP sta per mandare un frame beacon
		- si sveglia, controlla se è nella lista e in caso si rimette a dormire
La lista nel beacon dice: “ehi, ho qualcosa per questi dispositivi!”
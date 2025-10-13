# Nucleo della rete
Ha il compito di trasmettere una richiesta da una periferia all'altra, quindi da un host ad un altro.
Questo nucleo è composto da una "**maglia**" di commutatori di pacchetti (router o switch) e i vari collegamenti tra i vari host.

Un host non può inviare dati (**messaggi di livello applicativo**) di grandezza arbitraria, per questo vengono suddivisi in **pacchetti** (packets) che la rete **inoltra** (forwards) da un router all'altro attraverso i **collegamenti** (links) lungo un **percorso** (path o route) dalla sorgente alla destinazione.

##### Due funzioni chiave del nucleo della rete
###### 1. Inoltro (forwarding o switching)
È un'azione locale che avviene all'interno di ogni singolo router.
Il router riceve il pacchetto su un'interfaccia di ingresso e, tramite una tabella (detta **di inoltro locale**) sceglie a quale interfaccia di uscita inoltrarlo.
La tabelle sono uniche per ogni router.

Prendiamo questa tabella
![[Pasted image 20250315162624.png]]
- l'intestazione rappresenta l'identificativo di un pacchetto
- l'uscita indica, al singolo router, dove "instradare" quel pacchetto

###### 2. Instradamento (Routing)
È un'azione globale che riguarda l'intero percorso dalla sorgente alla radice.
Si occupa di determinare il percorso migliore possibile tra i router della rete e per farlo i router utilizzano algoritmi di instradamento che calcolano le migliori rotte in base a parametri (es. distanza, velocità del collegamento, ecc.).
![[Pasted image 20250315163121.png]]

### Commutazione di pacchetto: store-and-forward
Ricordando che servono $\frac L R$ secondi per trasmettere (***transmit***) un pacchetto di $L$ bit attraverso un collegamento di $R$ bps.
Un router deve aspettare che TUTTO il pacchetto arrivi prima di poterlo trasmettere collegamento in uscita (store-and-forward).

![[Pasted image 20250315164118.png]]


###### Con un pacchetto
Quindi, il ritardo da un capo all'altro (end-to-end) per la trasmissione di un pacchetto su un percorso di $N$ collegamenti di pari velocità $R$ è dato da $$d_{end-to-end} = N \frac L R$$Trascurando il ritardo di propagazione e altre forme di ritardo.
###### Con $P$ pacchetti 
$$d_{end-to-end} = (N + P - 1) \frac L R$$dove il $-1$ lo mettiamo perché il primo arriva prima degli altri senza intoppi (quindi nella formula non lo contiamo), mentre gli altri invece saranno vincolati sempre dal primo.
Anche qui trascurando il ritardo di propagazione e altre forme di ritardo.

### Accodamento
Il problema dell'accodamento (*queuing*) si verifica quando il lavoro arriva più velocemente di quanto possa essere servito, ossia se il tasso di arrivo (*arrival rate*, in bps) al collegamento successivo eccede il tasso di trasmissione (bps) del collegamento per un certo periodo di tempo 

Ricordiamo che abbiamo un buffer in ogni router, e se questo si riempie i pacchetti si accodano sul collegamento di entrata (o di uscita del router precedente).
I pacchetti possono essere scartati in base a degli algoritmi che vedremo poi.


### Alternativa: commutazione di circuito
La commutazione di circuito è un metodo di comunicazione in cui viene stabilito un percorso fisso tra il mittente e il destinatario prima che inizi la trasmisisone dei dati.

**Le risorse lungo il percorso vengono riservate** (es. buffer, banda di trasmissione) e **rimangono dedicate per tutta la durata della comunicazione**.
Il trasferimento dei dati avviene a velocità costante e garantita.

>[!warning] PROBLEMA
>Se il circuito non è in uso, rimane inattivo e quindi diventa inefficiente rispetto alla commutazione di pacchetto.

#### Due tecniche di multiplexing per la comunicazione di circuito
###### 1. Multiplexing a Divisione di Frequenza (FDM)
L'intero spettro di frequenza del collegamento viene suddiviso in bande di frequenza e ogni utente ha la propria banda dedicata.
	PRO: più utenti possono essere trasmessi in parallelo
	CONTRO: la velocità di banda è ridotta
![[Pasted image 20250315164844.png|300]]
	
>[!question]- Ma se due utenti trasmettono contemporaneamente, come faccio a capire chi ha trasmesso?
>La luce è un'onda elettromagnetica, la cui frequenza è connessa ad un colore.
>Ogni combinazione di colori ha un risultato differente, quindi partendo da un colore possiamo risalire alla combinazione che l'ha generato.
>![[Pasted image 20250315165033.png]]

###### 2. Multiplexing a Divisione di Tempo (TDM)
Il tempo viene suddiviso in frame, che a loro volta contengono slot temporali.
	PRO: utilizzi tutta la larghezza di banda del circuito
	CONTRO: puoi trasmettere solo nel tuo slot dedicato  
![[Pasted image 20250315165206.png|400]]

##### Commutazione di circuito VS commutazione di pacchetto
![[Pasted image 20250315165302.png]]
Quindi
![[Pasted image 20250315165323.png]]

### Come si verificano ritardi e perdite?
I pacchetti si accodano nei buffer del router, aspettando il proprio turno per la trasmissione.
La perdita di pacchetti si verifica quando la memoria che contiene la coda dei pacchetti si riempie.
![[Pasted image 20250315165446.png]]
#### Quattro cause principali
![[Pasted image 20250315165457.png]]
(`d` sta per **delay**).
Dove
- $d_{elab}$ : elaborazione di nodo
	(tipicamente < microsecondi) si verifica per
	- controllo errori sui bit
	- determinazione del canale di uscita
	
- $d_{acc}$ : ritardo di accodamento
	si verifica per
	- attesa di trasmissione
	e dipende dal livello di congestione del router.
	
- $d_{trasm}$ : ritardo di trasmissione 
	tutto il discorso di $\frac L R$
	
- $d_{prop}$ : ritardo di propagazione 
	$$d_{drop} = \frac d v$$
	dove 
	- `d`: lunghezza del collegamento fisico
	- `v`: velocità di propagazione ($\sim 2 \times 10^{8}$)

#### Analogia della carovana
![[Pasted image 20250315170329.png]]


Quindi il ritardo totale è dato dalla somma dei ritardi che subisce ogni pacchetto ad ogni nodo, ossia $$d_{end-to-end} = \sum_{i} \left( d_{elab_i} + d_{acc_i} + d_{trasm_i} + d_{prop_i} \right)$$
### Intensità di traffico
Il ritardo di accodamento dipende dall'intensità di traffico, ossia il tasso di utilizzo della rete, definita dalla formula $$\frac {L \times a} R$$dove 
- `a` = velocità media di arrivo dei pacchetti (in pacchetti al secondo).

Abbiamo tre casi
- Se $\frac {L \approx a} R \sim 0$ 
	- il traffico è molto basso rispetto alla velocità disponibile e non ci sono ritardi significativi
	
- Se $\frac {L \times a} R \rightarrow 1$  
	- il traffico si avvicina alla capacità massima del collegamento con quindi un ritardo medio che tende a crescere
	
- Se $\frac {L \times a} R > 1$
	- I pacchetti arrivano più velocemente di quanto possano essere trasmessi; in questo caso il ritardo tende all'infinito e la rete diventa congestionata

![[Pasted image 20250315170428.png]]


## Perdita di pacchetti
La coda (buffer) che precede un collegamento ha capacità finita e quando il pacchetto trova la coda piena, viene scartato.
![[Pasted image 20250315170613.png]]

#### Throughput
Il throughput è la frequenza ($\frac {bit} {unità \ di \ tempo}$) alla quale i bit sono trasferiti tra mittente e ricevente. 
Abbiamo due tipi
- istantaneo: in un determinato istante
- medio: in un periodo di tempo più lungo (es. un file di $F$ bit in $T$ secondi è $\frac F T$ bps)
![[Pasted image 20250315170546.png]]

Guarda questa immagine
![[Pasted image 20250315170503.png]]

In entrambi i casi abbiamo un collo di bottiglia che vincola il throughput end to end

### Scenario di internet
![[Pasted image 20250315170516.png]]
Ovviamente abbiamo due casi
- se il traffico non è interessato (sto usando solo io la connessione) allora $$throughput \approx min\{R_j\}$$
	dove $R_{j}$ è la velocità di trasmissione dell'i-esimo collegamento
	
- altrimenti devo fare come nella foto sopra e suddividere la velocità tra i vari flussi che lo attraversano.  
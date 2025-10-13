## Due tipi di collegamento
1. Punto a Punto
		è presente un trasmittente a un'estremità e dall'altra c'è un ricevente esempi:
	- collegamento punto a punto tra host e switch Ethernet
		- un collegamento diretto con un cavo 
	- protocollo PPP per accesso dial-up
		- (Point-to-Point Protocol)
		- veniva usato per collegarsi ai modem telefonici, collegavi il pc al modem telefonico ed eri connesso al tuo ISP
2. Broadcast
		un canale di tipo broadcast che è condiviso tra più nodi che trasmettono e più nodi che ricevono, ogni frame viene condiviso tra tutti, ad esempio:
	- Ethernet ai vecchi tempi dove tutto il cavo era condiviso
	- wireless LAN oppure 4g/5g oppure il satellitare
![[Pasted image 20250521105540.png]]

>[!bug] cosa succede però con questi canali broadcast? 
>se avvengono due trasmissioni in modo simultaneo dai nodi si può incorrere in una collisione o interferenza 

>[!success] per risolvere si usano protocolli ad accesso multiplo
>presenta l'uso di un algoritmo che determina come i nodi condividono il canale, e quando essi possono trasmettere su di esso
>- Il **canale di comunicazione è uno solo**: anche i messaggi per organizzare l'accesso (es. “sto per trasmettere”) viaggiano **sullo stesso canale** dei dati.
> - 🔵 Quindi **non c’è un canale separato** (out-of-band) per il coordinamento.
### Entriamo nel dettaglio di questi protocolli ad accesso multiplo
###### Protocollo di accesso multiplo di tipo IDEALE
- questo protocollo MAC(Multiple Access Channel)
- ha un canale con velocità di R bps
L'ideale sarebbe che
- quando solo un nodo trasmette, esso può farlo con una velocità R
- quando invece M nodi si aggiungono alla trasmissione la velocità si riduce e diventa di circa $R/M$
- non ci sono nodi speciali che coordinano le trasmissioni è tutto decentralizzato
- non ci sono clock, time slot o altro
#### tipi di protocolli ad accesso multiplo reali
##### con Channel Partitioning
- il canale viene suddiviso
- ogni nodo ha la sua fetta di canale
- se non la usa quella fetta è inutilizzata
##### a Random Access
- il canale non è diviso e sono presenti le collisioni
- per risolverlo si effettuano delle ritrasmissioni ogni volta con operazioni di recover
##### a Taking Turns
- i nodi usano il canale a turno
- i nodi con più materiale da inviare possono usare il canale per più tempo

#### Spieghiamo nel dettaglio i vari protocolli
##### I TDMA (Time Division Multiple Access)
Fanno parte della categoria dei Channel Partitioning
- il canale qui viene suddiviso per istanti temporali fissi 
- la durata di questo tempo si dice time slot e di solito serve per trasmettere un pacchetto del livello di collegamento
- gli slot che non vengono utilizzati si dicono idle

![[Pasted image 20250521112454.png]]

- quando tocca a un determinato nodo esso può trasmettere a velocità R bps 
- ma visto che tanto può farlo in un lasso temporale di 1/N comunque trasmette a velocità media R/N
##### GLI FDMA (Frequency Division Multiple Access)
Fanno anche questi parte della categoria dei Channel Partitioning
- Il canale viene diviso in uno spettro di frequenze
- ogni nodo prende una determinata frequenza 
- se un nodo non trasmette sulla sua frequenza semplicemente essa viene inutilizzata
![[Pasted image 20250521112857.png]]
- la velocità è comunque R/N
##### SLOTTED ALOHA
Fa parte della categoria dei segnali ad Accessi Casuali
- ricordiamo che questi ultimi hanno dei nodi che trasmettono alla massima velocità, poi quando ci sono collisioni, ovvero due nodi trasmettono simultaneamente
- poi sarà opportuno rilevare le collisioni e recuperare i dati dalle collisioni
	- attraverso protocolli ad accesso casuale
Come funziona SLOTTED ALOHA?
- sostanzialmente abbiamo una serie di slot temporali
- quando un nodo vuole trasmettere attende l'inizio del nuovo slot temporale e invia
- se avviene una collisione perché un altro nodo lo stava usando avviene il recupero e quel nodo prova a ritrasmettere il frame allo slot temporale successivo con una probabilità $p$ di successo che ora spiegherò meglio
	- la collisione rilevabile ad esempio dalla **mancanza di ACK**.
![[Pasted image 20250521114813.png]]
##### PRO e CONTRO dello SLOTTED ALOHA
![[Pasted image 20250521114843.png]]

| ✅ **Pro**                                                                               | ❌ **Contro**                                                                                     |
| --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Trasmissione continua per nodo singolo**                                              | **Collisioni frequenti**: se più nodi scelgono lo stesso slot, si perdono i dati.                |
| **Alta decentralizzazione**: i nodi decidono in autonomia, senza coordinatore centrale. | **Slot sprecati**: la trasmissione probabilistica può lasciare slot vuoti anche se ci sono dati. |
| **Semplicità**: l’algoritmo è facile da implementare.                                   | **Sincronizzazione necessaria**: i nodi devono avere clock allineati per rispettare gli slot.    |
|                                                                                         | **Lentezza nel rilevare collisioni**: i nodi capiscono solo dopo aver completato lo slot.        |
##### EFFICIENZA dello SLOTTED ALOHA
È la **frazione di tempo** in cui **il canale viene usato con successo**, cioè **slot che non vanno sprecati** per collisioni o inattività.

> ➝ **Obiettivo**: capire **quanta parte del tempo il protocollo è realmente utile** per trasmettere dati senza errori.

- vengono fatti una serie di calcoli probabilistici che portano a dire che:
	- può usare il canale in modo efficace solo nel 37% del tempo, al massimo!
>[!tip]- sezione con i vari calcoli
>![[Pasted image 20250521115553.png]]
>![[Pasted image 20250521115601.png]]
>![[Pasted image 20250521115612.png]]

##### ALOHA PURO(Unslotted ALOHA)
- non vi è presente alcuna sincronizzazione
- appena arriva un frame esso viene trasmesso per intero e in modo immediato
- se avviene una collisione lo ritrasmette immediatamente con una probabilità $p$ 
- la probabilità di collisione senza sincronizzazione aumenta ancora di più
Efficienza 18%
![[Pasted image 20250521115829.png]]
#### CSMA(Carrier Sense Multiple Access)
- anche questo tipo è ad accesso Casuale
	- però risolve parecchie cose
- il nodo prima di trasmettere ascolta il canale e vede se è libero o occupato
"Come una conversazione tra persone: **non parlo se sento che qualcuno sta già parlando**."
- anche se il tutto è sincronizzato bene possono avvenire lo stesso collisioni
	- questo perché potrebbero esserci ritardi di propagazione ecc...
![[Pasted image 20250521120808.png]]


#### CSMA/CD(Carrier Sense Multiple Access)/(Collision Detection)
- con questo aggiornamento del protocollo viene aggiunta una detection delle collisioni
**Mentre trasmette**, il nodo **continua ad ascoltare**:
- Se rileva una **collisione**, **interrompe subito la trasmissione**.
- Così **evita di sprecare banda** per un frame che comunque sarebbe perso.
questo funziona bene via cavo ethernet ma difficilmente può funzionare via wireless

"Come se **inizio a parlare**, ma se sento **qualcun altro iniziare a parlare contemporaneamente**, **mi fermo subito**."
![[Pasted image 20250521120825.png]]

#### Spiegazione nel dettaglio dell'algoritmo CSMA/CD su una rete Cablata Ethernet
suddivisione in step:
- STEP 1:
	- Ethernet riceve un pacchetto dai livelli superiori, lo incapsula in un frame per la trasmissione di esso
- STEP 2:
	- La scheda Ethernet controlla se il canale di trasmissione è libero
		- se libero trasmette sennò aspetta finché non si libera
- STEP 3:
	- Se il **frame viene trasmesso tutto senza collisioni**, la trasmissione è **conclusa con successo** ✅
- STEP 4:
	- 🔴 Se sta per avvenire una collisione
		- il nodo che sta trasmettendo si interrompe subito
		- si invia un segnale di disturbo per avvisare tutti dell'avvenuta collisione
- STEP 5:
	- Dopo la collisione Ethernet(il nodo che vuole trasmettere) aspetta un tempo casuale prima di rientrare nel canale
		- entra in una fase di **binary exponential backoff**
			- sostanzialmente dopo una m-esima collisione sceglie un numero K tra ${0,1,2,...,2^{m−1}}$ 
				- e attende un tempo pari a $K×512$bit di tempo trasmissivo.
			- poi si torna allo STEP 2

###### Spiegazione grafica

![[Pasted image 20250521121704.png]]

![[Pasted image 20250521121712.png]]
![[Pasted image 20250521121720.png]]
##### Efficienza di questo protocollo
![[Pasted image 20250521121820.png]]
### Protocolli a rotazione di tipo POLLING
- i protocolli a suddivisione di canale visti prima 
	- con Channel Partitioning
		- se condivisi tra più nodi si ha una certa equità
		- ma se solo un nodo usa il canale avrà una porzione del canale e non può usarlo a pieno
- con i protocolli ad accesso casuale
	- con Random Access
		- un singolo nodo può usare il massimo del carico
		- se però più nodi vogliono usarlo aumenta l'overhead per le troppe collisioni
- con i protocolli a rotazione 
	- si cercano di mixare i due elencati prima
Nel polling é presente un controllore centralizzato nel sistema che dice ai nodi quanti frame possono trasmettere per turno con un massimo di frame per turno prestabiliti
- questo riduce collisioni e slot inutilizzati
- il controllore verifica se il canale è utilizzato, così riesce a capire se il nodo che invia sta sfruttando quei frame che può inviare
però purtroppo
- il fatto che ci sia un controllore che deve inviare al nodo un segnale che dice che può procedere a inviare tot frame
	- aumenta il ritardo
- il fatto che ci sia un solo controllore se esso ha problemi si rompe tutto
il Bluetooth usa questo sistema
![[Pasted image 20250521122639.png]]
#### Token passing

Viene passato questo token tra i nodi, il nodo può trasmettere quando ha questo token
- il fatto che questo token debba essere scambiato tra nodo e nodo aumenta overhead
- anche qui abbiamo un singolo punto di rottura il token
![[Pasted image 20250521122744.png]]

#### **accesso a Internet via cavo**, con un mix di **FDM, TDM** e **accesso multiplo casuale**
![[Pasted image 20250521123618.png]]
Per fare il downstream vengono usati dei canali FDM in broadcast 
- un solo CMTS(Cable Modem Termination System) trasmette nei canali quindi nessun problema di accessi multipli
Per fare l'upstream vengono usati diversi canali che vengono contesi da i diversi utenti con un accesso casuale
- vengono usati mini-slot a determinati utenti mentre gli altri vengono assegnati in modo casuale
###### Precisazione sullo standard DOCSIS
serve per impostare uno standard tra i modem via cavo e i CMTS 
- per il downstream viene usata una FDM che ricordiamo era una divisione delle frequenze
il CMTS invia un frame MAP che serve per dire a chi appartiene quale frequenza
- per sincronizzare il tutto
per l'upstream il tutto è diviso in mini-slot come spiegato sopra
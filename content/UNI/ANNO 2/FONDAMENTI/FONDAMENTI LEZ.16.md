### Osservazione
Se L(G) contiene un numero infinito di parole, allora la macchina che abbiamo creato nel teorema G.5 chiamata $NT_G$ che non rigettava le parole contenenti qualche non terminale di G, allora significa che qualche computazione(ramo) di $NT_G$ non termina(entra in loop)
- praticamente questa macchina applica produzioni e poi verifica se la parola ottenuta coincide con quella ricevuta in input
- e continua a farlo fino a quando non porta al risultato sperato
- e quindi se x ∉ L(G), per poter rigettare NTG(x) deve continuare ad ‘‘applicare produzioni’’ fino a quando non ha confrontato x con tutte le parole in L(G)
- ma abbiamo detto che $L(G)$ ha infinite parole
- quindi va a infinito
Quindi quando x ∉ L(G) NTG(x) non rigetta

>[!bug] il problema è che siamo in una grammatica di tipo 0
>- ciò ci obbliga a dover provare tutte le produzioni finché non raggiungiamo caratteri terminali 
>- anche se abbiamo una parola più grande dell'input possiamo comunque poi ricondurci attraverso delle produzioni alla parola che cercavamo
>- da "aaaaaasdadsdas possiamo produrre una parola piccola anche come solo a asdadasdas -> aa"

>[!success] se invece ci riduciamo a usare una grammatica di tipo 1
>- possiamo utilizzare la regola del:
>	- a sx devo avere una parola più piccola di quella a dx
>	- quindi se raggiungo una parola più grande dell'input sto sforando e posso terminare quella computazione
>	- Produzioni che diminuiscano la lunghezza della parola generata sono proibite nelle grammatiche di tipo 1

>[!tip] rivedendo la regola solita della grammatica di tipo 1 abbiamo che:
>questo significa che, se G =$<V_T,V_N,P,S>$ è una grammatica di tipo 1 e y è una parola in $(V_T \cup V_N)^*$ tale che $S ⟹_G y$, da y non è possibile derivare in G alcuna parola x la cui lunghezza è inferiore a quella di x 
>- (ossia, |x| < |y|)
>- ricordiamo che $S ⟹_G y$ questo significa che una serie di produzioni della grammtica portano risultato y

Con la grammatica di tipo 0 abbiamo definito una macchina di Turing che <font color="#9bbb59">accetta</font>
invece ora con quella di tipo 1 proveremo a definirne una che <font color="#ffff00">decide</font>
Andiamo ora a modificare la macchina $NT_G$ in modo tale che ciascuna computazione deterministica in NTG(x) rigetti non appena viene generata una parola che contiene più caratteri di $x$
### Procediamo con la creazione di questa macchina
![[Pasted image 20250409183750.png]]
praticamente queste produzioni ci portano a raggiungere un loop e che non aumenta la dimensione fino a superare x, quindi finiamo in un loop anche se siamo nel tipo 1 quindi nella macchina $NT'_G(x)$ 
![[Pasted image 20250409184118.png]]
Anche in questo caso siamo in un loop
Conseguentemente, poiché x ∉ L(G) e dunque nessuna computazione deterministica di $NT’G(x)$ accetta, la computazione $NT’G(x)$ non termina
- quindi  $NT’G(x)$ non rigetta
- quindi non decide ma accetta il linguaggio
- dobbiamo fare in modo che si accorga che sta per entrare in un loop
Come facciamo a capire se siamo in un loop?
- dovrei definire un numero per cui quella parola poi per forza è in loop
la risposta è facile $|V_T \cup V_N|^{|x|}$ 
- attraverso questa formula riusciamo a definire quali sono tutte le possibili combinazioni delle parole di una data lunghezza dell'input x 
- e dell'unione delle parole terminali e non
>[!bug] una volta superato questo numero siamo in un loop

in questo caso facciamo $(3+2)^{4+1}$ dove abbiamo
- 3 caratteri terminali
- 2 non terminali
- input x con cardinalità 4 
- sommiamo 1 perché indica che abbiamo sforato di 1
#### Definiamo una macchina $NT^1$ che lavora su grammatica di tipo 1
e che oltretutto aggiunge questo riconoscimento del loop!!
- usiamo un nastro $N4$ per calcolare il valore della formuletta fatta prima $|V_T \cup V_N|^{|x|}$ 
	- in unario, farà il calcolo
	- Prendiamo per assodato che esiste una macchina di Turing che calcola la formuletta in unario
		- prendendolo per assodato basta che sul nastro $N4$ effettuiamo una simulazione
- usiamo un nastro $N5$ per contare quante volte troviamo le parole di una determinata lunghezza in modo sequenziale e consecutivo
- esso sarà inizializzato a 1 e, con una parola y scritta sul primo nastro, ogni volta che viene generata (non deterministicamente) una parola z: 
	- viene incrementato di 1 (eseguendo una somma in binario) se |z|=|y|, 
	- mentre viene resettato a 1 se |z|>|y|
tipo becco 3 volte di fila una parola lunga 5 allora segno 3 


### Come opera la macchina  $NT^1$ nello specifico
- ha input x scritto sul primo nastro
si svolgono 2 fasi
##### Fase di inizializzazione
-  $NT^1$ scrive S sul secondo nastro e 1 sul terzo nastro
	- come faceva già quella del teorema G.5
- poi calcola la formuletta $|V_T \cup V_N|^{|x|}$ in unario sul nastro 4
- scrive 1 sul quinto nastro perché ha scritto 1 volta una parola di quella lunghezza
- sposta le testine sui simboli non blank più a sx di ogni nastro
	- ritorna all'inizio
##### Fase di iterazione
questa fase si divide in 2 sotto casi
##### 1. Generazione
 $NT^1$ simula non deterministicamente l'applicazione di tutte le produzioni possibili alla parola scritta sul secondo nastro a partire dalla posizione indicata sul terzo nastro
 - modifica attraverso una produzione la parola sul secondo nastro
	 - se la produzione non aumenta la cardinalità della parola
		 - allora siamo nel caso $|z|=|y|$
		- e incrementiamo di 1 il contatore sul nastro 5
	- altrimenti ri-inizializza il nastro 5 a 1
- se una produzione porta a un blank sul secondo nastro
	- allora nessuna produzione è stata applicata
	- quindi le ho finite e posso passare al carattere successivo
		- incremento di 1 il terzo nastro 
##### 2. Verifica
Quando una parola sul secondo nastro viene modificata
- se coincide con l'input sul primo nastro allora  $NT^1$ accetta
- altrimenti se la parola così ottenuta 
	- non contiene alcun non terminale (contiene solo terminali)
	- se ad essa non può essere applicata alcuna produzione 
	- oppure se è più lunga della parola x 
	- oppure se il valore scritto sul quinto nastro è maggiore di quello scritto sul quarto nastro 
	- allora $NT^1$ rigetta,
 - se non succede nulla di tutto ciò 
	 - ri-inizializzando a 1 il contenuto del terzo nastro e riposizionando a sinistra la testina sul quarto nastro

Poiché  $NT^1$ accetta una parola x se e soltanto se G genera x
- allora possiamo concludere che  $NT^1$ accetta L(G)

Ora vogliamo dimostrare come ultima cosa che invece lo decide
- sostanzialmente andiamo a dimostrare che per ogni parola $\notin$  L(G)  $NT^1$ rigetta
- Poniamo quindi di avere una parola x che non appartiene a L(G) e che siamo nel corso di una computazione con una parola y che $\in (V_T \cup V_N)^*$ 
- abbiamo 3 casistiche
- se y contiene solo caratteri terminali per costruzione di  $NT^1$ , S $⟹_G y$  allora 
	-  y ∈L(G) e dunque, 
		- poiché x ∉ L(G), y è  ≠  da x 
		- e la computazione deterministica della macchina rigetta
- se y contiene almeno un carattere non terminale ma $|y|>|x|$ allora 
	- la computazione della macchina rigetta
- se y contiene almeno un carattere non terminale e la cardinalità è nei limiti quindi abbiamo che
	- $|y|\leq|x|$ 
	- allora la macchina troverà una parola z da sostituire a y tale che $|z| \geq |y|$ 
		- questo perché siamo nella grammatica di tipo 1 quindi le parole possono solo crescere o rimanere uguali
	- fino a quando poi non ricaschiamo nei casi 1 o 2 oppure abbiamo sforato le parole con cardinalità uguale possibili
		- definite dalla formuletta $|V_T \cup V_N|^{|x|}$ 
quindi rigettano
e quindi possiamo dire che questa macchina  $NT^1$
- DECIDE L(G)
### COROLLARIO per finire

**L’insieme dei linguaggi di tipo 1 è un sottoinsieme dei linguaggi decidibili** o **ricorsivi**
- decidibili e ricorsivi so la stessa coda
##### **OSSERVAZIONE**
Mentre i teoremi **G.4** e **G.5** implicano che un linguaggio è accettabile se e solo se esso è generato da una grammatica (ossia, **gli insiemi dei linguaggi decidibili e l’insieme dei linguaggi generati da grammatiche coincidono**), il **teorema G.6** dimostra soltanto che **tutti i linguaggi generati da grammatiche di tipo 1 sono decidibili**, ma **non il viceversa**!


### Visione sull'insieme delle varie grammatiche + Linguaggi accettabili o decidibili
![[Pasted image 20250409194405.png|600]]


### Grammatiche context free di tipo 2
tutte le grammatiche di tipo 2 si dicono context free
per contesto si intende quale istanza mi fa avvenire quella determinata produzione
se ho solo produzioni che hanno una lettera a sx indipendentemente da dove mi trovo posso applicarle quindi sono senza contesto
Ricordando che le Grammatiche di tipo-2 
- possiedono solo produzioni nella forma 
	- A →$\alpha$  con A ∈ $V_N$ e $\alpha$ $\in (V_T \cup V_N)^*$ 
##### ESEMPIO
![[Pasted image 20250409195259.png]]
in questo caso a=b perché ogni volta che faccio una produzione che sostituisce a avrò anche una b e viceversa invece c no


### Esercizi da fare in casa da benedetta
![[Pasted image 20250409195313.png]]

[[Dijkstra_2024.pdf|pdf della lezione]]
### ALGORITMO DI DIJKSTRA 
###### Consente di trovare il cammino minimo in un grafo pesato
###### Cammino minimo su un grafo pesato
Sia $G=(V,E,w)$ dove $w$ indica il peso in inglese
il grafo deve essere orientato o non
quando il grafo è pesato il cammino viene dato dalla
quindi in base alla somma dei pesi
prendiamo un cammino $\pi = <v_{0}, v_{1}, v_{2},...,v_{k}>$
avremo un costo:
$w(\pi) = \sum_{i=1}^{k} w(v_{i-1}, v_i)$
Ora che abbiamo visto la definizione di cammino con i pesi vediamo la vera e propria **definizione di cammino minimo**

tra una coppia di vertici x e y è un cammino che ha costo $\leq$ a quello di ogni altro cammino tra gli stessi vertici $x$ e $y$
>[!warning] non deve averne per forza 1
>esempio su excalidraw
>![[Pasted image 20241223095643.png|300]]
>esempio slide prof
>![[Pasted image 20241223095822.png]]

### ESEMPIO con pesi negativi
si può notare come ci sia $-1$ o $-10$
questo non si può fare con Dijkstra
![[Pasted image 20241223095918.png]]
Un cammino minimo viene detto **distanza**

##### PROBLEMA reale: 
dati u e v, trovare un cammino minimo(distanza) tra due nodi
![[Pasted image 20241223100034.png]]
- se il peso $w$ è dato dalla lunghezza in km abbiamo la strada più breve
- se il peso $w$ e il tempo di percorrenza avremo la strada più veloce

##### Esiste sempre un cammino minimo da u a v?
- se non esiste un cammino tra u e v no
	- diciamo che la distanza $d(u,v)=\infty$
- se abbiamo un cammino con un ciclo che ha un costo negativo allora non va bene
	- diciamo che e $-\infty$
![[Pasted image 20241223100551.png]]
- se non esistono cicli negativi in G esistono dei cammini minimi detti semplici
	- che non contengono nodi ripetuti
###### Sotto-struttura ottima
Ogni sotto-cammino di un cammino minimo è a sua volta un cammino minimo 
###### Dimostrazione
usiamo la tecnica del cut & paste per dire che se quello non era un cammino minimo allora assumiamo per assurdo che ne esista uno più corto, dopo aver tagliato ci accorgiamo che ne esce uno ancora più piccolo quindi significa che quello di prima era il più corto
![[Pasted image 20241223100856.png]]

##### Disuguaglianza triangolare
$\forall \ u,v,x \in V  \ \ \ vale \ \ \ d(u,v) \le d(u,x) + d(x,v)$
$d$ indica la distanza
![[Pasted image 20241223101113.png]]

##### Cammini minimi a singola sorgente
nel grafo prendiamo una sorgente $S$, dalla sorgente $S$ vogliamo calcolare tutti i cammini minimi che partono da esse

![[Pasted image 20241223104345.png|300]]

SPIEGAZIONE DEL PROBLEMA:
due varianti:
- Dato $G = (V,E,w)$ con $s \in V$, calcola le distanze di tutti i nodi da $s$, ovvero $d_G(s,v)$ per ogni $v \in V$ 
- Dato $G = (V,E,w)$ con $s \in V$, calcola l'albero dei cammini minimi di $G$ radicato in $s$
che significa la seconda?
che abbiamo un albero T con radice s, formato dai suoi cammini minimi con corrispondenza 1:1
c'e tipo $d_T(s,v)=d_G(s,v)$
con questo albero rappresentiamo n-1 cammini minimi da s a v
COSA CI RICORDA? il BFS(funziona senza pesi)
### Albero dei cammini minimi (o Shortest Path Tree - SPT)
dijkstra in output mi da lo shortest path tree
invece questo SPT con
![[Pasted image 20241223105120.png]]
![[Pasted image 20241223105141.png]]


#### ESERCIZIO PER CASA
![[Pasted image 20241223105602.png]]
#### Ora parliamo del vero e proprio DIJKSTRA
Assumiamo che tutti i pesi siano $\geq0$
- ogni arco $(u,w)$ ha $w(u,w)\geq0$
###### Idea dell'algoritmo
![[Pasted image 20241223111829.png|300]]
andiamo a scoprire i cammini minimi 
prendiamo tipo che gli archi siano dei tubi e $S$ è la sorgente dove sputiamo acqua costante
slide di acqua che scorre e che una volta raggiunto il nodo a una determinata celletta di acqua la prende
(ogni tubo viene diviso per il suo peso)
##### approccio greedy
1. per ogni nodo $v$ noi creiamo una stima della distanza, per eccesso.
	- ovviamente la prima stima deve essere per forza $D_{ss}$ 0 con se stesso
	- tutti gli altri devono essere $\infty$ 
2. mantiene un insieme X di nodi per cui le stime sono esatte 
	-  (nella gif sotto sono le stime dopo i collegamenti blu)
	- inizialmente $X = \{s\}$
3. l'algoritmo mi ritorna alla fine un albero $T$ con i cammini minimi
	- $T$ si aggiorna fino alla fine
	- $T$ non ha archi
4. Ad ogni passo inserisce in $X$ il nodo $u$ in $V-X$ con stima esatta
5. se una stima non è esatta allora avrò un arco <font color="#e36c09">arancione</font> se confermata <font color="#0070c0">blu</font>
6. Aggiorno le varie stime
![[Pasted image 20241223115515.png|300]]
- X si allarga piano piano
- nodi bianchi sono nodi a cui ancora non abbiamo scoperto il suo cammino che li raggiunge e sono a infinito
- arancioni sono quelli con cui almeno abbiamo un cammino però non sappiamo se è il minimo
	- li metto in una coda e ci metto la loro stima
--- 
ABBIAMO PARLATO DI STIMA ma come si aggiornano e 
La stima non aggiornata è data da 
$D_{sy} = min\{D_{sx} + w(x,y)\} : (x,y) \in E, \ x \in X$
dove
- $D_{sx}$ indica la distanza tra la radice e il nodo da cui parte l'arco entrante in y, che ho già calcolato come **minima**
- $w(x, y)$ è il peso
- $(x, y)$ deve appartenere all'insieme $E$ di archi (deve esistere un arco tra $x$ e $y$)
- $x$ deve appartenere all'insieme di nodi con le stime confermate $X$ (questa cosa mi conferma ancora di più il primo punto)

Ogni volta che trovo una stima migliore la aggiorno 
Ad esempio
se un nodo $y$ è in coda con un arco $(x,y)$ associato
se aggiungiamo un nodo $u$ a $T$ troviamo un arco $(u,y)$ tale che
$D_{su} + w(u,y) < D_{sx}+ w(x,y)$
significa che abbiamo trovato un arco migliore di $(x,y)$ per raggiungere $y$ partendo da $s$ ovvero $(u,y)$
#### PSEUDOCODICE
![[Pasted image 20241223121034.png]]
- assegna ad ogni vertice $u$ nel grafo una distanza di $\infty$
- crea un albero che ha come X zero perché ha una area molto ristretta
- inserisce nella coda la prima scoperta s quindi 0
- fa un ciclo finché la coda non è vuota
- se non ho ancora mai visitato quel nodo avrò come media attesa infinito quindi procedo a inserirlo nella coda
	- metto u padre di v perché sta prima e ci accontentiamo di tutto
- se la media attesa già esiste
	- faccio un controllo se l'arco è meglio e in caso modifico il tutto
	- compreso il padre
![[ezgif.com-speed_14.gif]]
parto dal nodo S e mi leggo tutti i suoi archi, sommo i vari cammini e li metto come stima
faccio la stessa cosa e aggiorno la stima con decreasekey
Quelli arancioni sono i cammini scoperti
#### DIMOSTRAZIONE DELLA CORRETTEZZA, per assurdo
![[Pasted image 20241223123500.png]]
abbiamo un caso in cui la distanza diretta tra s e v è più piccola di quella passante per u
mettiamo che l'algoritmo sbagli e pensi che passando da u si faccia prima
allora l'albero T avrà $(s,u)$ con una freccia blu e $(u,v)$ con freccia blu
riprendiamo la cosa dei sotto-cammini e mettiamo due nodi $x$ e $y$ con $x \in T$ e $y \not\in T$   
![[Pasted image 20241223142320.png]]
$(s,x)$ avrà freccia blu
Però per la proprietà sappiamo che $\pi_{sy}$ ha costo minore di $D_{sv}$ e quindi l'algoritmo ha sbagliato poiché avrebbe dovuto togliere dalla coda con priorità prima `y` rispetto a `v`.

![[Pasted image 20241223142848.png]]
### COMPLESSITÀ
#### Complessità
Escludendo le operazioni sulla coda con priorità la complessità è $$O(m+n)$$dove
- `m` = numero di archi (visito al più tutti gli archi una sola volta)
- `n` = numero di nodi (entro in ogni nodo solo una volta)


Andiamo a vedere ora quanto costerebbe una coda con priorità in base a come è implementata.
Innanzitutto noi nell'algoritmo avremo
- `n insert`, inserisco tutti i nodi nella coda
- `n deleteMin`, tolto tutti i nodi dalla coda
- AL PIÙ `m decreaseKey`, al massimo dovrò cambiare le chiavi `m` volte 

Il costo delle operazioni nella coda con priorità cambiano in base alla struttura utilizzata

| <center>***STRUTTURA***</center>        | `Insert`                     | `DelMin`                                    | `DecKey`                               |
| --------------------------------------- | ---------------------------- | ------------------------------------------- | -------------------------------------- |
| <center>**Heap binario**</center>       | <center>$O(1)$</center>      | <center>$O(n)$</center>                     | <center>$O(1)$</center>                |
| <center>**Array ordinato**</center>     | <center>$O(n)$</center>      | <center>$O(1)$</center>                     | <center>$O(n)$</center>                |
| <center>**Lista non ordinata**</center> | <center>$O(1)$</center>      | <center>$O(n)$</center>                     | <center>$O(1)$</center>                |
| <center>**Lista ordinata**</center>     | <center>$O(n)$</center>      | <center>$O(1)$</center>                     | <center>$O(n)$</center>                |
| <center>**Heap binario**</center>       | <center>$O(log(n))$</center> | <center>$O(log(n))$</center>                | <center>$O(log(n))$</center>           |
| <center>**Heap binomiale**</center>     | <center>$O(log(n))$</center> | <center>$O(log(n))$</center>                | <center>$O(log(n))$</center>           |
| <center>**Heap di Fibonacci**</center>  | <center>$O(1)$</center>      | <center>$O(log(n))*$</center>(ammortizzata) | <center>$O(1)*$</center>(ammortizzata) |
Quindi
- $n·O(1) + n·O(n) + O(m)·O(1) = O(n^2)$ ***con array non ordinati***
	
- $n·O(n) + n·O(1) + O(m)·O(n) = O(m·n)$ ***con array ordinati***
	(ricorda che al 99% [[13. Grafi#^4975e1|il numero di archi `m` > numero di nodi `n` ]])
	
- $n·O(1) + n·O(n) + O(m)·O(1) = O(n^2)$ ***con liste non ordinate***
	
- $n·O(n) + n·O(1) + O(m)·O(n) = O(m·n)$ ***con liste ordinate***
	
- $n·O(log n) + n·O(log n) + O(m)·O(log n) = O(m·log n)$ ***utilizzando heap binari o binomiali***
	
- $n·O(1) + n·O(log n)* + O(m)·O(1)* = O(m + n·log n)$ ***utilizzando heap di Fibonacci***

LA SOLUZIONE MIGLIORE LA AVRÒ CON L'HEAP DI FIBONACCI.


>[!tip] Osservazione sulla `decreaseKey`
>Per rendere le complessità temporali sulla `decreaseKey` valida devo mantenere un puntatore diretto tra in nodo `v` nell'array dei nodi della lista di adiacenza del grafo e l’elemento nella coda di priorità associato al nodo `v`; tale puntatore viene inizializzato nella fase di inserimento di quest’ultimo all’interno della coda.



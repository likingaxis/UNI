[[visite_2024.pdf|pdf della lezione]]
20 febbraio
- scritto
- orale
- punti ipotetici problem set
## VISITE DI GRAFI
Vedremo la parte algoritmica dei grafi
- quali sono i modi piu standard per rappresentare un grafo in memoria?
- algoritmi di visita dei grafi
### I GRAFI IN MEMORIA
Ci sono principalmente 2 modi
prima li vedremo sui grafi non diretti poi sui diretti
### Prendiamo di avere un grafo non diretto
![[Pasted image 20241213164616.png|150]]
##### potremmo usare una matrice di adiacenza, una matrice $n*n$
![[Pasted image 20241213164459.png|200]]
come funziona?
- se non ci sono pesi usiamo variabili booleane 
	- dicendo che 1 se c'è accoppiamento oppure 0 se non c'è
- usiamo lettere ma conviene numerarli con tipo 1,2,3,...n
OCCUPA SPAZIO $O(n^2)$
##### Usiamo liste di adiacenza
![[Pasted image 20241213164734.png|250]]
per ogni nodo abbiamo una lista collegata che indica chi è collegato con quel nodo
OCCUPA SPAZIO $O(n+m)$
dove $m$ indica il numero di archi
Per capire il numero di record(archi) facciamo $\sum_{v \in V} \delta(v) = 2m$ 

ripreso dalla lezione [[ALGORITMI LEZ.14]]

### Grafi diretti
![[Pasted image 20241213165200.png|230]]
##### matrice di adiacenza
Usiamo la stessa rappresentazione della matrice ma non è simmetrica come prima,
![[Pasted image 20241213170108.png|300]]
in questo caso indico con 1 quando gli elementi verdi entrano dentro quelli in rosso


##### liste di adiacenza: mettiamo solo i gradi uscenti
![[Pasted image 20241213170213.png|300]]

##### Operazioni che dipendono dal tipo di struttura usato
##### grafo non diretto

| Operazione                             | matrice | liste                             |
| -------------------------------------- | ------- | --------------------------------- |
| Elenco di archi che si incrociano in v | $O(n)$  | $O\delta(v)$                      |
| vedere se c'è arco in (u,v)            | $O(1)$  | $O(min \{\delta(u), \delta(v)\})$ |
##### grafo diretto

| Operazione                             | matrice | liste         |
| -------------------------------------- | ------- | ------------- |
| Elenco di archi che si incrociano in v | $O(n)$  | $O\delta(v)$  |
| vedere se c'è arco in (u,v)            | $O(1)$  | $O(delta(u))$ |

#### Algoritmi di visita
servono per calcolare alcune informazioni importanti del grafo, e lo visitano
- Abbiamo un grafo G, in modo sistematico lo visitiamo esaminando i vari nodi e archi in esso
- Fare la visita ci genera un albero di visita(lo vedremo tra poco)
- Esistono due tipi di visite e fanno cose diverse
	- BFS, ampiezza
	- DFS, profondità
#### BFS Visita in ampiezza
###### COSA FA? è importante saperlo
Prende un grafo, prende un nodo sorgente S, si calcola tutte le distanze o cammini minimi(sono la stessa cosa) da S verso ogni altro nodo v

#### Ha diverse applicazioni
- Usato per fare web crawling
	- ogni pagina e un nodo di un grafo, e le pagine sono collegate
	- il search engine di google scopre cosi nuove pagine 
	- TORRENTIO funziona cosi!
- social networking
	- trovare gli amici che potresti conoscere
	- nodo per ogni utente
	- visito tutti i nodi vicini a quelli a distanza 1(gli amici degli amici)
- network broadcast
	- se voglio mandare un pacchetto in broadcast(da un nodo sorgente a tutti i nodi)
- garbage collection
	- Come scoprire memoria non piu raggiungibile da buttare
- risolvere puzzle(lo vedremo meglio tra poco)
	- tipo il cubo di Rubik
##### Chi sa risolvere il cubo di Rubik? io no
###### come risolvere in poche mosse il cubo di Rubik 2x2x2
![[Pasted image 20241213172330.png]]
- rappresentiamo il cubo di Rubik attraverso
	- il grafo delle configurazioni
	- un vertice e un possibile stato del cubo
- grafo non orientato
numero di vertici<= $8! * 3^8$
- Partiamo dalla configurazione già risolta e poi andiamo a tutti i vicini casi con 1 mossa
	- ci sono poi a sua volta altre sequenze di mosse che portano a nuove configurazioni
		- saranno tutte le possibili mosse con 2 mosse
	- poi ci sono 3 mosse 4 mosse ecc... finche il grafo non finisce
- la distanza tra il nodo S e il punto più lontano si dice eccentricità(distanza massima da S a un nodo)
	- si dice anche god's number, il numero minimo di mosse sufficiente per risolvere 
- andiamo a ritroso dal nodo in cui siamo fino al nodo per risolverlo
![[Pasted image 20241213172349.png]]
#### Algoritmo di visita in ampiezza
##### Codice
![[Pasted image 20241213172804.png|500]]

- uso una coda per salvare momentaneamente tutti i vertici visitati e mi segno la distanza dal vertice S
- facciamo un ciclo che scorre finche la coda è vuota, ovvero quando abbiamo visitato tutti gli elementi
##### Esempio di visita BFS
![[ezgif.com-speed_12.gif|500]]
- i tratteggi indicano che comunque già lo conosco nella cosa quel nodo e quindi non serve visitarlo
- se già conosci vai avanti

![[Pasted image 20241213175102.png|300]]

albero dei cammini di G radicato in S 
##### Nei grafi orientati
![[Pasted image 20241213175150.png]]
per i grafi orientati basta solo andare a vedere i nodi in uscita
###### Quanto costa fare una visita BFS
dipende da come rappresentiamo il grafo:
con le matrici di adiacenza abbiamo: $O(n^2)$
con le liste di adiacenza:$O(m+n)$ 
ma abbiamo delle osservazioni perché 
- se il grafo è connesso abbiamo $m\geq n-1$  quindi non conta $O(m+n)$ ma basta $O(m)$ 
	- poiché prevale asintoticamente
- si ricorda che il numero di archi m ha un upper-bound al numero totale di archi possibili con quel numero di nodi $m\leq n(n-1)/2$ 
	- si ha quindi che se $O(m+n)=O(n^2)$ -> $m+n$ sarà sempre con un upper bound a $n^2$
	- sempre se $m=o(n^2)$ -> deve rimanere strettamente sotto posso dire che le liste so mejo

#### Teorema
il livello di un qualsiasi nodo $v$ dell'albero BFS corrisponde al cammino minimo dal nodo v alla sorgente $s$
![[Pasted image 20241213181339.png|600]]

### Visita in profondità
OGGI VEDREMO SOLO COME FUNZIONA, Domani lo usiamo per calcolare tante cose
Per spiegarlo usa un labirinto e fa un esempio con la corda e il gesso
- ad ogni strada che prendo la segno con il gesso
- uso una corda per tornare indietro
![[Pasted image 20241213181833.png|500]]

##### PSEUDOCODICE
![[Pasted image 20241213182131.png|500]]
Funzione ricorsiva per ogni nodo, ogni nodo si fa un for che vede i suoi archi
- ad ogni nodo non visitato richiama la funzione ricorsiva
![[ezgif.com-speed_13.gif|600]]
rossi piccoli: ancora in attivo
rossi grandi: si usano in quel momento

![[Pasted image 20241213183544.png|200]]

bho nel grafo diretto è così
![[Pasted image 20241213183714.png|500]]

>[!bug] cammino minimo
>per contare i cammini minimi si deve usare la visita in ampiezza 
>quella in profondità non worka
#### Costo visita in profondità
- con liste $O(m+n)$
- con matrice$O(n^2)$

![[Pasted image 20241213183544.png|200]]
riprendendo l'albero possiamo fare delle considerazioni
- se prendo un arco $(u,v)$
	- l'ho contato e quindi formano un arco
	- oppure sono uno discendente/antenato dell'altro
![[Pasted image 20241213191743.png|500]]
se è orientato:
le stesse cose di prima ma si aggiunge una cosa
- $(u,v)$ possono formare un arco trasversale a sinistra 


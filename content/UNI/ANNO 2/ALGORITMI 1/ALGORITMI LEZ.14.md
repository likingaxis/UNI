[[grafi_2024.pdf|pdf della lezione]]
## I GRAFI
#### POCA STORIA
Il concetto dei grafi nasce nel 700 da Eulero, matematico che per risolvere un problema usò i grafi,
il problema: la citta di Konigsberg aveva 7 ponti, voleva farli visitare a un amico senza passare piu di una volta su un singolo ponte
![[Pasted image 20241205110809.png]]
##### Definizione di grafo(non orientato)
Un grafo G=(V,E) 
- V= vertici o nodi
- E= insieme di coppie non ordinate di vertici detti archi
###### Grafo di Eulero
![[Pasted image 20241205111127.png]]
<font color="#f79646">questo si dice multigrafo quando ha archi paralleli (collegamenti)</font>
il grafo di Eulero possiamo vedere che ha <font color="#c0504d">4 vertici</font> e <font color="#c0504d">7 coppie</font> ovvero i collegamenti
$V={A,B,C,D}$
$E={(A,B), (A,B), (A,D), (B,C), (B,C), (B,D), (C,D)}$

###### 3 ESEMPI DI GRAFI PARTICOLARI
![[Pasted image 20241205111447.png|250]]
<font color="#4bacc6">grafo completo </font>
- c'è un arco per ogni coppia di vertici, tutti i nodi sono collegati tra loro
![[Pasted image 20241205111707.png]]
<font color="#4bacc6">a stella</font> 
centro e le punte formando una stella

![[Pasted image 20241205111818.png|300]]
<font color="#4bacc6">grafo a caso</font>
bho un classico grafo non direzionato



###### Grafo che modella scenario sulla scacchiera dei possibili cammini di un rook
♜♜♜♟️♟️
![[Pasted image 20241205112057.png]]
qui si potrebbe usare un grafo orientato se ipoteticamente la torre dovesse fare solo una direzione senza tornare indietro

##### GRAFO ORIENTATO
esempio di grafo orientato con frecce
Un grafo diretto $D=(V,A)$
- $V=vertici$
- $A=coppie \ ordinate \ di \ archi \ diretti$
![[Pasted image 20241205112835.png|500]]

##### esempio di grafo sociale dove uno conosce il nome e cognome di un altro
c'è un arco $(u,v)$ se $u$ conosce il nome e cognome di $v$ 
![[Pasted image 20241205112933.png|600]]

#### TERMINOLOGIA DEI GRAFI
![[Pasted image 20241205113543.png]]
grafo non diretto:
- $n$ viene usato per indicare la cardinalità dei vertici $|V|$
- $m$ viene usato per il numero di archi $|E|$
- $u$ e $v$ sono adiacenti o vicini
- l'arco $(u,v)$ è incidente a $u$ e a $v$ 
- il grado($\delta$) di $u$ è il numero di archi che riguardano $u$ 
- grado di $G$=max tra tutti i vertici di tutti i gradi di $V$ 
	- deg $G$= $max_{ \{v \in V \} } \ \{ \delta(v)\}$

grafo diretto:
![[Pasted image 20241205114646.png]]

nell'arco $(u,v)$ sarà uscente da $u$ e entrante in $v$
il grado uscente ($\delta_{out}$) di $u$ è il numero di archi uscenti da $u$ 
il grado entrante ($\delta_{in}$) di $u$ è il numero di archi entranti da $u$ 
- grado entrante o uscente  di $G$=max tra tutti i $\delta_{out}$  oppure $\delta_{in}$di $V$ 
	- deg $G$= $max_{ \{v \in V \} } \ \{  \delta_{out} (v)\}$
	- deg $G$= $max_{ \{v \in V \} } \ \{  \delta_{in} (v)\}$
##### Relazione fra grado dei nodi e numero di archi
in un grafo non orientato:
![[Pasted image 20241205115131.png|400]]
non è orientato, facciamo la somma di tutti i gradi di tutti i vertici
otterremmo $2$ volte il numero di archi facendo una sommatoria $\forall$ $v$
$\sum_{v \in V} \delta(v) = 2m$

il numero di nodi di un grado dispari è sempre pari
in un grafo orientato:
![[Pasted image 20241205120205.png|400]]
$\sum_{v \in V} \delta_{in}(v) = \sum_{v \in V} \delta_{out}(v)= m$
#### Altre terminologie
![[Pasted image 20241205120720.png|200]]
- il cammino indica una sequenza di nodi connessi tra loro con archi
- lunghezza di un cammino: il numero di archi del cammino
- distanza tra due vertici indica il cammino piu corto per arrivare da un vertice a un altro
	- distanza tra L e A e 4 $(L,H,E,B,A)$ 
- G è connesso se esiste un cammino per ogni coppia di vertici
- ciclo: cammino chiuso che parte da un vertice e finisce nel vertice stesso
- il diametro indica la lunghezza massima dell'insieme di tutti i cammini minimi di tutti i nodi
	- $max_{u,v\in V}$ $dist(u,v)$
	- se non è connesso la distanza e infinito
###### ESEMPI
![[Pasted image 20241205123520.png|500]]

##### Grafo di Petersen
![[Pasted image 20241205123604.png|200]]
- percorribile ogni nodo in 2, quindi $diametro=2$
- ha un ciclo interno e un ciclo esterno, la stella e il pentagono
- tutti vertici hanno grado 3
##### grafo estremale di Hoffman
- di diametro 2 e grado 7
![[Pasted image 20241205123758.png|400]]
##### Grafo pesato
mettere dei pesi o costi sui grafi 
$G=(V,E,w)$
il cammino più corto si calcola sommando i pesi
![[Pasted image 20241205123908.png|300]]
![[Pasted image 20241205123919.png|300]]
#### Quanti archi può avere un grafo con n nodi
![[Pasted image 20241205124321.png|200]]
uno <font color="#4bacc6">totalmente sconnesso</font> ha 0 archi
![[Pasted image 20241205124426.png|200]]
uno <font color="#4bacc6">completo</font> ha m=|E|=$n*(n-1)/2$
- indicato con $K_n$
un <font color="#4bacc6">grafo semplice</font> può avere da $0$ a $n*(n-1)/2= \ \theta(n^2) \ archi$ 
##### grafo connesso ma con numero minimo di archi 
- non esistono nodi lasciati da soli
- $n-1$ archi
- aciclico non ha ciclo perché non ritorno su quel nodo
- libero
- radicato
![[Pasted image 20241205125509.png|500]]
##### Come dimostriamo che è n-1 ? induzione
caso base: il grafo ha un solo vertice 0 archi $n=1$ -> $(1-1)$ 
caso induttivo: 
nel caso in cui abbiamo un grafo con n nodi aciclico e connesso
- deve avere almeno una foglia
- rimuovendo questa foglia avremmo $n-1$ nodi e $n-2$ archi per l'ipotesi induttiva
>[!success] quindi T ha ancora n-1 archi

![[Pasted image 20241205130246.png]]
##### ESERCIZIO PER VEDERE DEFINIZIONI ALTERNATIVE
![[Pasted image 20241205130705.png]]
importante, se abbiamo un grafo G connesso deve avere almeno $n-1$ archi e al più $n^2$ archi
$m=\Omega(n)$ oppure $m=O(n^2)$
>[!bug] non è detto che se un grafo ha n-1 archi sia connesso
#### Come si risolve la cosa dei 7 pontos?
ciclo si <font color="#c0504d">dice euleriano</font> se puoi attraversare tutti gli archi di $G$ solo una volta
- quando un grafo ammette un ciclo euleriano? <--> tutti i nodi hanno grado pari
ammette invece un <font color="#c0504d">cammino euleriano</font> se tutti i nodi hanno grado pari tranne $2$ nodi
questo pontos non si può fare
![[Pasted image 20241205131208.png]]
### Pk i grafi?
utilizzato per reti stradali nodi=incroci archi=strade
per voli aerei nodi= aereoporti archi= rotte aeree
per la metro nodi=fermate archi=tratte metro
>[!info]- ecco esempi grafici
>![[Pasted image 20241205154310.png|400]]
>![[Pasted image 20241205154328.png|400]]
>![[Pasted image 20241205154347.png|400]]
>
#### PERCORSO PROFESSOR PASQUALE
Il professor pasquale voleva da centocelle arrivare alla pallalottomatica in breve tempo
il navigatore suggerisce il percorso migliore prendendo pesi degli archi come
-  la lunghezza(strada più breve)
- tempo di percorrenza(strada più veloce)
![[Pasted image 20241205154618.png|500]]


#### Reti sociali
![[Pasted image 20241205154648.png|500]]

Kevin Bacon ha mille collegamenti impossibile incredibile
![[Pasted image 20241205155533.png|400]]
#### Reti delle dipendenze
![[Pasted image 20241205155506.png|400]]
ci sono nodi che hanno compiti da svolgere
l'arco $(u,v)$ indica che u deve essere eseguito prima di v, in termini di compiti
- esami a propedeuticita
- moduli software di un progetto a dipendenze

Ordinamento topologico del grafo, mettendo le dipendenze da sx a dx
![[Pasted image 20241205155706.png]]
nodi: compiti da svolgere
archi u,v rappresentano conflitti
date esami e vincoli
certi esami non possono essere svolti lo stesso giorno
==vedere poi il problema alle ultime slide==
#### Numero cromatico
Per colorazione si intende "colorare" i nodi del grafo usando il minimo numero $X$ di colori evitando di mettere colori simili adiacenti.
![[Pasted image 20241205160535.png]]
$\chi(G)=3$



>[!pen]- ESERCIZIO
>![[Pasted image 20241205160453.png]]


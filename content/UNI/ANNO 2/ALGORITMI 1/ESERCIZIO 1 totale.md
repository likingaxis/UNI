### 1. 
![[Pasted image 20250622115057.png]]
### 2.
##### Teorema master

![[Screenshot_2024-10-23-11-59-54-17_45415775811cea13943236d9369df411.jpg|300]]
![[Screenshot_2024-10-23-12-27-58-82_45415775811cea13943236d9369df411.jpg|400]]
##### Fibonacci
![[Screenshot_2025-06-22-12-55-43-31_45415775811cea13943236d9369df411.jpg|400]]
##### Albero della ricorsione
##### 1-ario
![[Screenshot_2025-06-22-12-46-39-51_45415775811cea13943236d9369df411.jpg|300]]
##### b-ario
![[Screenshot_2025-06-22-12-52-08-60_45415775811cea13943236d9369df411.jpg|400]]
##### Cambio di variabile
- effettuo una sostituzione di variabile per ricondurmi a una forma nota
- una volta rappresentata la sostituzione ne effettuo un'altra con R(x) per rappresentarla consiglio di vedere gli argomenti della funzione $R$ rispetto a $T$ 
- ora sono in una forma notevole che già conosco e costa $O(log \ x)$
- sostituisco la x con la vera x
- fine
![[Pasted image 20241023132417.png|400]]

### 3.
#### Ordinare n interi compresi tra un val min e un val max
- si usa il radix sort con costo 
- $O(n+b)log_b(val_{max})$ 
- se b=n la base è ottimale con costo $O(2n)log_n(val_{max})$ 
#### Aggiungere $\sqrt n$ elementi a un heap binario di n elementi
- Merge con inserimenti ripetuti
- $O(\sqrt n \ log(n)$  
- con $\sqrt n$ elem e $log(n)$  altezza 
#### Fondere 2 heap binari uno con $n$ nodi e l'altro con $n^2$  nodi 
- Merge con inserimenti ripetuti, prendendo l'heap più piccolo e si fonde con quello più grande
	- $O(n \ log(n^2))$ = $O(n*2 log(n))$=$O(nlogn)$ 
- se invece voglio fare un merge da zero e quindi creare un heap che contiene i due dentro devo metterli in un array qualsiasi e poi faccio Heapify che ha un costo di $O(m^2 + n)$=$O(m^2)$ 
#### Fondere 2 heap binomiali con $n$ e $n^2$ nodi
- Merge con costo $O(log(n+n^2))$= $O(log(n^2))$=$O(log(n))$ 
#### Costruire un heap binario con n chiavi
- procedura heapify con costo O(n)
#### Costruire un heap binomiale con n chiavi
- Inserimento ripetuto in modo incrementale da 1 a n, poi unioni $log(n)$ quindi poi è $O(nlogn)$ 
#### Partendo da un nodo calcola nodi raggiungibili di un grafo diretto con matrice adiacenza 
- uso DFS, $O(n^2)$ per la profondità 
#### Cercare in albero AVL l'elemento più grande fra quelli più piccoli di un elemento dato x
Ricerca predecessore
- O(log n)
#### In un grafo non orientato e pesato, calcolare distanza tra tutte le coppie di nodi 
Dijkstra da ogni nodo $O(n(m+nlogn)$ 

#### Aggiungere 2 elementi ad un heap binomiale di n elementi
insert con
- $O(logn+logn)$ -> $O(log n)$ 

#### Calcolare in un grafo diretto e pesato il nodo più lontano da un certo nodo T
- Dijkstra e si seleziona v tale che d(t->v) sia massima
- $O(m+nlogn)$ 
#### Dato un vettore di n numeri, trovare i k elementi più grandi
- Ordina con merge sort e poi prende ultimi k elementi
- $O(n logn)$ 
####  Ordinare un vettore $V [1 : n]$ di $n$ bit $(V [i] ∈ {0, 1})$:
- Integer sort con n bit quindi k=O(n)
- algoritmo costa $O(n)$ 

#### Cercare elemento in una lista ordinata implementata con record e puntatori
- non è possibile fare un accesso casuale
- quindi si ha una ricerca lineare ordinata $O(n)$
#### Restituire gli elementi di un BST in ordine decrescente di chiavi
- visita nodo DX, Radice, SX ricorsivamente VISITA SIMMETRICA
#### Cercare in un grafo diretto e pesato quanto è lungo il cammino più corto da S a T che non usa archi e1 ed e2
- imposto archi e1 ed e2 un peso di 100
- applico Dijkstra e seleziono il percorso che va da S a T 
- $O(m+nlogn)$ 
#### Ordinare n interi compresi tra 1 e $nlog(logn)$ 
- Radix sort
- $O(nlog(log n))$ 
#### In un grafo orientato capire se tutti i nodi possono raggiungere 2 nodi T1 e T2
- invertiamo la direzione degli archi
- facciamo il DFS in T1 e T2 e controlliamo il risultato dell'algoritmo applicato
- $O(n+m)$
#### In un grafo pesato e non orientato, capire se esiste un cammino minimo da S a T che oltre a essere minimo passa per uno specifico nodo $u$ 
- Dijkstra in S
- trovo cammino minimo d(S-> u) e d(S-> T) 
- poi chiamo Dijkstra da u e vedo d(u->T)
- se d(S->u)+d(u-> t) è uguale a d(s->t) allora ok
- costo $O(m+nlogn)$ 
#### Costruire albero AVL contenente n chiavi prese in input
- n inserimenti -> $O(nlogn)$ 
#### Ordinare n interi compresi tra 1 e $n^4$
- Radix sort 
- costo $O((n+n)log_n n^4)$ -> $O(n)$ 
#### Dato un BST di n nodi, restituire tutte le chiavi associate in ordine crescente
- visita in profondità 
- in ordine simmetrico (SX,RAD,DX) 
- costo $O(n)$ 
#### In un grafo orientato capire se c'è un cammino da S a T di al più K archi che passa per uno specifico nodo w
- BFS in S per trovare d(S, w) 
- poi BFS in w per trovare d(w, T)
- se d(S, w)+d(w, T) $\leq K$  allora ok
- $O(n+m)$
#### Costruire un heap binario con n chiavi
- procedura Heapify
- $O(n)$ 
#### In un grafo orientato, capire se c'è un cammino da S a T di al più K archi che evita nodo specifico w
- elimino archi collegati al nodo w 
- poi faccio BFS in S e controllo se d(s->t)$\leq K$ 
- $O(n+m)$ 
#### Trovare k-esimo minimo in una lista ordinata di n elementi (implementata con record e puntatori)
- Ricerca lineare sequenziale 
- con record e puntatori non si può fare la ricerca casuale
- $O(n)$ 
#### Dato un grafo diretto G, stabilire se tutti i nodi possono raggiungere un nodo T
- inverto direzione archi
- DFS su t
- costo $O(n+m)$ 
#### In un arco non orientato completo e pesato, calcola albero dei cammini minimi con sorgente S
- Dijkstra in S
- poiché completo $m=n^2$ 
- $O(n^2+nlogn)$ -> $O(n^2)$ 
#### Ordinare un vettore di n interi compresi tra $n$ e $n^2$ 
- Radix Sort 
- $O((2n)log_n n^2)$ -> $O(n)$ 
#### Fondere due alberi AVL uno contenente $n$ nodi e l'altro contenente $logn$ nodi
- effettuo $logn$ inserimenti nell'albero da n nodi
- $O(logn*logn)$ -> $O(log^2n)$ 
#### Costruire un heap binomiale con n chiavi
- inserimenti ripetuti
- $O(nlogn)$ 
#### In un grafo diretto dire se un nodo T non può essere raggiunto da almeno un nodo S
- Grafo componenti fortemente connessi
- applico DFS 
- costo $O(n+m)$ 
#### In un grafo non orientato e pesato individua il cammino più corto da S a T che non passa per specifico nodo w
- Metto tutti gli archi di w a $\infty$ 
- applico Dijkstra in S e restituisco d(S->T)
#### Costruire un albero AVL con n chiavi in input
- n inserimenti 
- $O(nlogn)$ 

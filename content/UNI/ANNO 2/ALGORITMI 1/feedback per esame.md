1. idea
2. descrizione+pseudocodice
3. analisi
la descrizione deve aiutare il lettore a comprendere il codice
analisi di correttezza!= descrizione algoritmo
correttezza/complessita:
insieme di proprieta che combinate ti fanno avere correttezza o bound di complessità
==11:00==
Studiare spiegazione correttezza di tutti gli algoritmi
==16:00== mi sembra assurdo
### Riepilogo delle lezioni precedenti ragionato
- obiettivo principale:
	- introduzione alle analisi e progettazione di algoritmi
- nozioni necessarie
	- lessico
	- significato algoritmi
	- complessita
	- caso medio
- costruzione di una prima toolbox per analizzare e progettare
	- divide and conquer o roba simile
- esempi illustri di problemi/algoritmi/strutture dati
##### Nozioni necessarie
- modello di calcolo RAM a costi uniformi
- complessità nel caso peggiore e medio(da sapere solo che esiste)
- notazione asintotica
#### Problemi per fare esperienza
- zio paperone
- calcolo fibonacci
##### Altro strumento per correttezza
- Equazioni di ricorrenza
QUALI SONO SEMPRE NELLO SCRITTO
- Teorema Master
- metodo di iterazione
- albero della ricorsione
## Algoritmi
#### Di ordinamento
- selection sort $(\Theta(n^2))$
- merge sort $(\Theta(nlogn))$ D&C
- quick sort 
	- $(O(n^2))$
	- $(\theta(nlogn))$ caso medio
- quick sort randomizzato
	- $O(nlogn)$
caso medio vs algoritmi randomizzati
- Heap sort $O(n(logn))$
- bongo sort $O(binglao)$
==1:13==
- lower Bound ordinamento
	- $\Omega(nlogn)$ confronti nel caso peggiore
- Integer Sort(Bucket Sort)
	- $O(n+k)$ per $[1,k]$ elementi
==1:16== guala fischia
- Radix sort $O(n)$ se $k$ e un polinomio $O(n^c)$
#### Rappresentazione di alberi e algoritmi di visita
- visita in ampiezza BFS
- visita in profondita DFS
utilizzati per calcolare informazioni su alberi
#### problema del dizionario
- tipo di dato vs struttura dati
- BST $O(h)$ $h$ altezza
- AVL $O(logn)$ per garatire che $h$ e sempre logaritmico
#### problema della coda con priorita
==1:28==
- d-heap heap
- binomiali merge $O(logn)$
- heap di Fib(accenni solo complessita) $O(1^*)$
- complessita ammortizzata
#### Grafi
- rappresentazione in memoria
	- matrici di adiacenza$\Theta(n^2)$ vs liste di adiacenza $\Theta(m+n)$
	- conviene usare le liste di adiacenza
- visita BFS calc. SPT/ distanze singola sorgente (tutto con grafi non pesati) 
	- $O(m+n)$
- visita DFS trovare ordinamento topologico per DAG
	- componenti fortemente connesse
- algoritmo di Dijkstra SPT/singola sorgente su grafi pesati $\geq 0$  $O(m+nlogn)$ 
### ESERCITAZIONI
- ricerca binaria utile
- usando algoritmi che in tempo lineare trovavano informazioni sui suffissi e sui prefissi
- ==1:39==

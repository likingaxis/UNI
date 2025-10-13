[[cap4.5.pdf|pdf della lezione 7]]
# Heap sort
#### Come funziona?
- Ha un approccio simile al [[ALGORITMI LEZ.6#Algoritmo 1 _**Selection Sort**_|selection sort]]
- metodo di progettazione mediante struttura dati efficiente $O(log_n)$
- seleziona i numeri dal più grande al più piccolo(cercando il massimo e portandolo in fondo)
>[!question]- differenza rispetto al selection sort?
>usa una struttura dati che ci permette di estrapolare il massimo in tempo logaritmico

>[!info]- differenza tra tipo di dato e struttura dati
>- tipo di dato: definisce il modo in cui una collezione di oggetti è fatta, come ad esempio un dizionario avrà chiave valore, i suoi metodi insert, search ecc...
>- struttura dati spiega come una collezione di oggetti deve funzionare in termini di algoritmi efficienti
##### **OBIETTIVO**
Per fare l'heap sort bisogna progettare una struttura dati che abbia le seguenti caratteristiche:
- Dato un Array A generare H velocemente
- Trovare il valore più grande in H
- Cancellare l'oggetto più grande in H

#### **Albero d-ario**
Un albero che ha tutti i nodi interni con al _**più**_ d figli
>[!info]- precisazioni su alberi
> - RADICE, origine
> - PADRE, nodo che genera un altro nodo
> - FIGLIO, nodo generato da un padre
> - FRATELLI, figli dello stesso padre
> - NODO INTERNO, che è sia figlio che padre
> - FOGLIA, nodo senza figli
> - LIVELLI, nodi paralleli
> - ALTEZZA, cammino più lungo partendo dalla foglia fino alla radice contando le freccette

![[Pasted image 20241104122453.png|500]]

**Albero Completo**=Albero che ha nodi interni con d figli e non al più
![[Pasted image 20241104123245.png|400]]
#### Specifichiamo meglio la **struttura dati** che useremo per l'heap
- Abbiamo una struttura dati associata a un insieme di elementi S (i numeri disordinati)
- Deve essere **COMPLETO** fino al penultimo livello
	- deve essere rafforzato quindi a sinistra deve essere compattato
- Gli elementi di S sono memorizzati singolarmente in ogni nodo $v$
- deve esserci questa proprietà $chiave(padre(v))\geq chiave(v)$ $\forall \ nodo \ eccetto \ v$
>[!info]- esempio
>![[Pasted image 20241104125906.png|600]]

se questo albero ha n nodi la sua altezza non puo essere tantissima
#### 3 proprieta salienti
1. il valore massimo dell'insieme S è nella radice
2. albero con n nodi è alto $O(log_n)$ (lo vediamo subito dopo)
3. un heap con struttura rafforzata può essere rappresentato con un array di dimensione n
#### Dimostrazione punto 2
- prendiamo l'albero come completo fino al penultimo livello e avrò una sommatoria
- metto 1+ perchè rappresenta il nodo che deve essere almeno 1 della parte rafforzata
- il numero di nodi deve essere maggiore dell'altezza
- la sua altezza deve essere più piccola della sua larghezza
![[Pasted image 20241104131658.png|500]]
 
![[Screenshot_2024-11-04-13-40-10-43_45415775811cea13943236d9369df411.jpg|400]]
#### Dimostrazione punto 3
dimostriamo che sia sufficiente un array lungo $n$ applicando queste regolette mentre inseriamo gli elementi dell'albero dall'alto verso il basso
- la posizione 0 non la usiamo
- il nodo a sinistra verrà posizionato nella posizione doppia a $i$ dove siamo quindi $2i$
- il nodo a destra verrà posizionato nella posizione doppia a $i+1$ quindi $2i+1$
- ogni padre si posiziona in $\lfloor i/2 \rfloor$
- nello pseudocodice verrà indicato con $heapsize([A])$
![[Pasted image 20241104151542.png|500]]

>[!info]- se si ha bisogno di vedere un'altro esempio
>![[Pasted image 20241104151826.png|600]]
#### Funzione **FixHeap**
Quando abbiamo un albero che ha una radice più piccola non abbiamo un heap
- per albero si intende anche eventuali sotto alberi
- per risolverlo usiamo FixHeap
![[Pasted image 20241104153417.png|400]]
##### PSEUDOCODICE FixHeap
``` scss
fixHeap(nodo v, heap H)
    if (v non è una foglia) then
    // sia u il figlio di v con chiave massima
    if ( chiave(v) < chiave(u) ) then
        scambia chiave(v) e chiave(u)
        fixHeap(u,H)
```
>[!info]- codice di Guala complesso
> 
> ``` scss
> fixHeap(i, A)    // i è una posizione, A è l'array
> 1.   s = sin(i)  // ricorda che sin(i) = 2i, s è una posizione
> 2.   d = des(i)  // ricorda che des(i) = 2i+1, d è una posizione
> 3.   n = heapsize[A]  // numero di elementi totale di A
> 
> 4.   if (s ≤ n e A[s] > A[i])  
> 5.       then massimo = s   // se s è più grande di suo padre devo scambiarlo
> 6.   else massimo = i       // se s non è più grande di suo padre lo lascio
> 
> 7.   if (d ≤ n e A[d] > A[massimo])
> 8.       then massimo = d  // se d è più grande di suo padre devo scambiarlo
> 
> 9.   if (massimo ≠ i)   // questo vuol dire che i deve essere scambiato
> 10.       then scambia A[i] e A[massimo]
> 11.      fixHeap(massimo, A)
> ```
> 
>- s e d rappresentano le posizioni degli elementi a sinistra e a destra della radice che prendiamo come inizio albero ricorsivo
>- faccio due controlli uno per il ramo di sinistra e uno per il ramo di destra
>	- controllo se s o d sta sforando la dimensione dell'array e controllo se l'array nella posizione sinistra o destra è più grande del padre preso in quella determinata ricorsione(all'inizio potrebbe essere la radice)
>	- se si verificano uno dei due uso una variabile massimo per salvare la posizione altrimenti massimo rimane i
>- se massimo è stato cambiato scambio le due posizioni e richiamo la funzione ricorsiva prendendo il ramo più grande

>[!info]- animazione **FixHeap**
>![[ezgif.com-speed_4 1.gif|500]]
#### Complessità FixHeap
$O(log_n)$
#### Algoritmo per trovare il massimo
- l'albero deve essere un Heap
- scambiamo la radice dell'albero con l'ultima posizione a destra dell'albero
- togliamo la foglia(la radice) e la mettiamo da parte
- Applichiamo FixHeap per riordinare il tutto
![[ezgif.com-animated-gif-maker 1.gif|600]]
#### Complessità Trovare il massimo
$O(log_n)$

#### Heapify
- per avere gli elementi disposti bene farò delle chiamate ricorsive fino alla fine dell'albero dividendo parte sx dalla parte dx, una volta arrivato alla fine dell'albero inizio a organizzare correttamente gli elementi prendendo padre per padre con FixHeap
	- Prendo il sottoalbero sinistro e lo faccio diventare un heap
	- faccio la stessa cosa con il destro
	- MI RITROVO NELLA SITUAZIONE IDEALE DEL FixHeap, lo eseguo così avrò la struttura HEAP da cui posso estrarre il massimo.
##### PSEUDOCODICE Heapify

``` scss
heapify(heap H)
    Se (H non è vuoto) then
        heapify(sottoalbero sinistro di H)
        heapify(sottoalbero destro di H)
        fixHeap(radice di H, H)
```

#### Complessità Heapify
Per calcolare la complessità in modo semplice noi cerchiamo di calcolarlo su un albero completo binario e non come dovrebbe essere un heap
quindi se l'albero ha $n$ elementi noi avremo $n'\geq n$ e sia un ipotetico heap con $n'$
- di altezza $h$
- completo fino alla fine
- ci sarà la seguente considerazione
	- $T(n)\leq T(n')$
visto che $n$ rappresenta l'heap rafforzato e $n'$ rappresenta solo $n$ ma con i nodi in più per renderlo completo, inevitabilmente avrò che $n'\leq 2n$
![[Screenshot_2024-11-04-17-53-49-53_45415775811cea13943236d9369df411.jpg|707]]
###### Applico [[ALGORITMI LEZ.5#teorema master enunciato(easy)|Teorema Master]]
![[Screenshot_2024-11-04-17-54-11-10_45415775811cea13943236d9369df411.jpg|300]]

$$T(n) \le T(n') = O(n') = O(2n) = O(n)$$
visto che prima abbiamo detto che $n'\leq 2n$ allora inevitabilmente $2n$ lo posso scrivere come $n$  e fine.
#### Max Heap e Min Heap
già abbiamo visto l'algoritmo per trovare il massimo, se vogliamo farlo con il min useremo algoritmi simili ma con $\leq$
usare Max è meglio di min per fare il sort e lo vederemo subito

### L'Heap Sort
- Crea un Heap con Heapify
- Estrae il massimo n-1 volte mette il massimo nella posizione libera dell'array

```scss 
heapSort(A)
1. Heapify(A)    //O(n)
2. Heapsize[A] = n   // calcolo la grandezza dell'array

// da 3-6, n-1 estrazioni di costo O(log(n))
3. for i = n down to 2 do  // fino a 2 perché parto dalla posizione 1

4.     scambia A[1] e A[i]  // scambio l'elemento in posizione 1 (il max) con    
                            // quello in posizione i (il min)

5.     Heapsize[A] = Heapsize[A] - 1  // diminuisco la dimensione dell'array perché 
                                    // so che l'ultimo elemento è ordinato

6.     fixHeap(1, A)  // devo riordinare l'array perché ora ho il min in cima 
                      // all'albero e non va bene
```
![[heapsort-600.gif|500]]

>[!lemma] TEOREMA 
>L’algoritmo HeapSort ordina in loco un array di lunghezza n in tempo O(n log n) nel caso peggiore.
>

>[!question]- Perché abbiamo utilizzato il Max-Heap e non il Min-Heap? 
>nel senso perché estraiamo il più grande e non il più piccolo? 
>Perché così utilizziamo memoria costante, con il Min-Heap utilizzeremo memoria lineare.


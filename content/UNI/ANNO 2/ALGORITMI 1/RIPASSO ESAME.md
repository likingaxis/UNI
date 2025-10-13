# FIBONACCI




# RICERCA 
### RICERCA BINARIA (costo $O(log(n)$)
```c
RicercaBinaria(array A, elem x, int i, int j)
	if (i > j) then return -1
	
	m = [(i + j) / 2]  // PARTE INFERIORE
	
	if (A[m] == x) then return m
	else if (A[m] > x) then
		return RicercaBinaria(A, x, i, m-1)
	else 
		return RicercaBinaria(A, x, m+1, j)
```


---

# ORDINAMENTO BASATO SU CONFRONTI
### SELECTION SORT (costo $O(n^{2})$)
```c
SelectionSort(A)
	for k = 1 to n-1 do
		m = k
		
		for j = k+1 to n do
			if (A[j] < A[m]) then
				m = j
	
	Scambia A[m] con A[k+1]
```

### MERGE SORT (cost $O(nlog(n))$)
```c
MergeSort(A, i, f)
	if (i < f) then
		m = [(i + f) / 2]  // PARTE INFERIORE
		MergeSort(A,i,m)
		MergeSort(A, m+1, f)
		Merge(A, i, m, f)
	
	if (i = f) then return A[i]
```

### MERGE ($O(n)$)
```c
Merge(A, i, m, f)
	X = array ausiliario di dimensione f-i+1
	
	j = 1, k_1 = i
	k_2 = m+1
	
	while(k_1 < = m AND k_2 < = f) then
		if(A[k_1] < A[k_2]) then
			X[j] = A[k_1]
			incrementa k_1 e j
		else
			X[j] = A[k_2]
			incrementa k_2 e j
	
	if (k_2 < = f) then
		Inserisci alla fine di X -> A[k_2, f]
	else
		Inserisci alla fine di X -> A[k_1, m]
	
	Copia X in A[i, f]
```

### QUICK SORT ($O(nlog(n))$ oppure $O(n^{2})$)
```c
QuickSort(A, i, f)
	if (i < f) then
		m = partition(A, i, f)
		QuickSort(A, i, m-1)
		QuickSort(A, m+1, f)
```

### PARTITION
```c
Partition(A, i, f)
	x = A[i]
	inf = i
	sup = f + 1
	
	while (true)
		do (inf += 1) while (inf < f AND A[inf] <= x)
		do (sup -= 1) while (A[sup] > x) 
		if (inf < sup) then
			scambia A[inf] e A[sup]
		else
			break
		
		Scambia A[i] e A[sup]
	return sup
```


---

# Tipo di dato  
Specifica una collezione di oggetti e una serie di operazioni di interesse su tale collezione.
Nel senso immagina di avere un array di interi:
- collezione: tutti gli interi
- tipo di dato: l'array di interi e le operazioni che posso fare su quell'array
Allo stesso modo abbiamo:
- dizionario
- int, boolean, double ecc. (questi son tipi di dati PRIMITIVI)

# Struttura dati 
Organizzazione dei dati che permette di memorizzare la collezione e supportare le operazioni di un tipo di dato usando meno risorse di calcolo possibile.
Quindi il modo più ottimale in cui io posso gestire il mio tipo di dato. 

# HEAP E HEAPSORT (quindi ancora sui confronti) 
Proprietà Heap
1. completo fino al penultimo livello (struttura rafforzata: foglie sull'ultimo livello tutte compatte a sinistra)
2. gli elementi di S sono memorizzati nei nodi dell'albero (ogni nodo v memorizza uno e un solo elemento, denotato con `chiave(v)`)
3. le chiavi devono avere una proprietà,$$ chiave(padre(v)) \ge chiave(v)$$
Di conseguenza altre proprietà
4. Il `max` è contenuto nella radice
5. Con `n` nodi l'altezza è $O(log(n))$
6. UN heap può essere rappresentato con un array di grandezza `n`
	![[Pasted image 20241029093452.png|center|500]]

### FIX HEAP ($O(log(n))$)
```c
FixHeap(nodo v, Heap H)
	if(v non è una foglia) then
		sia u il figlio di v con chiave massima
		if(chiave(v) < chiave(u)) then
			scambia chiave(u) con chiave(v)
			FixHeap(u, H)
```

Versione per l'array
```c
FixHeap(i, A)
	s = 2i
	d = 2i + 1
	n = Heapsize[A]
	
	if (s ≤ n e A[s] > A[i]) then
		massimo = s
	else massimo = i
	
	if (d ≤ n e A[d] > A[i]) then
		massimo = d
	
	if (massimo != i) then
		scambia A[i] con A[massimo]
	
	FixHeap(massimo, A)
```

### Heapify ($O(n)$)
```c
Heapify(H)
	if (H non è vuoto) then
		Heapify(sottoalbero sx di H)
		Heapify(sottoalbero dx di H)
		FixHeap(radice di H, H)
```
###### Complessità (vedi meglio sul pdf)
![[Pasted image 20241029100737.png|center|450]]

### Heap Sort ($O(nlog(n)$)
Costruisco un heap con Heapify, scambio il primo elemento con l'ultimo (rispettivamente il massimo e il minimo) e decremento ogni volta la porzione di array da guardare
```c
HeapSort(A)
	Heapify(A)   // O(n)
	Heapsize[A] = n
	
	// O(nlog(n))
	for i = n down to 2 do  // l'ultimo elemento non ha senso controllarlo
		Scambia A[1] con A[i]
		
		Heapsize[A] = Heapsize[A] - 1
		
		FixHeap(1, A)   // mi serve per mettere il nuovo max all'inizio
```


# Altezza albero in base alle foglie
>[!lemma] LEMMA
>Un albero binario T con k  foglie, ha un altezza di almeno $log_2(k)$ 

***DIMOSTRAZIONE PER INDUZIONE SU K***
- CASO BASE: `k = 1`
	Quando `k = 1` l'albero ha **solo una foglia**, che è anche la **radice**, quindi l'altezza dell'albero è $0$, che è uguale a $log_2(1)$. QUESTO SODDISFA LA CONDIZIONE DEL LEMMA. 
	![[Screenshot 2024-11-05 134944.png]]

- CASO INDUTTIVO: `k > 1`
	Assumiamo che il lemma sia vero per tutti gli alberi binari con meno di `k foglie` e tentiamo di dimostrare che lo sia per un albero binario con `k foglie`.
	1. ***Nodo v***
		- consideriamo il primo `nodo v`, un padre, che si trova più vicino alla radice; `v` ha due figli (ed esiste perché abbiamo detto che `k > 1`). In pratica se sappiamo di avere più di una foglia, esisterà per forza un albero con due figli (nel nostro caso è proprio `v`)![[Screenshot 2024-11-05 134951.png]]
	
	2. ***Suddivisione dei figli***:
		- Uno dei figli di `v` (nel nostro caso `u`) è la radice di un sottoalbero con un numero di foglie compreso tra $$\frac k 2 \le NUMERO \space\space DI \space\space FOGLIE < k$$Nel senso, se io so che il mio albero in totale ha 3 foglie, vuol dire che:
			- `v` esiste, lo abbiamo dimostrato prima
			- `u` sarà il padre di ALMENO 2 foglie e AL PIÙ $k-1$ foglie (perché $< k$)
			- `l'altro figlio` sarà direttamente una foglia
			![[Screenshot 2024-11-05 134957.png|center|150]]
	
	3. ***Altezza dell'albero T***: 
		- L'altezza di T è ALMENO $$1 + h$$dove:
			- 1 è l'approssimazione di tutti i nodi dalla `radice` fino a `v` (compreso)
			- h è l'altezza del `sottoalbero con radice in u`
		
		- Per il `sottoalbero con radice in u` applichiamo l'ipotesi induttiva, perché ha `< k` foglie e all'inizio abbiamo assunto che l'ipotesi per chi ha `< k` foglie fosse ***sempre vera***, quindi$$h = log_2\left(\frac k 2\right)$$![[Pasted image 20241105134759.png|center]]
		QUINDI sostituendo$$1 + log_2\left(\frac k 2\right)$$$$= 1 + log_{2}(k) - log_{2}(2)$$$$= log_{2}(k)$$
		

# LOWER BOUND PER ALG BASATI SU CONFRONTI
Questa dimostrazione fa notare come il miglior algoritmo che si basa su confronti abbia costo $$\Omega(nlog(n))$$
Consideriamo l'albero di decisione di un qualsiasi algoritmo che risolve il problema di ordinamento di `n` elementi
L'altezza h dell'albero di decisione è almeno $log_{2}(n!)$ 

Utilizziamo la formula di Stirling: $n! \approx 2(\pi \space n)^{\frac 1 2} \times (\frac n e)^n$    
![[Pasted image 20241105161953.png|center]]


---

# ORDINAMENTO SENZA CONFRONTI
### Integer Sort ($O(n + k)$)
- Nel mio array trovo il `min` e il `max`.
- Creo un array di contatori in cui inserisco TUTTI gli elementi dal `min` al `max`.
- Per ogni valore che leggo nell'Array originale incremento il suo contatore.
- Una volta finito di scorrere l'array originale lo riscriverò inserendo numeri, in ordine, basandomi sul contatore.

```scss
Algoritmo IntegerSort (X, k)
1. Sia Y un array di dimensione k   // O(1)

2. for i = 1 to k do        // O(k)  
3.     Y[i] = 0       

4. for i = 1 to n do        // O(n)
5.     Y[X[i]] += 1   

6. j = 1                    // O(1)
7. for i = 1 to k do        // O(k)
8.     while (Y[i] > 0) do  // per i fissato,                                
                            // #volte eseguite è al più 1 + Y[i] -> O(k + n)
9.         X[j] = i
10.        j += 1
11.        Y[i] -= 1
```
##### Spiegazione di $O(n+k)$
![[Pasted image 20241105163558.png]]
>[!tip] La sommatoria di `Y[i]` fa `n` perché io nei `k` contatori salverò comunque `n` numeri

### Bucket Sort
Stessa idea dell'integer ma
- abbiamo un array di appoggio con delle LISTE (e non contatori)
- quando trovo una chiave che già è presente, la "appendo" nella lista
- ordino scorrendo le liste

```scss
BucketSort (X, k)
1. Sia `Y` un array di dimensione `k`
2. for i = 1 to k do          // creazione dell'array con liste vuote
3.	   Y[i] = lista vuota

3. for i = 1 to n do
5.	   appendi il record X[i] alla lista Y[chiave(X[i])]  
       // appendo (inserisco alla fine) l'elemento nella lista corretta

4. for i = 1 to k do
7.	   copia ordinatamente in `X` gli elementi della lista Y[i]
      // inserisco gli elementi nell'array originale nell'ordine corretto
```

>[!example] È stabile perché appendo ogni volta gli elementi in una lista, quindi mantengo l'ordine originale.

### Radix Sort
Viene utilizzato per ordinare n interi compresi tra `[1, k]`.
- Per ogni cifra presa in esame, viene utilizzata una passata del bucket sort.
- Viene scelta una base `b`, che servirà per costruire l'array di appoggio nel bucket (avremo un array `[0, b-1]`.

Si parte dall'i-esima cifra meno significativa, e si inserisce quella cifra nel bucket
- cifra presa in considerazione = chiave
- altre cifre = informazioni satellite

Poi, in base alla cifra successiva, SI SPOSTA L'INTERO NUMERO, se necessario, IN UN ALTRO BUCKET.
![[Pasted image 20241106142406.png]]
Tipo, il numero `2397`
- prima andrà nel bucket `7`
- poi verrà spostato nel bucket `9`
- poi nel `3`
- e infine nel `2`

>[!example] È stabile 
>Perché per ogni cifra utilizziamo il bucket, e sappiamo che bucket ordina in base all'ordine "precedente"; quindi quando visiteremo la `i-esima` cifra, allora sappiamo che si troverà nella posizione corretta

#### Complessità temporale
1. **NUMERO DI PASSATE DEL BUCKET SORT**
	- `n` numeri
	- il massimo è `k`
	- base `b`
	Allora il massimo numero (`k`) richiede circa $$log_{b}(k) \ \ \text{passate}$$(es. `999` in `b = 10` lo visito completamente in $log_{10}(999) \approx 3$ passate) 

2. **TEMPO PER OGNI PASSATA**
	- Impiego $O(n)$ per distribuire gli `n` elementi nel bucket
	- Impiego $O(b)$ per gestire i bucket, ossia "raccogliere" i valori che ho nei vari bucket (ricorda che io qui prendo l'intera lista e la copio, non la scorro mai per intero).
	
	QUINDI IL COSTO DI OGNI PASSATA È $$O(n+b)$$

3. **TEMPO TOTALE DI ESECUZIONE**
	- Devo eseguire $log_{b}(k)$  passate
	- Ogni passata costa $O(n+k)$
	
	COSTO TOTALE $$O((n+b) \cdot log_{b}(k))$$


---

# Calcolo altezza albero
Il nostro albero
![[Pasted image 20241118180502.png|center]]

Formato da due sottoalberi con le rispettive altezze
![[Pasted image 20241118180647.png|center]]

Per calcolare l'altezza totale $$h = 1 + \max \{h_{s,} \space \space h_{d}\}$$
Dove l'`1` sta ad indicare la radice.
##### PSEUDOCODICE
```scss
Altezza(v)
	if(v == NULL) then return -1
	
	sx = Altezza(sx(v))  // O(n)
	dx = Altezza(dx(v))  // O(n)
	
	return 1 + max{sx, dx}  // O(1)
```

ESEMPIO
![[Pasted image 20241118181308.png|center]]
Se vedi, io la radice la conto (anche se ha altezza `0`), quindi per bilanciare le foglie ritorneranno `0` $$1 + max\{-1, -1\} = 1 + (-1) = 0$$

---

# Implementazione Dizionario
Vogliamo far sì che TUTTE le operazioni su un dizionario
- `insert`
- `delete`
- `update`
costino $O(log(n))$ (cosa che con Array e Liste non è possibile)

### Binary Search Tree (BST)
Proprietà
- un nodo `v` ha una `chiave(v)`
- Il sottoalbero `sx` di `v` contiene TUTTI E SOLI elementi $\le chiave(v)$ 
- Il sottoalbero `dx` di un nodo `v` contiene TUTTI E SOLI elementi $\ge chiave(v)$ 
![[IMG_0423.png]]

ESEMPIO
![[Pasted image 20241124124213.png]]

### Ordinamento crescente in un BST
![[Pasted image 20241124124520.png|center|500]]
```scss
InorderTraversal(nodo)
	Se nodo != NULL then
		InorderTraversal(nodo.sottoalbero_sinistro)
		VISITA(nodo)
		InorderTraversal(nodo.sottoalbero_destro)
```

#### Dimostrazione
![[Pasted image 20241124170952.png]]![[Pasted image 20241124171021.png]]

## Operazioni
#### Search
Cerco una chiave `x`
Parto dalla radice
- Visito il nodo `v`
	- se $chiave(v) == x$ -> la ritorno
	- se $chiave(v) > x$ -> la cerco nel sottoalbero `sx`
	- se $chiave(v) < x$ -> la cerco nel sottoalbero `dx`

```scss
search(chave k)
	v <- radice di T
	
	while(v != NULL) do
		if (k == chiave(v)) then return elem(v)
		else if (k < chiave(v)) then v <- figlio sinistro di v
		else v <- figlio destro di v
	
	return NULL // se non ho trovato la chiave
```

Versione Ricorsiva
```scss
search(nodo v, chiave k)
	if (v == NULL) then return NULL
	
	if (k == chiave(v)) then return elem(v)
	else if (k < chiave(v)) then
		return search(sx(v), k)
	else 
		return search(dx(v), k)
```
###### ESEMPIO
Scrivo `search(7)`
![[Pasted image 20241124171903.png]]


#### Insert
L'idea è quella di inserire l'elemento come foglia nella posizione corretta.
Per far sì che accada simuliamo una ricerca con la chiave da inserire, seguendo questi passi
1. creo un nuovo nodo `u` con `elem = e` e `chiave = k`, che dovrò inserire
2. cerco la `chiave k` nell'albero, se non la trovo posso comunque identificare la foglia `v` che diventerà il padre di `u`
3. appendo `u` come figlio sinistro/destro di `v` così da rispettare le proprietà di ricerca
###### ESEMPIO
Scrivo `insert(e, 8)`
![[Pasted image 20241124172725.png]]


#### Delete
Abbiamo bisogno di  operazioni ausiliarie
- `Min/Max`
- `Precedessore/Successore`

##### Max (il mix è simmetrico)
Il max sarà l'ultimo figlio destro del sottoalbero `dx` della radice (non per forza una foglia, attenzione)
```scss
Max(u)
	v <- u
	
	while(figlio destro di v != NULL) do
		v <- figlio dx di v
	
	return v
```

Versione ricorsiva
```scss
Max(u)
	if(dx(u) == NULL) then return u
	
	return Max(dx(u))
```
###### ESEMPIO
Voglio cercare il minimo dell'albero con `radice 15` e il massimo dell'albero con `radice 6`
![[Pasted image 20241124173630.png]]

#### Predecessore/Successore
Il `predecessore` di un nodo `v` è un nodo avente massima chiave $\le$ `v`
- Nel senso, devo cercare l'elemento con chiave più GRANDE tra tutte le chiavi più PICCOLE di un nodo `v` 

Il `predecessore` di un nodo `v` è un nodo avente minima chiave $\ge$ `v`
- Nel senso, devo cercare l'elemento con chiave più PICCOLA tra tutte le chiavi più GRANDI di un nodo `v`

```scss
Predecessore(u) 
	if(u ha un figlio sinistro sin(u)) then
		return max(sin(u))   // chiamo il max implementato prima
	
	// se non ha un figlio sx, il pred sta nei padri
	while(padre(u) != NULL e u è il figlio sx di suo padre) do
		u <- padre(u)  // continuo a salire
	return padre(u)  
	// se esco dal while vuol dire che u è un figlio destro o la radice
```
![[Screenshot 2024-11-24 180319.png|center]]


#### Delete
Sia `u` il nodo contenente l'elemento `e` da cancellare
Abbiamo tre casi possibili
1. `u` è una foglia -> la rimuovo
2. `u` è un padre con un solo figlio -> lo rimuovo e collego il figlio al `padre(u)`
	![[Pasted image 20241124181244.png|center]]
3. `u` è un padre con due figli 
	- cerco il predecessore/successore di `u` con AL PIÙ un figlio
	- scambio `u` e `pred/succ` 
	- mi trovo nel caso `1` o `2`
	![[Screenshot 2024-11-24 181445.png]]


## PROBLEMA DEL BST
Effettivamente tutte le operazioni costano quanto l'altezza `h` dell'albero$$O(h)$$ma abbiamo due casi importanti
- **BST BILANCIATO**
	![[Pasted image 20241124182055.png]]dove $$h = O(log(n))$$
- **BST LINEARIZZATO**
	![[Senza titolo.png]]dove $$h = O(n)$$


# AVL: soluzione al BST
Con l'AVL facciamo in modo di avere un altezza sempre pari a $O(log(n))$

Introduciamo il fattore di bilanciamento $\beta(v)$ che viene inserito in ogni nodo e si calcola come $$\text{altezza sottoalbero sinistro} - \text{altezza sottoalbero destro}$$
>[!example] Un albero è bilanciato se ha $|\beta(v)| \le 1$ per ogni `v` 

ESEMPIO
![[Pasted image 20241126130620.png|center]]


### Numero nodi in alberi di fibonacci
![[Pasted image 20241126131242.png]]In pratica, nel lemma:
- Parto da una $T_h$
- posso calcolare il numero di nodi di $T_h$ facendo $$numero \ nodi (n_h)= F_{h + 3} - 1$$Infatti, ad esempio, con $T_4$, ho $$n_{h} = F_{7} - 1 = 13 - 1 = 12$$
>[!tip] LUCATA
>Gli alberi di Fibonacci $F_{h}$ sono il **CASO LIMITE** di un AVL di altezza h.

### Dimostrazione altezza AVL
![[Pasted image 20241126131313.png]]Riscriviamo la formula di prima $$n_{h} = F_{h + 3} - 1$$
Sapendo che $$F_{k} = \Theta(\phi^{k})$$e che $\phi = 1.618...$ 
Allora possiamo scrivere che $$n_{h} = \Theta(\phi^{h +3}) - 1 = \Theta(\phi^{h})$$
Troviamo $h$ $$\phi^{h} = n_{h} \ \implies \ h = log_{\phi}(n_{h})$$
Sappiamo che $n_{h} \le n$ , perché il numero MINIMO di nodi ($n_h$) per avere l'albero di una certa altezza sarà sempre $\le$ del numero MASSIMO di nodi (per la stessa altezza). 
Per esempio, $T_3$ ha come numero minimo di nodi $7$, però io posso arrivare a scriverne anche $15$ per avere sempre altezza $3$.

Sapendo questo, allora $$h = \Theta(log(n_{h})) = O(log(n))$$

### Operazioni AVL
#### Search
Identica a BST

#### Insert e Delete
Quando parliamo di AVL, facciamo riferimento al bilanciamento dell'intero albero.
Un AVL bilanciato, a seguito di un inserimento o di un'eliminazione, potrebbe avere un nodo con un fattore di bilanciamento $|\beta(v)| = 2$, rendendo l'intero albero sbilanciato.

Questo nodo viene chiamato **nodo critico** e per bilanciarlo vengono eseguite delle rotazioni.
Abbiamo quattro casi fondamentali

| Nome caso | $\beta(v)$ | Situazione                                                            | Cosa fai                                |
| --------- | ---------- | --------------------------------------------------------------------- | --------------------------------------- |
| **SS**    | $+2$       | Il problema si trova nel **sottoalbero sinistro del figlio sinistro** | Rotazione semplice a **destra**         |
| **DD**    | $-2$       | Il problema si trova **sottoalbero destro del figlio destro**         | Rotazione semplice a **sinistra**       |
| **SD**    | $+2$       | Il problema si trova nel **sottoalbero destro del figlio sinistro**   | Rotazione doppia: **sinistra → destra** |
| **DS**    | $-2$       | Nodo inserito nel **sottoalbero sinistro del figlio destro**          | Rotazione doppia: **destra → sinistra** |

#### CASO SS
![[Pasted image 20241127175903.png|center]]
Devo eseguire una rotazione semplice a `sx` partendo dalla radice `v`

Abbiamo due sottocasi (derivanti dall'altezza effettiva di $T_{2}$)
1. L'altezza di $T_{2}$ è h -> post rotazione l'albero avrà altezza $h+2$ (non più $h+3$)
	![[Pasted image 20241127181325.png]]

2. L'altezza di $T_{2}$ è $h+1$ -> l'altezza dell'albero post rotazione non cambia
	![[Pasted image 20241127181523.png]]

>[!definizione] Osservazioni
>- L'inserimento di un elemento nell'AVL (ossia l'aggiunta di una foglia ad un albero bilanciato), causa solo il sottocaso `1` (altrimenti vorrebbe dire che l'AVL era già sbilanciato). 
>- La cancellazione di un elemento dall'AVL (che necessariamente fa diminuire l'altezza di qualche sottoalbero) può causare sia `1` che `2`.


#### CASO SD
![[Pasted image 20241127183505.png|center]]
Nota come qui so che il problema me lo da il sottoalbero `dx` di `z` perché $$\beta(z) = -1$$e quindi so che `dx(z)` ha un'altezza maggiore a `sx(z)`

Qui applichiamo una doppia rotazione
- a `sx` sul nodo `z` (figlio sinistro di nodo critico)
- a `dx` sul nodo `v` (nodo critico)
![[Pasted image 20241127184654.png]]
>[!definizione] Osservazione
Il caso SD può essere provocato sia da inserimenti (in $T_2$ o $T_3$), sia da cancellazioni che abbassano di $1$ l'altezza di $T_4$.

#### Insert
- Inserisco come nel BST
- Ricalcolo il fattore di bilanciamento
- Se è presente un nodo critico `v`, eseguo una rotazione su `v`
###### ESEMPIO: insert(10, e)
![[ezgif.com-speed (5).gif]]

#### Delete
- Elimino come in BST (trovando predecessore/successore)
- Ricalcolo il fattore di bilanciamento
- Se ho un nodo critico eseguo una rotazione (potrebbe essere necessario anche una doppia rotazione)
###### ESEMPIO: delete(18)
![[slides_animation_slower-ezgif.com-crop.gif|center]]

>[!tip] Nota una cosa
>L'eliminazione può portare a casi in cui bisogna fare delle rotazioni ANCHE negli antenati del nodo critico iniziale.
>Questo vuol dire che bisogna fare $O(log(n))$ rotazioni MA ogni rotazione ha costo costante quindi non intacca nel costo totale.
##### Dettagli importanti
![[Pasted image 20250628161826.png]]


--- 

# Code con priorità
Un insieme `S` di `n` elementi utilizzato per mantenere ordinati questi elementi secondo delle proprietà.

#### Operazioni possibili
- `findMin() -> elem`
- `insert(elem e, chiave k)`
- `delete (elem e)`
- `deleteMin()`

OPERAZIONI AGGIUNTIVE
- `increaseKey(elem e, chiave d)`
	- incrementa della quantità `d` la chiave dell'elemento `e` in `S`
- `decreaseKey(elem e, chiave d)`
	- stessa cosa di prima ma decrementa
- `merge(CodaPriorità c_1, CodePriorità c_2) -> CodaPriorità`
	- restituisce una nuova coda con priorità $c_{3} = c_{1} \cup c_{2}$ 

#### Costo operazioni
![[Screenshot 2024-12-03 184218.png]]
### Come posso avere costi migliori?
Abbiamo tre implementazioni efficienti.

## D-HEAP
È un albero `d-ario` con le seguenti proprietà
- completo fino al PENULTIMO livello (struttura rafforzata)
- ogni nodo `v` ha un `elem(v)`  e `chiave(v)` prese da un dominio ordinato
- SI BASA SUL MIN-HEAP, quindi $$\text{chiave padre} \le \text{chiave figli}$$
Da questo deriva che
- il `min` si trova nella radice -> `findMin` = $O(1)$ 
- con `n` nodi -> $h = \Theta(log_d(n))$
- può essere rappresentato tramite un vettore posizionale


#### Operazioni su un D-HEAP
##### Muovi in alto
Prende un nodo e lo sposta in alto, mantenendo le proprietà (lo faccio quando inserisco/rimuovo elementi).
```scss
muovi_in_alto(v)
	while(v != radice e chiave(v) < chiave(padre(v))) do
		scambia di posto v e padre(v)
```
$$T(n) = O(log_{d}(n))$$
##### Muovi in basso
Stessa cosa ma spostando in basso
```scss
muovi_in_basso(v)
	repeat
		sia u il figlio di v con minima chiave(u), se esiste
		if(v non ha figli o chiave(v) <= chiave(u)) break
		scambia di posto v e u in T
```
$$T(n) = O(log_d(n))$$

#### Operazioni 
#### FindMin
```scss
findMin()
	"restituisce l'elemento nella radice di T"
```
$$T(n) = O(1)$$

#### Insert
Inserisco un elemento nella foglia più a sinistra disponibile e, se necessario, eseguo `muovi_in_alto`
###### Insert(e, 8)
![[ezgif.com-crop.gif]]$$T(n) \ = \ O(1) \ + \ O(log_{d}(n)) \ = \ O(log_{d}(n))$$

#### Delete
Scambio il nodo con la foglia più a destra
- elimino il nodo (che ora è una foglia)
- eseguo un `muovi_in_basso` sulla foglia spostata
###### delete(8)
![[ezgif.com-speed (11).gif]]$$T(n) \ = \ O(1) \ + \ O(log_{d}(n)) \ = \ O(log_{d}(n))$$
###### delete(17)
![[ezgif.com-speed (10) 1.gif]]

#### Decrease Key
Prendo l'elemento, decremento la sua chiave e eseguo `muovi_in_alto`
![[pages_32_to_36_looping-ezgif.com-speed.gif]]$$T(n) \ = \ O(1) \ + \ O(log_{d}(n)) \ = \ O(log_{d}(n))$$

#### Increase Key
Incremento ed eseguo `muovi_in_basso`
![[increment key.gif]]

#### Merge
Il merge su un d-heap è molto costoso.

Abbiamo due approcci
- **Costruisco da 0** -> elimino le due strutture e ne creo una nuova da 0 (la utilizzo solo se non posso eseguire la seconda)
- **Inserimenti ripetuti** -> inserisco la coda più piccola in quella più grande (eseguendo `k` inserimenti)

#### Costruzione da 0 (Generalizzazione di Heapify)
- Unisco i due d-heap in un unico d-heap 
- rendo ricorsivamente i sottoalberi degli heap con Heapify
- eseguo `muovi_in_basso` sulla radice

![[Pasted image 20241204183849.png]]
- $d \ T(\frac n d)$ è l'Heapify fatto su `d` figli
- $O(d \ log_{d}(n))$ è il `muoviBasso` fatto sulla radice

#### Inserimenti ripetuti
Inserisco uno ad uno gli elementi della coda con priorità più piccola nella coda con priorità più grande (`k` volte).
![[Pasted image 20241204184224.png]]
##### RIEPILOGO
|                                         | Find Min | Insert        | Delete            | DelMin            | Incr. Key         | Decr. Key     | Merge |
| --------------------------------------- | -------- | ------------- | ----------------- | ----------------- | ----------------- | ------------- | ----- |
| **Array non ord.**                      | Θ(n)     | O(1)          | O(1)              | Θ(n)              | O(1)              | O(1)          | O(n)  |
| **Array ordinato**                      | O(1)     | O(n)          | O(n)              | O(1)              | O(n)              | O(n)          | O(n)  |
| **Lista non ordinata**                  | Θ(n)     | O(1)          | O(1)              | Θ(n)              | O(1)              | O(1)          | O(1)  |
| **Lista ordinata**                      | O(1)     | O(n)          | O(1)              | O(1)              | O(n)              | O(n)          | O(n)  |
| <font color="#ff0000">**d-Heap**</font> | O(1)     | $O(log_d(n))$ | $O(d \ log_d(n))$ | $O(d \ log_d(n))$ | $O(d \ log_d(n))$ | $O(log_d(n))$ | O(n)  |


# ALBERI BINOMIALI
Un albero binomiale $B_{i}$ è definito ricorsivamente in questo modo
- $B_{0}$ ha solo la radice
- $B_{i+1}$ è ottenuto fondendo tra loro due $B_{i}$, ponendo la radice dell'uno come figlio della radice dell'altro
![[Pasted image 20241204185758.png]]
#### Proprietà strutturali
1. In $B_i$, la $i$ è il numero massimo di figli (la `d` di prima)
2. Il numero totale di nodi: $2^i$
3. L'altezza: $H(n) = h = log_{2}(n)$
4. Grado della radice: $D(n) = log_{2}(n)$
5. Ogni Albero $B_i$ avrà come figli i sottoalberi $B_0,...,B_{i-1})$ 

# HEAP BINOMIALI
Un heap binomiali è una foresta di alberi binomiali con le seguenti proprietà
- nella foresta è presente AL MASSIMO un $B_{i}$
- ogni nodo ha un elemento e una chiave
- ogni HEAP è un MIN-HEAP, quindi con $chiave(padre) \le chiave(figli)$

![[Pasted image 20241204191854.png]]

##### Capire quanti alberi devo avere nella foresta in base ai nodi
- Prendo `n` (il numero di nodi)
- lo codifico in binario
- vedo in che posizione si trovano gli `1` -> per ogni posizione `i` avente `1` avrò un $B_{i}$.

Esempio: `n` = 13 $$13 = 1101$$quindi
- $B_{0}$ -> SI
- $B_{1}$ -> NO
- $B_{2}$ -> SI
- $B_{3}$ -> SI
Rappresentazione di `n` = 13
![[Pasted image 20241204192113.png]]

Da questo consegue che in un heap binomiale ci sono AL PIÙ $\lceil log(n) \rceil$ alberi binomiali, ciascuno con grado e altezza $O(log(n))$

### Procedure
#### Ristruttura
Quando ho una struttura che vorrei fosse un heap binomiale MA NON RISPETTA LA PROPRIETÀ DI UNICITÀ (un solo $B_{i}$), posso usare la ristruttura scorrendo da `sx` a `dx`

```scss
ristruttura()
	i = 0
	
	while(esistono ancora due B_i) do
		fondi i due B_i costruendo un B_{i+1} 
		mettendo la radice max come figlio della radice min
		i++
```
$$T(n)$$
###### ESEMPIO
Voglio formare un heap binomiale ma ho due $B_0$ , eseguo `ristruttura(H)`
![[Pasted image 20241204194802.png]]

#### Operazioni
- `findMin()`
	- scorre gli heap controllando le varie radici e restituisce la `min`

- `insert(elem e, chiave k)`
	- inserisce l'elemento come un $B_{0}$ e esegue la ristruttura se serve

- `deleteMin()`
	- elimina la radice `min`
	- i sottoalberi destri diventano tanti nuovi $B$ -> esegue ristruttura
	![[Pasted image 20241204195704.png]]![[Pasted image 20241204195724.png]]

- `decreaseKey(elem e, chiave d)`
	- decrementa di `d` la chiave del nodo `v` contenente l'elemento `e`
	- eseguo se serve `muovi_in_alto`
	![[Pasted image 20241204200117.png]]![[Pasted image 20241204200131.png]]

- `delete(elem e)`
	- eseguo un `decreaseKey(e, -inf)` -> così rendo quel nodo talmente piccolo che diventa la radice del suo albero e anche il `min` dell'Heap Binomiale
	- eseguo un `deleteMin()`

- `increaseKey(elem e, chiave d)`
	- chiama `delete(e)` e poi fa `insert(e, k+d)`, dove `k` è la chiave originale di `e`

- `merge(CodaPri.c1, CodaPri.c2) -> CodaPri`
	- unisce `c1` e `c2` in un nuovo heap binomiale `c3` e poi fa ristruttura per evitare doppioni
	![[Pasted image 20241204201025.png]]

>[!lemma] Tutte le operazioni hanno costo $$T(n) = O(log(n))$$ e durante la ristrutturazione esistono AL PIÙ tre $B_i$ per ogni $i \ge 0$

#### HEAP FIBONACCI
Una struttura dati **avanzata** per implementare una **coda con priorità**, progettata da Tarjan.
> L’idea è: “**rimando le operazioni costose** (come ribilanciamenti) e le faccio solo **quando servono davvero**”.

|                  | Find Min    | Insert      | Delete       | DelMin       | IncrKey      | DecrKey     | Merge       |
| ---------------- | ----------- | ----------- | ------------ | ------------ | ------------ | ----------- | ----------- |
| **d-Heap**       | $O(1)$      | $O(log(n))$ | $O(log(n))$  | $O(log(n))$  | $O(log(n))$  | $O(log(n))$ | $O(n)$      |
| **Heap binom.**  | $O(log(n))$ | $O(log(n))$ | $O(log(n))$  | $O(log(n))$  | $O(log(n))$  | $O(log(n))$ | $O(log(n))$ |
| **Heap fibona.** | $O(1)$      | $O(1)$      | $O(log(n))*$ | $O(log(n))*$ | $O(log(n))*$ | $O(1)*$     | $O(1)$      |
Gli asterischi indicano che quella non è la complessità nel caso peggiore ma la complessità in senso ammortizzato (solo intuizione).

### 💡 **Costo ammortizzato – che significa?**
È come dire:
> “Una singola operazione potrebbe costare tanto, ma se ne faccio tante, **in media** costano poco”.

Serve per valutare le strutture in **scenari reali**, dove conta **il costo totale** su molte operazioni, non il caso peggiore singolo.


---

# Grafi
I **grafi** sono strutture matematiche usate per rappresentare insiemi di oggetti (i **nodi**, o **vertici**) collegati tra loro da **relazioni** (chiamate **archi**).

Si distunguono in
- NON ORIENTATO -> $G = (V, E)$
- DIRETTO -> $D = (V, A)$
- PESATO -> $G = (V, E, w)$

#### Terminologia
**GRAFO NON DIRETTO**
![[Pasted image 20241205113555.png|center]]
- $G = (V, E)$, grafo non diretto
- $n = |V|$ -> numero di vertici
- $m = |E|$ -> numero di archi
- $(u, v)$ -> è un arco indicente ai due vertici e questi sono detti **estremi**
- $\delta(u)$ -> è il grado di un vertice e indica quanti archi sono associati a quel vertice
- Grado di G -> $max_{v \in V}\{\delta(v)\}$ 

**GRAFO DIRETTO**
![[Pasted image 20241205114725.png|center]]
- Primi quattro punti identici
- $\delta_{in}(u)$ -> grado ENTRANTE in `u`, ossia gli archi che entrano in `u`
- $\delta_{out}(u)$ -> grado USCENTE in `u`, ossia gli archi che escono da `u`
- Grado ENTRANTE di G -> $max_{v \in V}\{\delta_{in}(v)\}$ 
- Grado USCENTE di G -> $max_{v \in V}\{\delta_{out}(v)\}$ 

#### Altra terminologia
- **cammino** -> sequenza di nodi connessa da archi
- **lunghezza di un cammino** -> `#` di archi del cammino
- **distanza** -> lunghezza del più cammino tra due vertici
- **G è connesso** -> esiste un cammino per ogni coppia di vertici
- **ciclo** -> se esiste un cammino che parte da un nodo e ritorna in quel nodo
- **diametro** -> massima distanza fra due nodi


### Quanti archi può avere un grafo di n nodi?
- SCONNESSO -> 0
- CONNESSO E ACICLICO -> $m = \Omega(n)$ (ha almeno $n-1$ archi)
- COMPLETO -> $O(n^2)$

>[!lemma] Teorema
>Sia $T = (V,E)$ un albero; allora $|E| = |V| - 1$

>[!lemma] Definizione
>Dato un **grafo G**, un **ciclo** (rispettivamente un cammino) **Euleriano** è un ciclo (rispettivamente un cammino non chiuso) di G che passa per tutti gli archi di G **una e una sola volta**.



# METODI PER RAPPRESENTARE I GRAFI
#### Matrici $N \times N$
![[Pasted image 20241213164713.png|center|200]]
Uso delle variabili booleane e inserisco $1$ negli incroci in cui ho collegamenti.
	Occupa spazio $O(n^2)$.

#### LISTE DI ADIACENZA
![[Pasted image 20241213164753.png|center|200]]Uso una lista collegata per tenere conto dei collegamenti
	Occupa spazio $O(n + m)$, dove $n$ è il numero di nodi e $m$ è il numero di archi


# ALGORITMI DI VISITA DI UN GRAFO
### VISITA IN AMPIEZZA (BFS)
>[!lemma] FUNZIONAMENTO
>Dato un **grafo G** (non pesato) e un **nodo s**, trova tutte le **distanze** (o cammini minimi) *da s verso OGNI ALTRO nodo v*

##### PSEUDOCODICE
- Utilizzo una coda -> gli elementi vengono messi in fondo
- Estraggo ogni volta il nodo in cima, lo pongo come figlio del nodo presente nell'Albero T
```scss
BFS(vertice s)
	T <- albero formato solo da s
	C <- coda
	
	marca il vertice s nel grafo; dist(s) <- 0
	C.enqueue(s)
	
	while(not C.isEmpty()) do
		u <- C.dequeue()
		for each (arco (u,v) in G) do
			if (v non è marcato) then
				C.enqueue(v)
				marca il verticev; dist(v) <- dist(u) + 1 
				rendi u il padre di v in T
	
	return T
```
###### ESEMPIO VISIVO ![[ezgif.com-speed (12).gif|center|400]]
###### ALBERO CONSEGUENTE
![[Pasted image 20241213175140.png|center|300]]

##### COSTO BFS
***MATRICE***
![[Pasted image 20241213175508.png]]
>[!question]- Spiegazione dell $O(n^{2})$ 
>![[Pasted image 20250603102635.png]]

***LISTA***
![[Pasted image 20241213180027.png]]
	Se il grafo è connesso io so che il numero di `archi` (**m**) è maggiore o al massimo uguale al numero di `nodi - 1` (**n-1**) $$m \ge n-1$$e quindi $$O(m+n) = O(m)$$
	Se però il grafo è completamente connesso, $$m \le \frac {n(n-1)} 2$$ allora $$O(m+n) = O(n^2)$$
Quindi
- SE $m = o(n^2)$ è sempre meglio utilizzare la liste
- SE $m = O(n^2)$ allora utilizza le matrici (perché la ricerca di un arco costa $O(1)$!!)

>[!lemma] Teorema
![[Pasted image 20241213181400.png]]
Quindi in pratica, il **livello di un qualsiasi nodo v** nell'albero BFS CORRISPONDE al **cammino minimo dal nodo v alla radice s**.


### VISITA IN PROFONDITÀ (DFS)
La visita in profondità è un algoritmo di esplorazione dei grafi che procede esplorando ogni cammino in profondità prima di tornare indietro e visitare altre strade.
###### VERSIONE RICORSIVA
```scss
DFSricorsiva(v)
	marca e visita il vertice v 
	for each (arco(v, w)) do 
		aggiungi arco (v, w) a T
		DFSricorsiva(w, T)

CHIAMATA(s, T)
	T <- albero vuoto
	DFSricorsiva(s)
	return T
```

##### Considerazioni
![[Pasted image 20241213185748.png]]

#### Altra utilità per le DFS
##### DFS con il clock
POsso utilizziare una variabile `clock` per tenere traccia 
- di quando un nodo viene scoperto (`pre`)
- di quando un nodo viene abbandonato (`post`)

```scss
DFS(v, T, clock)
	marca e visita il vertice V
	pre(v) = clock
	clock++
	
	for each (arco (v, w)) do
		if (w non è marcato) then
			aggiungi (v, w) a T
			DFS(w, T, clock)
	
	post(v) = clock
	clock++


ChiamataDFS(s)
	T <- albero vuoto
	clock  = 1
	ChiamataDFS(s, T, clock)
	return T
```

>[!question] Perché il clock lo incremento sia a `riga 3` e `riga 9`
>- `riga 3` la uso per far sì che tutti i `pre` siano diversi tra loro
>- `riga 9` la uso per far sì che sia i `pre` che i `post` siano diversi

###### ESEMPIO
![[DFS con clock.png]]

#### Cosa fare quando ho dei nodi scollegati dal resto?
![[Pasted image 20241215115840.png|center|600]]

Posso creare una foresta di alberi, in cui inserire tutti gli alberi che creo
```scss
ForestaDFS(grafo G)
	for each nodo v do
		imposta v come non marcato
	
	clock = 1
	F <- foresta vuota
	
	for each nodo v do
		if(v non è marcato) 
			T <- albero vuoto
			DFS(v, T)   // l'algoritmo che hai visto sopra
			aggiungi T a F
	
	return F
```

### Spiegazione 
- nel `for each` se `v` non è marcato vuol dire che 
	- ho appena iniziato il `for each`
	- oppure che dopo la chiamata DFS non ho visitato quel nodo -> si trova in un altro nodo
	 SCOLLEGATO dall'albero appena visitato

Se sono nel secondo caso, allora creerò un nuovo albero, lo riempirò e lo aggiungerò a T.

### Proprietà 
1. Per ogni coppia di nodi **u** e **v**, abbiamo rispettivamente
	- `[pre(u), post(u)]`
	- `[pre(v), post(v)]`
	e questi possono essere disgiunti oppure uno è contenuto nell'altro

2. **u** è antenato di v nell'albero DFS, se $$pre(u) < pre(v) < post(v) < post(u)$$(nella foto sopra abbiamo, per esempio, `A antenato di G`).

3. usiamo i tempi di visita per riconoscere un tipo generico di arco (u,v) nel grafico
	![[Pasted image 20241215124717.png|center]]
	**IN AVANTI** = `(A, E)`,...
	**ALL'INDIETRO** = `(F, B)`,...
	**TRASVERSALI** (necessitano un collegamento) = $post(v) < pre(u)$ = `(H, G), (D, H)`


## Come riconoscere la presenza di un ciclo in un grafo diretto
Eseguo una **DFS** e controllo se c'è un **arco all'indietro** -> se c'è allora abbiamo un ciclo.

>[!lemma] DEFINIZIONE: DAG
>Un **grafo diretto aciclico** (**DAG**) è un grafo diretto senza cicli (diretti)
>
>![[DAG.png|center]]
>
>N.B.: sorgente e pozzo devono per forza esserci, altrimenti avrei un ciclo (es. se 7 non fosse un pozzo avrei un ciclo.)

>[!lemma] DEFINIZIONE: Ordinamento topologico
>Un ordinamento topologico di un grafo diretto $G=(V,E)$ è una funzione biettiva $$\sigma: V → {1,2,..,n}$$ tale che per ogni arco $(u,v) \in E$, $$\sigma(u) < \sigma(v)$$
>In pratica se esiste un collegamento tra due nodi, metto prima il nodo che ha l'arco OUT e poi quello che ha l'arco IN.
>
>Ovviamente metto la sorgente all'inizio e il pozzo alla fine.
>
>IL DAG DI PRIMA SI SCRIVEREBBE COSÌ
>
>![[Pasted image 20241215145439.png|center]]


#### N.B.: solo i grafi DAG ammettono un ordinamento topologico
Questo perché, se la funzione biettiva prevedere che $$\sigma(u) < \sigma(v)$$ per ogni arco $(u, v)$, se io ho un ciclo $<v_{0}, v_{1}, ..., v_{k}=v_{0}>$ avrò una situazione del genere $$\sigma(v_{0}) < \sigma(v_{1}) < ... < \sigma(v_{k-1} < \sigma(v_{k}) = \sigma(v_{0})$$e questo vuol dire che $$\sigma(v_0)<\sigma(v_1) \ \ MA \ ANCHE \ \ \sigma(v_{k} = v_{0}) > \sigma(v_{k-1})$$il che è impossibile $\square$ 


#### Algoritmo per calcolare l'ordinamento topologico
Eseguo una DFS con il clock, non appena esco dal `for each`, il nodo prende il `post` e io lo inserisco nella con l'ordinamento.
In pratica, inserisco nella lista l'elemento con il `post` più basso ogni volta, e gli altri li inserisco sempre dalla cima.

```scss
OrdinamentoTopologico (grafo G)
	top = n; L <- Lista vuota
	chiama visita DFS ma
		quando ha finito di visitare un nodo v
			sigma(v) = top; top -= 1
		aggiungi v in testa a L
	return L e sigma
```

***COSTO*** $$\Theta(n+m)$$

#### Versione alternativa
Qui l'idea è
- costruisco un nuovo grafo $G^{'}$
- rimuovo da $G^{'}$ ogni volta il vertice che non ha archi entranti
- lo aggiungo alla lista (faccio `append`)
SE $G^{'}$ NON DIVENTA VUOTO, vuol dire che $G$ non è aciclico

```scss
OrdinamentoTopologico(grafo G)
	Ĝ <- G
	ord <- lista vuota di vertici
	
	while (esiste un vertice v senza archi entranti in Ĝ) do
		appendi v come ultimo elemento di Ĝ
		rimuovi v da Ĝ
	
	if (Ĝ non è diventato vuoto) then
		errore: G non è aciclico
	
	return ord
```


## COMPONENTI FORTEMENTE CONNESSE
Una componente fortemente connessa di un grafo G è un insieme massimale di vertici $C \subseteq V$ tale che per ogni coppia di nodi `u` e `v` -> `u` è raggiungibile da `v` e `v` è raggiungibile da `u`

> In pratica, se ho un ciclo tra due vertici ho una componente fortemente connessa tra quei vertici

![[Pasted image 20241215163305.png|center]]
- `A` è una componente fortemente connessa di sé stessa
- `B` e `E` sono una componente fortemente connessa

La cosa interessante è che il grafo originale non era un **DAG**, ma il grafo delle componenti connesse si.
![[Pasted image 20241215163409.png|center]]

#### Varie proprietà
1. Se eseguo una visita `DFS` a partire da `u`, questa termina solo quando ho finito di visitate tutti i nodi raggiungibili da `u`
>[!lemma] IDEA
>Quindi per costruire il grafo delle componenti fortemente connesse conviene far partire le `DFS` dalla componente pozzo, una volta finita la `DFS` "elimino" quella componente e ripeto.

2. Se `C` e `C'` sono due componenti e esiste un arco diretto `C -> C'`  allora il più alto valore di `post` di `C'` sarà più piccolo del più alto valore di `post` di `C`
	![[Pasted image 20241215170308.png|center|200]]
	e questo ha senso perché parto da `C` -> entro in `C'` -> esco da `C'` (ho il `post`) -> esco da `C` (ho il `post`)

3. La componente sorgente ha il `post` più alto

### Per trovare una componente pozzo dopo aver trovato una sorgente, INVERTIAMO TUTTI GLI ARCHI
L'idea qui è
- trovo la componente sorgente di `G` -> quella con il `post` più alto
- creo `G'` -> inverto gli archi 
- in `G'` eseguo `DFS` partendo dalla componente con il `post` più alto di `G`

###### CODICE
![[Pasted image 20250603114758.png|center|300]]

##### ESEMPIO VISIVO
![[Pasted image 20241215171028.png]]

>[!lemma] Perché è utile?
>Se io costruisco il mio grafo delle componenti connesse PARTENDO da una pozzo, io sono SICURO che non ha archi uscenti, quindi rimarrò confinato dentro quella componente.
>
>Questo vuol dire che io partendo dal pozzo sono sicuro di visitare quella componente nella sua completezza, senza rischiare di uscire fuori.


---

# Cammini minimi su grafi pesati
Se ho un grafo orientato pesato (orientato e non), la distanza tra due nodi è data dai pesi degli archi che passano per i due nodi.

Il cammino minimo qui è dato dal costo minimo degli archi presi in considerazione.

>[!tip] Non è per forza unico

>[!danger] NON ESISTE SEMPRE UN CAMMINO MINIMO TRA DUE NODI
>Potremmo avere due nodi che non sono collegati da nessun arco/insieme di archi, allora $$d(u, v) = +\infty$$
>
>Se ho un ciclo negativo tra due archi, potrei sfruttarlo per far diminuire la loro distanza, allora $$d(u, v) = -\infty$$
>E QUESTA SECONDA COSA NON VA BENE
>![[Pasted image 20241221153039.png]]

### Proprietà dei cammini minimi
>[!lemma] Ogni sottocammino di un cammino minimo è a sua volta un cammino minimo.
>
>Dimostrazione per assurdo: **cut & paste**
>![[Pasted image 20241221153352.png]]
>Scelgo, erroneamente, il cammino orizzontale per `u - v` come "minimo".
>Provo a verificare la proprietà di prima -> prendo due nodi `x` e `y` e controllo se il loro cammino è minimo -> NO perché ho un collegamento diretto.


### Disuguaglianza triangolare
$$\forall u, v, x \in V  \ \ \ \text{vale} \ \ \ d(u,v) \le d(u,x) + d(x, v)$$![[Pasted image 20241221155101.png|center]]
- Per i grafi non pesati vale sempre (basta fare BFS)
- Per i grafi pesati vale solo se prendo il cammino minimo (serve Dijsktra)


# SPT (albero dei cammini minimi)
T è un SPT con sorgente `s` di un grafo $G$ se
- T è un albero radicato in `s`
- per ogni $v \in V$ vale che $d_{T}(s, v) = d_{G}(s,v)$

#### SPT per grafi non pesati
Basta eseguire una `BFS`
![[PST = BFS.png|center|500]]

## SPT per grafi pesati: Dijsktra
Usiamo questo algoritmo per calcolare i cammini minimi a singola sorgente su grafi pesati MA TUTTI I PESI DEGLI ARCHI DEVONO ESSERE NON NEGATIVI $$\forall(u, v) \Rightarrow w(u,v) \ge 0$$

#### Approccio greedy
1. Inizialmente do a tutti i nodi delle stime per eccesso -> $D_{sv} = +\infty$
	Ossia pongo che la loro distanza dalla radice `s` sia infinito
	
2. L'unica stima esatta è quella della radice -> la distanza da sé stessa è 0 -> $D_{ss} = 0$
	
3. Ho un insieme `X` in cui inserisco solo i nodi con le stime esatte (quindi i nodi di cui so il cammino minimo) 
	Inizialmente `X = {s}`
	
4. Utilizzo una coda con priorità in cui, una volta visitato un nodo `u` (con la stima esatta, quindi messo in `X`), inserisco tutti i nodi che hanno archi entranti a partire da `u` e
	- Se la stima di un nodo `v` è $+\infty$ -> sto visitando quel nodo per la prima volta -> aggiorno la sua stima a $$D_{su} + w(u,v)$$
	- Se la stima è $\ne +\infty$ -> l'ho già visitato -> confronto la sua stima precedente $D_{sv}$ con la stima attuale $D_{su} + w(u,v)$ e se quest'ultima è **MINORE** allora aggiorno la sua stima con $$D_{su} + w(u,v)$$altrimenti rimane identica

5. Quando estraggo un nodo dalla coda con priorità, vuol dire che ha la stima esatta
	- Lo metto in `X` -> ogni volta in `X` viene inserito il nodo `u` appartenente a `V - X`
	- Lo metto in `T`, l'SPT che voglio creare, come figlio del nodo con la stima corretta precedente

##### Come funziona una stima non confermata?
La stima non confermata (presente nella coda) per un nodo $y \in V - X$ è data da $$D_{sy} = min\{D_{sx}+ w(x,y) : (x,y) \in E, \ x \in X\}$$

```scss
Dijsktra(G, s)
	X <- insieme vuoto
	T <- albero con radice in s
	coda con priorità C
	
	for each (vertice u in G) do
		D_su = +inf
	
	D_ss <- 0
	
	C.insert(s)
	
	while(not C isEmpty()) do
		u = C.deletemin()
		X = X ∪ {u}
		
		for each (arco (u, v) in G) do
			if (D_sv == +inf) then
				D_sv = D_su + w(u,v)
				rendi u padre di v in T
			else if (D_su + w(u,v) < D_sv) then
				C.decreaseKey(v, D_sv - (D_su + w(u,v)))
				D_sv = D_su + w(u, v)
				rendi u padre di v in T
	
	return T 
```

### Lemma per Dijsktra
>[!lemma] LEMMA
>Quando il nodo `v` viene estratto dalla coda con priorità vale:
>- $D_{sv} = d(s,v)$
>- il cammino da `s` a `v` nell'albero corrente ha costo $d(s,v)$ (cammino in G) (stima esatta)
>
>In pratica, quando un nodo esce dalla coda con priorità la sua stima è esatta.

DIMOSTRAZIONE PER ASSURDO
Ipotizziamo un caso del genere
	![[Pasted image 20241222173730.png]]

Sappiamo che la distanza da `s` a `v` è minore della distanza da `s` a `u` a `v`, $$D_{sv} < D_{su} + w(u, v)$$
Ora, ipotizziamo che Dijsktra abbiamo scelto la strada passante per `u`.

Riprendiamo la disuguaglianza triangolare (ogni sottocammino di un cammino minimo è un cammino minimo) e usiamola su $D_{sv}$
![[Screenshot 2024-12-22 174443.png]]
Introduciamo due nodi `x` e `y` per cui esiste un arco $(x, y) \in E$.
`x` si trova nell'insieme `X` (quindi ha stima esatta), proprio come `u`.
Ora, sapendo che l'arco $(x, v)$ ha sicuramente peso minore dell'arco $(u, v)$ (per la disuguaglianza triangolare) -> possiamo dire che Dijsktra avrebbe dovuto estrarre il nodo `y` dalla coda, e non `v`

QUINDI è un assurdo -> il lemma è vero

#### Complessità 
Escludendo le operazioni sulla coda con priorità il costo è $$O(m +n)$$
Sfruttando una coda con priorità con un Heap di Fibonacci (la migliore opzione), avremo come costi delle operazioni
- `Insert` = $O(1)$
- `DelMin`  = $O(log(n))^{*}$
- `DecKey` = $O(1)^{*}$  -> se utilizzo un puntatore diretto al nodo

Contando quindi che
- eseguo `n` insert -> $O(n)$
- eseguo `n` deleteMin -> $O(n \cdot log(n))^{*}$
- eseguo al più `m` decreaseKey -> $O(m)^{*}$

#### COSTO TOTALE
$$O(m+n) + O(m + n \cdot log(n)) \Rightarrow O(m + n \cdot log(n))$$
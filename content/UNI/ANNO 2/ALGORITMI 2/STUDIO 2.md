## GREEDY
- in ogni passo scegli la soluzione _migliore a breve termine_ (la scelta locale ottimale), sperando che porti anche alla soluzione globale ottimale.
### Interval scheduling
![[Pasted image 20250826114947.png|600]]

#### definizione
- Dati in input n intervalli: $I_1 ,...,I_n$
- $I_i$  ha tempo di inizio $S_i$  e tempo di fine $f_i$ 
- Due intervalli sono compatibili se non si sovrappongono 
- *Trovare il sottoinsieme di intervalli compatibili con cardinalità massima*
##### Soluzione greedy
- ordina  gli intervalli per tempo di **fine**
- Complessità: $O(n \ log n)$
![[Pasted image 20250826115641.png]]

##### *Teoremi*
![[Pasted image 20250828102548.png]]
![[Pasted image 20250828102600.png]]

### Interval partitioning
![[Pasted image 20250826115327.png]]


#### definizione
- Dati in input un insieme di $n$ intervalli (lezioni): $j_1,...,j_n$
- Lezione $j$ inizia a $s_j$ e finisce a $f_j$ 
- *Trovare il minimo numero di classi per schedulare tutte le lezioni affinché non ci siano due lezioni contemporaneamente nella stessa classe( ovvero le lezioni nella stessa classe devono essere compatibili)*
##### Soluzione greedy
- ordina per tempo di inizio $s_i$
- Complessità: $O(n \ log n)$
##### *Teoremi*
![[Pasted image 20250828103431.png]]
![[Pasted image 20250828103440.png]]

### Union Find Struttura dati
![[Pasted image 20250826120227.png|450]]

#### definizione
- Mantenere una collezione di insiemi disgiunti contenenti elementi distinti durante l’esecuzione di una sequenza di operazioni del seguente tipo: 
	- `Makeset(x)` = crea il nuovo insieme` x = {x}` di nome `x` 
	- `Union(A,B)` = unisce gli insiemi `A, B` in un unico insieme di nome A (distrugge quelli vecchi) 
	- `Find(x)` = restituisce il nome dell’insieme che contiene l’elemento `x` (si suppone di accedere direttamente all’elemento `x`)
### QuickFind
![[Pasted image 20250826120456.png]]

Usiamo una **foresta di alberi** di altezza 1 per rappresentare gli insiemi disgiunti. In ogni albero: 
- *Radice = nome dell’insieme*
- *Foglie = elementi ( incluso l’elemento rappresentativo, il cui valore è nella radice e da il nome all’insieme stesso)*
##### Implementazione delle varie operazioni
- `Makeset(elem e)` $T(n) = O(1)$
	- Crea un albero composto da due nodi: una radice e una foglia. Memorizza e sia nella foglia che nella radice come nome dell’albero
- `Union(name a, name b)` $T(n) = O(n)$ 
	- Sostituisce tutti i puntatori delle foglie di B alla radice di B con puntatori alla radice di A. cancella la vecchia radice di B.
- `Find(elem e) --> name` $T(n) = O(1)$
	- Accede alla foglia x corrispondente all’elemento e. da tale nodo segue il puntatore al padre che è la radice dell’albero e restituisce il nome memorizzato in tale radice


### QuickFind bilanciato
>[!bug] troppi cambi di puntatori con troppe union fanno venire un costo complessivo di $O(n^2)$


![[Pasted image 20250826121503.png|250]]
- Union by size
	- Nell'unione degli insiemi A e B attacchiamo  gli elementi dell’insieme con cardinalità minore a quello di cardinalità maggiore e se necessario modifichiamo la radice dell’albero ottenuto
	- si ottiene complessità $T_{amm}=O(log \ n)$ 
##### *Teoremi*
![[Pasted image 20250828103536.png]]
![[Pasted image 20250828103545.png]]


### QuickUnion
![[Pasted image 20250826122050.png]]
#### definizione
Usiamo una foresta di alberi di altezza anche maggiore di 1 per rappresentare gli insiemi disgiunti. In ogni albero: 
- Radice = elemento rappresentativo dell’insieme 
- Rimanenti nodi = altri elementi( escluso l’elemento nella radice)
##### Implementazione delle varie operazioni
- `Makeset(x`) $= O(1)$
- `Union(A,B)` $= O(1)$
- `Find(x)` $= O(n)$
#### QuickUnion con Union-By-Size
![[Pasted image 20250826122247.png]]

- la find costa $O(n)$ per risolverlo applichiamo l'euristica *UBS*
Nell'unione degli insiemi A e B, rendiamo la radice dell’albero con meno nodi figlia della radice dell’albero con più nodi e cambiamo il nome se necessario 
- L'operazione find richiede tempo $O(log n)$
#### QuickUnion con Union-By-Size+ Compressione dei Cammini
![[Pasted image 20250826122321.png]]
- Quando eseguo find e attraverso il cammino da x alla radice, comprimo il cammino, ovvero rendo tutti i nodi del cammino figli della radice
### Minimum spanning tree
![[Pasted image 20250826122636.png]]
#### definizione
- Dato un grafo connesso e non orientato $G=(V,E,W)$, pesato sugli archi. 
- un MST è un sottoinsieme di archi $T \subseteq E$ tale che ci sia
	- uno spanning ovvero un albero (V,T) connesso e aciclico che include tutti i nodi di V
	- e un minimum ovvero il peso totale, ovvero la sommatoria di tutti gli archi di T sia minimizzata
##### definizioni
- *Ciclo*: set di archi della seguente forma:  $a-b,b-c,...,y-z,z-a$
- *Cut*: Partizione sui vertici $V$ che forma due insiemi disgiunti $S$ e  $V\textbackslash S$
- *Cutset*: associato a un taglio $S$ abbiamo un cutset $D$ che è un sottoinsieme di archi con esattamente un nodo in $S$  e l'altro in $V\textbackslash S$ 
#### Proprietà
- 1. Se $G$ ha <font color="#4bacc6">pesi distinti</font> allora esiste un <font color="#4bacc6">unico MST</font>
- 2. Cycle-cut intersection
	- L'intersezione tra un cutset e un ciclo ha cardinalità pari
	- Il motivo è **geometrico**: un ciclo non può “entrare” in una parte del grafo senza poi “uscire” lo stesso numero di volte, altrimenti non riuscirebbe a richiudersi.
- 3. Cut property
	- Sia $S$ un qualunque taglio e sia $e$ l’arco del cutset dal costo minimo rispetto agli archi che attraversano quel taglio 
		- *Allora esiste un MST che contiene e*
- 4. Cycle property
	- Sia $C$ un qualsiasi ciclo  e sia $f$ l’arco appartenente al ciclo di peso massimo. rispetto agli archi che appartengono a quel ciclo
		- *Allora esiste un MST che non contiene f*
##### *Teoremi*
![[Pasted image 20250828103619.png]]
![[Pasted image 20250828103629.png]]

### Kruskal
- algoritmo che risolve MST
- si basa sulla  cycle property
#### definizione
- Inizia con $T= \varnothing$ , considera gli archi in ordine crescente di peso, viene inserito l’arco $e$ a $T$ se non genera un ciclo 
- Un implementazione efficiente di questo algoritmo utilizza la UnionFind
- Funziona ordinando tutti gli archi in ordine crescente di peso e vengono aggiunti uno alla volta se non creano cicli.
- Qui entra in gioco la **Cycle Property**: se un arco è il più pesante in un ciclo, non serve prenderlo. Kruskal infatti “scarta” implicitamente questi archi perché, quando un arco formerebbe un ciclo, non lo aggiunge.
##### Soluzione greedy
- tempo $O(m\ log \ n)$
![[Pasted image 20250826151632.png]]
##### *Teoremi*
![[Pasted image 20250828103647.png]]
![[Pasted image 20250828103656.png]]
![[Pasted image 20250828103714.png]]
#### Correttezza di Kruskal
- **Cut property**
    - Dato un qualsiasi cut (partizione dei vertici in due insiemi), l’arco di peso minimo che attraversa quel cut appartiene a _tutti_ gli MST.
    - Quindi, se prendiamo gli archi in ordine crescente, ogni volta che troviamo il più piccolo che connette due componenti diverse (cioè non crea ciclo), stiamo proprio scegliendo un “arco minimo di un certo cut”.
    - Questo garantisce che quell’arco deve stare in almeno un MST → la scelta è sempre “sicura”.
        
- **Cycle property**
    - In un ciclo, l’arco di peso massimo **non appartiene a nessun MST**.
    - Quindi, se durante l’algoritmo troviamo che un arco crea un ciclo, essendo l’ultimo che stiamo considerando (quello di peso maggiore nel ciclo, dato che stiamo andando in ordine crescente), possiamo scartarlo con certezza.

- ogni arco aggiunto è giustificato dalla **cut property**,
- ogni arco scartato è giustificato dalla **cycle property**.

### Prim
#### definizione
- Inizia da un nodo radice $s$ e fa crescere un albero $T$ in modo greedy da $s$ verso l’esterno, ad ogni passo aggiunge a $T$ l’arco meno costoso che ha esattamente un estremo in $T$
##### Soluzione greedy
- Mantiene l’insieme dei nodi esplorati $S$ 
- Usa una coda con priorità per mantenere i nodi inesplorati 
- Per ogni nodo inesplorato la priorità è l’attachment $cost \ a[v] =$ costo dell’arco meno costoso incidente a $v$ che ha l’altro estremo in $S$
	- Parte da un nodo e costruisce l’albero estendendolo passo passo.
	- Ad ogni passo sceglie l’arco **più leggero che attraversa il taglio** tra i vertici già inclusi e quelli ancora fuori.
	- Qui si usa la **Cut Property**: l’arco più leggero che attraversa un taglio appartiene sempre a qualche MST, quindi è sicuro includerlo.
![[Pasted image 20250826152512.png]]
- $O(m+nlogn)$ 

## Programmazione dinamica
- dividi il problema in _sotto-problemi sovrapposti_ e usa i risultati salvati (memoization/tabulation) per evitare ricalcoli.
#### Independent Set
![[Pasted image 20250826154450.png|400]]
#### definizione
- Dato un cammino $G$ di $n$ nodi. Ogni nodo $v_i$ ha peso $w_i$
- Trovare un insieme indipendente di peso massimo ovvero un insieme $S$ tale che: 
	- 1. $S$ è un insieme indipendente  
	- 2. $w(S) = somma$ dei pesi dei nodi in $S$, è più grande possibile
- Un insieme indipendente di $G$ è un sottoinsieme di nodi che non contiene due nodi adiacenti, ovvero per ogni coppia di nodi del insieme i due nodi non sono collegati da un arco.
##### Soluzione dinamica
- $G_j$ : sotto-cammino composto dai primi $j$ vertici di $G$
- Sotto-problema $j$ : calcolare il peso del miglior insieme indipendente per $G_j$
	- $OPT[ j ]$ : valore della soluzione sotto-problema $j$, ovvero peso dell’insieme indipendente di peso massimo di $G_j$ 
	- $OPT[1] = w_1 ; OPT[2] = max\{ w_1 , w_2\}$
	- $OPT[j] = max\{ OPT[ j-1], w_j+OPT[ j-2]\}$

### Interval scheduling con peso
![[Pasted image 20250826160255.png]]

#### definizione
- Dati $n$ intervalli chiamati job $j_1,...,j_n$ 
- Job $j$  inizia a $s_j$ e finisce a $f_j$ , e ha peso $w_j > 0$. 
- Due job sono compatibili se non si sovrappongono 
- Trovare il sottoinsieme di job compatibili di peso massimo
##### Soluzione dinamica
- ordino i job per finish time in modo crescente
- $p( j )$ = più grande indice $i < j$ tale che job $i$ sia compatibile con job $j$
###### sotto-problema $j$:
$OPT[ j ]$ = peso massimo di un qualsiasi sottoinsieme di job compatibili costituito solo dai job $1,2,..,j$
- La soluzione cercata si trova in $OPT[ n ]$ 
	- Caso 1. $OPT[ j ]$ non seleziona $j$: 
		- Allora l’ottimo di $j$ deriva  dall’ottimo dei primi $j-1$esimi job 
- Caso 2. $OPT[ j ]$ seleziona $j$: 
	- Colleziona il costo di $w_j$ 
	- Non può usare i job incompatibili $\{ p(j) +1, p(j)+2, ..., j-1\}$.
	- Deve contenere una soluzione ottima per i job compatibili rimanenti $1, 2 , .., p(j)$
![[Pasted image 20250826161344.png]]
- $O(n\ log \ n)$ 
#### Knapsack problem
![[Pasted image 20250826164212.png]]
#### definizione
- Dati $n$ elementi: 
- L'elemento $i$ fornisce un valore $v_i$ e pesa $w_i$ 
- Valore di un sottoinsieme di oggetti = somma dei valori dei singoli oggetti 
- Lo zaino ha peso limite $W$ 
- Riempire lo zaino in modo tale da massimizzare il valore degli oggetti trasportati, ma non superare il limite $W$ 
##### Soluzione dinamica
**Def sotto problemi**
- $OPT[ i , w]$ = valore ottimo del knapsack problem con oggetti  $1,.., i$ con peso limite $w$
Goal: $OPT[ n, W]$
- Caso 1. $OPT[ i, w ]$ non seleziona $i$: 
	- $OPT [ i, w]$ seleziona i migliori $\{1,2,..,i-1\}$ con peso limite $w$ 
- Caso 2. $OPT[ i, w ]$ seleziona $i$: 
	- Colleziona il valore $v_i$  
	- Nuovo peso limite = $w-w_i$   
	- $OPT[ i, w ]$ seleziona i migliori $\{1,2,...i-1\}$ con nuovo peso limite
![[Pasted image 20250826165200.png]]
![[Pasted image 20250826165213.png]]
- $O(nW)$ tempo e spazio
##### Soluzione per il recupero
![[Pasted image 20250826165346.png]]
- *trace back* parte dalla fine della matrice dove si ha la soluzione ottima e prende di volta in volta la condizione massima tenendo conto che può prendere oppure no quel determinato peso
![[Pasted image 20250905111050.png]]

#### Sequence Alignment
![[Pasted image 20250827100012.png|400]]

![[Pasted image 20250827100003.png|500]]
#### definizione
**definizione di edit distance**
- operazioni di allineamento che portano a un costo minimo che include
- Gap penalty $δ$; mismatch penalty $α_{pq}$
- Cost= somma delle penalità gap e mismatch
**sequence alignment definizione** 
- Date 2 stringhe  $x_1x_2...x_n \ e \  y_1y_2...y_n$ trovare un allineamento di costo minimo  
- Un allineamento $M$ è un insieme di coppie ordinate $x_i-y_j$ affinché ogni carattere appaia al massimo in una coppia e senza incroci 
- Il costo di un allineamento $M$ è:
![[Pasted image 20250827100507.png]]
##### Soluzione dinamica
**definisco sotto-problemi**
$OPT[ i,j ]$ = costo minimo di allineamento delle stringhe di prefisso $x_1x_2...x_i$ e $y_1y_2...y_j$

**Goal.** $OPT[ m,n ]$
Caso 1. $OPT[ i,j]$  matcha  $x_i-y_j$   
- Paga mismatch per $x_i-y_j$ + costo minimo per allineare  $x_1x_2...x_{i-1}$ e $y_1y_2...y_{j-1}$  (costo può anche essere 0)
Caso 2a. $OPT[ i,j ]$ lascia $x_i$ non matchata 
- Paga gap per $x_i$ + costo minimo per allineare   $x_1x_2...x_{i-1}$ e $y_1y_2...y_j$   
Caso 2b. $OPT[ i,j ]$ lascia $y_j$ non matchata 
- Paga gap per $y_j$ + costo minimo per allineare  $x_1x_2...x_i$ e $y_1y_2...y_{j-1}$
![[Pasted image 20250827101219.png]]
- $O(mn)$ 
##### migliorie con Hirschberg's algorithm
- si può ridurre il costo spaziale in $O(m+n)$ 

#### Max-flow e min-cut
![[Pasted image 20250827152136.png]]


#### definizione
Una rete di flusso è una tupla $G=(V,E,s,t,c)$: 
- Grafo diretto $(V,E)$ con una sorgente s e un pozzo t 
- Capacità $c(e) ≥ 0$ per ogni arco $e$
per risolvere questo problema dobbiamo definire cosa sono
- *st-cut*
	- partizione $(A,B)$ di nodi con $s ∈ A$  e $t ∈ B$
	- La *capacità* di un st-cut è la somma delle capacità degli archi che vanno da A in B
![[Pasted image 20250901123055.png]]
- *min-cut*
	- Trovare un taglio di capacità minima
	- Il **min-cut** è quello che fornisce il limite più stretto, cioè il collo di bottiglia minimo del grafo.
- *st-flow*
	- Un st-flow $f$ è una funzione che soddisfa: 
![[Pasted image 20250827152718.png]]
- *il valore di un st-flow* è 
![[Pasted image 20250827153032.png]]

- *max-flow*
	- problema dove si vuole trovare un flusso dal valore massimo
- *Residual network definizione*
	- *Arco originale*
		- $e=(u,v) ∈ E$
		- Flow $f(e)$
		- Capacity $c(e)$ 
	- *Arco al contrario* $e^{reverse}$ = $(v,u)$
		- undo del flusso inviato
	- *residual capacity:*
![[Pasted image 20250827153432.png]]
- *Residual network.* $G_f =(V,E_f , s, t, c_f)$ 
	- $E_f = { e : f(e) < c(e)} \ \   U \ \  {e : f(e^{reverse}) > 0}$
	- Proprietà chiave : $f′$ è un flusso valido  in $G_f$ se $f+f′$ è un flusso valido in $G$
*Augmenting path definizione:*
- Un cammino aumentante è un cammino semplice $s↝t$ nella rete residua $G_f$  

*Def bottleneck capacity:* 
- La capacità di bottleneck di un cammino aumentante  $P$ è la capacità minima residua di un arco in $P$ 
Proprietà chiave: 
Sia $f$ un flusso e $P$  un cammino aumentante in $G_f$ allora, dopo aver chiamato $f’ ← AUGMENT( f,c,P)$, l’$f’$ risultante è un flusso e $val(f’) = val(f) + bottleneck(Gf,P$) 

#### Ford-Fulkerson
- Inizia con $f(e) = 0$ per ogni arco $e ∈ E$ 
- Trova un cammino $s↝t$ $P$ nella rete residua $G_f$  
- Aumenta il flusso lungo il cammino $P$ 
- **continua a cercare cammini aumentanti nel grafo residuo$G_f$**, e aggiorna il flusso lungo quei cammini, **finché non esistono più cammini da s a t nel grafo residuo**.


- *Lemma del valore del flusso.* 
	- Sia f un flusso qualsiasi e sia $(A,B)$ un taglio qualsiasi. Allora, il valore del flusso f è uguale al flusso netto attraversante il taglio $(A,B)$
![[Pasted image 20250827153032.png]]


- *Dualità debole:* 
	- Sia $f$ un qualsiasi flusso  e sia $(A,B)$ un qualsiasi taglio .                  
		- Allora,   $val(f) ≤ cap(A,B)$. 

- *Corollario:* 
	- Sia f un qualsiasi flusso e $(A,B)$ un qualsiasi taglio. se $val(f)$ = $cap(A,B)$, allora $f$ è un max flow e $(A,B)$ è un min cut 

- *Max-flow min-cut theorem:* 
	- Il valore di un flusso massimo = capacità di un taglio minimo 

- *Augmenting path theorem :* 
	- Un flow $f$ è un max flow se non ha cammini aumentanti  

- *Teorema:* 
	- Dato un qualsiasi max flow f, possiamo calcolare il min cut (A,B)  in O(m) tempo
>[!danger]- ALTRA COSA FONDAMENTALE: il numero di cammini aumentanti può essere **ESPONENZIALE** rispetto all'input. 
>![[Pasted image 20250830172252.png]]

L'obiettivo principale è **scegliere dei cammini aumentanti** tali che
- possano essere **trovati in modo efficiente** (quindi in $O(m)$),
- vengano eseguite **poche iterazioni** (e quindi pochi aumenti),

Per farlo possiamo sceglierli con

- una **bottleneck capacity molto grande** -> così ogni aumento contribuisce MOLTO al flusso totale,
- pochi archi -> riduci la probabilità di dover "tornare indietro",

###### Verso l'algoritmo Partendo dai due punti precedenti, l'idea è questa

- Usiamo un **parametro** $\Delta$ -> è un valore grande,
- Costruisco un **sottografo** $G_{f}(\Delta)$ contenente SOLO gli archi che hanno capacità $\ge \Delta$,
- In questo modo ogni cammino aumentante nel nuovo grafo ha una **bottleneck capacity** $\ge \Delta$
![[Pasted image 20250830172854.png]]
,

###### PSEUDOCODICE 
Come scegliere il successivo cammino aumentante in Ford-Fulkerson? Scegli quello che usa meno archi (il più corto) -> usa la BFS. >Scegliendo i più corti saturi velocemente gli archi "colli di bottiglia" 
![[Pasted image 20250830173227.png]]



![[Pasted image 20250908095623.png]]
![[Pasted image 20250908095631.png]]
![[Pasted image 20250908095639.png]]


## Algoritmi di approssimazione
#### definizione
- Un α-approximation algorithm per un problema di ottimizzazione è un algoritmo polinomiale che per tutte le istanze del problema produce una soluzione il cui valore è compreso entro un fattore α  rispetto al valore di una soluzione ottima
*Minimization problem:* voglio minimizzare un costo
- $α ≥ 1$ 
- Per ogni soluzione restituita $x$, $cost(x) ≤ α$  $OPT(x)$ 
*Maximization problem:* voglio massimizzare un valore
- $α ≤ 1$ 
- Per ogni soluzione restituita $x$, $value(x) ≥ α OPT(x)$
### Load balancing
![[Pasted image 20250827162647.png]]
#### definizione
Date $m$ identiche macchine, $n ≥ m$ jobs, job $j$ ha processing time $t_j$. 
- Job $j$ deve essere eseguito contiguamente su una macchina 
- Una macchina può processare al più un job alla volta 
- Assegnare ogni job a una macchina affinché il make span sia minimo
*Def load:* 
- Sia $S[i]$ il sottoinsieme di job assegnati alla macchina $i$. 
- Il load  della macchina $i$ è $L[i] = Σ_{j \ ∈ \ S[i]}  \ t_j$ . 

*Def make span:* 
- Il make span è il valore massimo di load di ogni macchina $L = max_i L[i]$
##### Soluzione List Scheduling Algo
- Considera i job in un qualche ordine fisso 
- Assegna il job $j$ alla macchina $i$ il cui carico è finora il più piccolo
- Complessità: 
	- $O(n log n)$ 
	- Usando una coda con priorità per i carichi $L[k]$ 
##### Dimostrazioni e lemma

![[Pasted image 20250828104129.png]]
![[Pasted image 20250906111359.png]]
![[Pasted image 20250906111345.png]]
![[Pasted image 20250828104137.png]]
![[Pasted image 20250828104146.png]]
![[Pasted image 20250828104212.png]]
### Load balancing LPT(Longest Processing Time)
#### definizione
- Ordina $n$ jobs in ordine decrescente di tempo di processione
- ciò lo rende molto più vicino alla soluzione ottima
##### *Teoremi*
![[Pasted image 20250828104447.png]]
![[Pasted image 20250828104454.png]]
## RIDUZIONI POLINOMIALI
### Definizione
Una **riduzione polinomiale** è un metodo per trasformare un problema $X$ in un altro problema $Y$, in modo che:
- qualsiasi istanza di $X$ possa essere risolta tramite:
    - un numero polinomiale di operazioni standard, più
    - un numero polinomiale di chiamate a un "oracolo" che risolve $Y$.
Si scrive:
- $X \leq_P Y$ 
- **risolvere Y implica poter risolvere X** in tempo polinomiale
#### 3 proprietà importanti
- **Progettazione di algoritmi**:  
    Se $X \leq_P Y$ e $Y$ è risolvibile in tempo polinomiale, allora anche $X$ lo è.
- **Dimostrare difficoltà (intractability)**:  
    Se $X \leq_P Y$ e $X$ non è risolvibile in tempo polinomiale, allora neanche $Y$ lo è.
- **Equivalenza**:  
    Se $X \leq_P Y$ e $Y \leq_P X$, allora $X \equiv_P Y$.  
    Significa che hanno la stessa complessità polinomiale (si risolvono in polinomiale se e solo se l’altro lo è).
### Esempi di riduzioni
#### 1. Independent Set con Vertex Cover
- descriviamo prima il problema dell'indipendent set
**Independent Set (IS)**: Dato un grafo $G=(V,E)$ e un intero $k$, esiste un sottoinsieme di $k$ vertici non adiacenti tra loro?
![[Pasted image 20250902125926.png]]
- problema del Vertex Cover
**Vertex Cover (VC)**: Dato $G=(V,E)$ e un intero $k$, esiste un sottoinsieme di $k$ vertici che copre tutti gli archi?
![[Pasted image 20250902130038.png]]
#### Vogliamo dimostrare che $IS \equiv_P IS$.
### (⇒) Da Independent Set a Vertex Cover

- Supponiamo che $S$ sia un IS di dimensione $k$.
- Allora $V−S$ ha dimensione $n−k$.
- Consideriamo un arco $(u,v)∈E(u,v)$
    - Poiché $S$ è indipendente, non può contenere entrambi i vertici $u,v$.
    - Quindi almeno uno dei due appartiene a $V-S$.
- Dunque $V−S$ è un vertex cover di dimensione $n-k$
### (⇐) Da Vertex Cover a Independent Set

- Supponiamo che $V−S$ sia un VC di dimensione $n−k$.
- Allora $S$ ha dimensione $k$.
- Consideriamo un arco $(u,v)∈E(u,v)$.
    - Poiché $V−S$ è un VC, almeno uno tra $u,v$è in $V−S$.
    - Quindi non possono essere entrambi in $S$.
- Dunque $S$ è un independent set di dimensione $k$.
#### 2. Set Cover con Vertex Cover
- descriviamo prima il problema del Set Cover
- **Set Cover (SC)**: Dato un insieme universo $U$, una collezione di sottoinsiemi $S_1, ..., S_m$​, e un intero $k$, esistono al più $k$ sottoinsiemi che coprono tutto $U$?
![[Pasted image 20250902160112.png]]
#### Vogliamo dimostrare che $VC \leq_P SC$.
## Costruzione della riduzione
Dato un grafo $G=(V,E)$ e un intero $k$:
1. **Universo**:
    $U = E \quad (\text{gli archi del grafo diventano gli elementi dell’universo})$
2. **Famiglia di sottoinsiemi**:  
    Per ogni vertice $v \in V$, definiamo:
    $S_v = \{ e \in E : e \text{ è incidente a } v \}$
3. **Parametro**:  
    Manteniamo lo stesso valore $k$.

Così otteniamo un’istanza di Set Cover $(U, \mathcal{S}, k)$
### (⇒) Se $G$ ha un Vertex Cover di dimensione $k$
- Supponiamo che $X \subseteq V$ sia un VC con $|X|=k$.
- Consideriamo $\mathcal{Y} = \{ S_v : v \in X \}$
- Ogni arco è coperto da almeno un vertice in $X$, quindi $\mathcal{Y}$ è un set cover di dimensione $k$.
### (⇐) Se $(U, \mathcal{S}, k)$ ha un Set Cover di dimensione $k$

- Supponiamo che $\mathcal{Y} \subseteq \mathcal{S}$ sia un set cover di dimensione $k$.
- Sia $X = \{ v \in V : S_v \in \mathcal{Y} \}$.
- Poiché ogni arco $e$ appartiene ad almeno un sottoinsieme $S_v$, significa che $v \in X$ copre quell’arco.
- Quindi $X$ è un VC di dimensione $k$.

![[Pasted image 20250902160308.png]]
#### 3. 3-SAT con Independent Set
- descriviamo prima il problema del 3-SAT
- **3-SAT**: Formula booleana in CNF con clausole di 3 letterali ciascuna. La formula è soddisfacibile?
![[Pasted image 20250902161354.png]]
#### Vogliamo dimostrare che $3-SAT \leq_P IS$.
## Costruzione della riduzione

1. **Nodi**:  
    Per ogni clausola della formula, aggiungiamo 3 nodi (uno per ogni letterale).
2. **Archi interni**:  
    I 3 nodi di una clausola vengono collegati in un triangolo.  
    → garantisce che al massimo 1 letterale possa essere scelto dall’insieme indipendente.
3. **Archi tra clausole**:  
    Collegare ogni letterale con la sua **negazione** (es: $x_i$​ con $\neg x_i$).  
    → impedisce di selezionare contemporaneamente un letterale e la sua negazione.
4. **Parametro**:
	$k = |\Phi| \quad (\text{cioè una scelta per ogni clausola})$.
## Dimostrazione

### (⇒) Se $\Phi$ è soddisfacibile

- Esiste una assegnazione che rende vera ogni clausola.
- Per ciascuna clausola, scegliamo un letterale che risulta **vero**.
- Questi nodi non saranno collegati fra loro (per costruzione), quindi formano un **independent set** di dimensione $k$.
### (⇐) Se $G$ contiene un independent set di dimensione $k$

- Ogni triangolo rappresenta una clausola.
- Per avere un IS di dimensione $k$, dobbiamo scegliere **esattamente un nodo per triangolo**.
- I letterali scelti non possono essere contraddittori (perché IS esclude coppie collegate).
- Assegniamo **true** a quei letterali → tutte le clausole sono soddisfatte.
- Dunque $\Phi$ è soddisfacibile.


![[Pasted image 20250902161504.png]]

- **Transitività**: Se $X \leq_P Y \ X≤P​Y \ e \ Y≤_PZ \ Y \leq_P Z$.  
    → Esempio:
    $\text{3-SAT} \leq_P \text{IS} \leq_P \text{VC} \leq_P \text{SC}$



- **P**: problemi di decisione per i quali **esiste un algoritmo polinomiale** che li risolve.  
    → Sono i problemi “facili da risolvere”.
    
- **NP**: problemi di decisione per i quali **esiste un certificatore polinomiale**.  
    → Non sappiamo se sono facili da risolvere, ma se qualcuno ci dà una _soluzione candidata_ (certificato), possiamo verificarla velocemente.
    
- **EXP**: problemi di decisione per i quali **esiste un algoritmo esponenziale** che li risolve.  
    → In pratica: anche se non troviamo algoritmi migliori, con una brute force in tempo esponenziale si riescono a risolvere.

$P \subseteq NP$
$NP \subseteq EXP$

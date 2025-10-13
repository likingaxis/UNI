[[cap3.pdf|pdf della lezione]]
Ripassiamo prima di tutto la
>[!info]- differenza tra tipo di dato e struttura dati
>- tipo di dato: definisce il modo in cui una collezione di oggetti è fatta, come ad esempio un dizionario avrà chiave valore, i suoi metodi insert, search ecc...
>- struttura dati spiega come una collezione di oggetti deve funzionare in termini di algoritmi efficienti

Vedremo diversi tipi di dato
### 1. IL DIZIONARIO
Il dizionario è un tipo di dato che è un insieme di $S$ elementi tutti formati da $(chiave,valore)$
##### Operazioni possibili
1. `insert(elem e,chiave k)`
		aggiunge a $S$ una nuova coppia 
2. `delete(chiave k)`
		cancella da $S$ la coppia che ha quella chiave $k$
3. `search(chiave k)`-> ritorna $elem$
		restituisce l'elemento che ha quella chiave altrimenti $null$

### 2. LA PILA
la pila è un tipo di dato che ha una sequenza $S$ con $n$ elementi

##### Operazioni possibili
1. `isEmpty()`-> ritorna il risultato
		restituisce $true$ se S è vuota e $false$ altrimenti 
2. `push(elem e)`
		aggiunge $e$ come ultimo elemento di $S$
3. `pop()`-> ritorna  $elem$
		toglie da $S$ l'ultimo elemento e li restituisce
4. `top()`-> ritorna $elem$
		restituisce l'ultimo elemento di $S$ (senza toglierlo da $S$)


### 3. LA CODA
la coda è un tipo di dato che ha una sequenza $S$ con $n$ elementi

##### Operazioni possibili
1. `isEmpty()`-> ritorna il risultato
		restituisce $true$ se S è vuota e $false$ altrimenti 
2. `enqueue(elem e)`
		aggiunge $e$ come ultimo elemento di $S$
3. `dequeue()`-> ritorna  $elem$
		toglie da $S$ il primo e lo restituisce
4. `first()`-> ritorna $elem$
		restituisce il primo elemento elemento di $S$ (senza toglierlo da $S$)


### TECNICHE DI RAPPRESENTAZIONE
Ci sono due tipi di tecniche di rappresentazione:
>[!info] Rappresentazioni indicizzate
>Rappresento il mio tipo di dato attraverso ad esempio $array$
>- proprietà forte
>	- gli indici sono tutti numeri consecutivi
>- proprietà debole
>	- non puoi aggiungere nuove celle ad un array(per farlo devi fare realloc ecc...)

>[!question]- definizione di array
>è una collezione di celle numerate, in ogni cella c'è un elemento di un tipo prestabilito

>[!info] Rappresentazioni collegate
>I dati sono contenuti in $record$ collegati fra loro mediante puntatori
>- i $record$ sono numerati tipicamente con il loro indirizzo di memoria, si possono creare e distruggere dinamicamente
>- il collegamento tra $record$ avviene tramite puntatori
>- proprietà forte
>	- è possibile aggiungere o togliere $record$
>- proprietà debole
>	- gli indirizzi non sono per forza consecutivi
>esempi grafici
>![[Pasted image 20241118120857.png|600]]




### COME SI REALIZZA UN [[ALGORITMI LEZ.10#1. IL DIZIONARIO|DIZIONARIO]]

### 1. ARRAY NON ORDINATO
uso un array non ordinato in base alle chiavi
1. **insert** mi costa $O(1)$ mi basta inserire dopo l'ultimo elemento
2. **search** costa $O(n)$ perché per trovare la chiave devo scorrere l'array
3. **delete** costa $O(n)$ perché devo fare il search
### 2. ARRAY ORDINATO
1. **insert** mi costa $O(n)$ perché devo fare $O(log(n))$ confronti per scoprire la posizione e poi $O(n)$ per far shiftare gli altri elementi se devo metterlo in mezzo
2. **search** costa $O(log(n))$ farò la ricerca binaria
3. **delete** costa $O(n)$ come con insert quindi faccio ricerca e poi lo shift di elementi
>[!bug]- queste cose nelle liste?
>- nelle liste non ordinate i costi rimangono invariati
>- in quelle ordinate variano perché nelle liste non posso fare ricerche binarie .
>	- search sarà $O(n)$ perchè
>		- le liste non hanno indici ma sono concatenate e quindi bisogna scorrerle tutte
>	- insert $O(n)$ 
>		- sarà sempre $O(n)$
>	- delete $O(n)$

## ESERCIZIO
![[Pasted image 20241118124310.png]]

## DEFINIZIONI SUGLI ALBERI
![[Pasted image 20241118124837.png]]
- il ***grado*** di un nodo é il numero dei figli
- un ***antenato*** è quando ho un nodo $u$ e se scendo di padre in padre raggiungo un figlio $v$ 
- un ***discendente*** è come antenato ma visto al contrario
#### USIAMO GLI ALBERI d-ari CON GLI ARRAY
#### STRUTTURA 1.VETTORE DEI PADRI
come verrà gestito il tutto?
per un albero con $n$ nodi avrò un array di dimensione $P$ con almeno $n$ elementi
una generica cella $i$ conterrà:
- il contenuto del nodo $i$
- l'indice nell'array del rispettivo padre 

![[Pasted image 20241118150152.png|500]]
![[Pasted image 20241118150210.png|500]]
quindi dentro la singola posizione avremmo `(P[i].info, P[i].parent)`
- `P[i].info`: contenuto informativo nodo 
- `P[i].parent`: indice del nodo padre
- il tempo per individuare il padre di un nodo è $O(1)$, perché basta accedere al valore 
- il tempo per individuare uno o più figli di un nodo è $O(n)$ poiché al più é necessario scorrere tutto l'array
- il numero di figli può essere un numero arbitrario
#### STRUTTURA 2. VETTORE POSIZIONALE
###### Come mi trovo gli elementi dell'albero?
![[Pasted image 20241118155454.png]]
si possono fare due operazioni per trovare o i figli o i padri
##### 1. come trovare i figli di un determinato padre
applichi la seguente formula partendo da 0:
$$(d \times i) + j$$
dove:
- $d$ rappresenta il numero massimo di nodi
- $i$ rappresenta la posizione del padre su cui ci basiamo
- $j$ rappresenta sei intendiamo il primo, il secondo, il terzo ... figlio
##### 2. come trovare un padre di un determinato figlio
applichi la seguente formula partendo da 0:
$$\left\lfloor \frac{i-1}{d} \right\rfloor$$
dove:
- $i$ rappresenta il nome del figlio
- facciamo -1 perché il padre è nella parte prima del nodo figlio
- $d$ è il massimo dei nodi
###### COSTI DI QUESTA STRUTTURA
- il tempo per individuare il padre di un nodo è $O(1)$, perché basta fare la formula
- il tempo per individuare uno o più figli di un nodo è $O(1)$ poiché basta fare la formula
- il numero di figli deve essere ESATTAMENTE $d$
### Rappresentazione delle due strutture ma usando liste collegate

###### 1. struttura vettore dei padri
![[Pasted image 20241118163423.png]]
###### 2. struttura vettore posizionale
![[Pasted image 20241118163442.png]]
###### 3. struttura primo figlio-> fratelli successivi
![[Pasted image 20241118163841.png]]
## VISITE DI ALBERI
ci sono algoritmi che consentono di visitare alberi in modo sistematico, ovvero una sola volta 
per una sola volta intende che arrivo al mio risultato senza scorrere l'albero più volte
ci sono due tipi di visite che si visitano tutto l'albero:
#### Visita in profondità
![[Pasted image 20241118170424.png|400]]
ha come obiettivo quello di partire dalla radice $r$ fino visitando di figlio in figlio fino a raggiungere la foglia, una volta raggiunta la foglia si passa agli antenati e si visitano i figli dei rispettivi antenati se esistono
##### PSEUDOCODICE DI VISITA IN PROFONDITÀ
questo pseudocodice vale per un albero binario
le informazioni che visitiamo le inseriamo in una pila
![[Pasted image 20241118170553.png|500]]

![[ezgif.com-speed_3.gif]]
#### COSTO
avrò un costo $O(1)$ per un singolo nodo, quindi per ogni nodo avrò $O(n)$
#### La sua versione ricorsiva
![[Pasted image 20241118172316.png|500]]

così con la **visita in preordine** si fa 
- radice
- sottoalbero sinistro
- sottoalbero destro
ci sono altri due tipi di visita che si fanno scambiando delle righe di codice
**visita simmetrica**:
- sottoalbero sinistro
- radice
- sottoalbero destro
**si scambia riga 2 con 3**
**visita postordine**:
- sottoalbero sinistro
- sottoalbero destro
- radice
**si scambia riga 2 con 4**
![[Pasted image 20241118173255.png|500]]
in Preordine sarebbe:` A L E R B O `
in Simmetrica sarebbe: `E L R A B O` 
in Post-ordine sarebbe: `E R L O B A`
##### ALGORITMO DI VISITA IN AMPIEZZA
![[Pasted image 20241118175818.png|400]]
parte da $r$ e visita i nodi per livello
##### PSEUDOCODICE DI VISITA IN AMPIEZZA
questo pseudocodice vale per un albero binario
![[Pasted image 20241118175942.png|600]]
se non ti ricordi le code guarda [[ALGORITMI LEZ.10#3. LA CODA|guarda qua]]
- enqueue aggiunge all'ultima posizione la radice
- poi in un while ogni volta andiamo a prelevare il primo elemento della coda e visitiamo il nodo mettendo nella coda il figlio $sx$ e $dx$
non avrò mai dei null nella coda perché non torno mai indietro
![[Pasted image 20241118180346.png]]

#### COSTO
avrò un costo $O(1)$ per un singolo nodo, quindi per ogni nodo avrò $O(n)$
## ESEMPIO SULL'UTILITÀ DI QUESTI ALGORITMI DI VISITA
### Calcolo dell'altezza
![[Pasted image 20241118182559.png|400]]
- in maniera ricorsiva mi calcolo l'altezza dei due sottoalberi e mi prendo il massimo
- mi calcolo $1$+ il massimo dei sottoalberi, 1 è la radice
##### PSEUDOCODICE DEL CALCOLO DELL'ALTEZZA 
![[Pasted image 20241118182739.png|500]]
- $r=null$ ci serve anche per definire 
#### COSTO
scendiamo in profondità fino a $O(n)$ sia sin che des sono $O(n)$

![[Pasted image 20241118183351.png|500]]

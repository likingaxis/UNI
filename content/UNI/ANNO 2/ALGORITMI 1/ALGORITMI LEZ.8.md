[[cap4.7.pdf|pdf della lezione 8]]
### Complessità di un algoritmo
Fino ad ora abbiamo sempre definito la complessità di un algoritmo basandoci su delle risorse
che staranno in un upper-bound o lower-bound

- <font color="#d83931">lower-bound:</font> definisco un $\Omega (f(n))$ tale che tutte le risorse che genero $r(n)$ del mio algoritmo rispettino la seguente condizione $r(n)=\Omega(f(n))$ nel caso peggiore
	-  **$f(n)$** è il "punto minimo" da cui partire, e posso solo andare a salire.
- <font color="#d83931">upper-bound:</font> definisco un $O (f(n))$ tale che tutte le risorse che genero $r(n)$ del mio algoritmo rispettino la seguente condizione $r(n)=Of(n))$ nel caso peggiore
	-  **$f(n)$** è il "punto massimo" che posso raggiungere, e posso solo andare sotto a lui

>[!question]- che intende per risorsa di calcolo? 
>memoria $o$ spazio utilizzati

- ==lower-bound di un problema: minimo si sta a quel determinato costo computazionale==
- ==per dimostrare un lower bound in termini di costi si puo usare una tecnica che usa gli alberi di decisione(non funziona con tutti gli algoritmi ma solo su algoritmi basati su confronti)==
### Analizzare invece un **problema** e non un algoritmo
>[!info]- come vedo io la differenza tra problema e algoritmo
>- il problema rappresenta una cosa risolvibile con più algoritmi e quindi i costi devono definire ogni algoritmo
>- l'algoritmo invece è una singola istanza del problema che lo risolve

Un problema ha una complessità rispetto ad una risorsa di calcolo definibile in due casi
- <font color="#d83931">lower bound: </font> se ogni algoritmo del problema P ha costo di esecuzione nel caso peggiore di $\Omega(f(n))$ in quella determinata risorsa
- <font color="#d83931">upper bound: </font> se esiste almeno un algoritmo del problema P che ha costo di esecuzione nel caso peggiore $O(f(n))$ rispetto a una determinata risorsa

### Quando un algoritmo è ottimale?
Un algoritmo si dice ottimale quando abbiamo un problema con lower-bound tipo $\Omega(f(n))$ e l'algoritmo riesce a risolvere il problema rispetto a quella risorsa di calcolo in $O(f(n))$  quindi in maniera **Ottima**, ovvero che più di così non si può fare
##### Esempio con ordinamento
se ho n numeri e voglio ordinarli ad esempio il lower-bound potrebbe essere $\Omega$(n)
ma non sappiamo algoritmi che fanno la cosa in n ma solo con upper-bound tipo $nlogn$
quindi abbiamo un gap
possiamo fare meglio?
## Complessità temporale del problema dell'ordinamento
 - Lower bound: $\Omega(n)$
	 - un algoritmo che deve ordinare `n` per forza di cose deve vederli tutti.
	 - non esiste al momento nessun algoritmo che costi n

- upper-bound: $O(n^2)$
	- Insertion Sort
	- Selection Sort
	- Quick Sort
	- Bubble Sort

- upper-Bound migliore: $O(n \space log(n))$
	- Merge Sort
	- Heap Sort
	Questi due algoritmi, sulla base della definizione di prima, sono definiti ottimi all'interno della classe degli algoritmi basati su confronti.


Abbiamo quindi un gap di $log (n$) tra il **lower-bound** e il miglior **upper-bound**.

Come accennato prima, **tutti questi algoritmi sono basati su <u>CONFRONTI</u>.

# Algoritmi basati su confronti
Sono tutti quegli algoritmi che confrontano gli elementi per dare un risultato.
>[!warning]- Tutti gli algoritmi che abbiamo visto sono per confronto e quindi questo lower bound vale

>[!summary]- DEFINIZIONE: ORDINAMENTO PER CONFRONTI
>Dati due elementi $a_i$ e $a_j$, per determinare l'ordinamento relativo effettuiamo una delle seguenti operazioni di confronto:
>- $a_{i} < a_j$
>- $a_{i} \le a_j$
>- $a_{i} = a_j$
>- $a_{i} \ge a_j$
>- $a_{i} > a_j$
>
>Non si possono esaminare i valori degli elementi oppure ottenere informazioni sul loro ordine senza eseguire ALMENO UNA di queste operazioni.
### Teorema Lower-Bound
###### Enunciato
prendete un algoritmo che gira su modello RAM di tipo confronto
- ordina n elementi
- deve fare nel caso peggiore $\Omega$ $(nlogn)$ confronti
- MI RACCOMANDO DI USARE LA PAROLA CONFRONTI
Merge e Heap sono ***ottimi***
#### Per dimostrare il Teorema usiamo albero di decisione
IDEA: descrivere in modo astratto il comportamento di un generico algoritmo di ordinamento per confronto attraverso una struttura ad albero, basandosi sull'ipotetico input dato in pasto all'algoritmo.
In pratica, partendo dall'input, descrive i confronti che l’algoritmo esegue.

La sequenza di confronti che osserviamo sul display dipende dall'input stesso
- descriviamo in modo astratto tutte le possibili sequenze su un input di dimensione n
	- attraverso un albero
	- la prossima decisione di ogni algoritmo la facciamo in base al confronto che facciamo prima, ovvero l'esito che porta

Un generico algoritmo di ordinamento per confronto lavora nel modo seguente: 
- confronta due elementi $a_i$ e $a_j$ (ad esempio effettua il test $a_i\le a_j$ ); 
- a seconda del risultato, riordina e/o decide il confronto successivo da eseguire.

STRUTTURA: l'albero è radicato e
	- i **nodi interni** (cerchi grigi) sono i **potenziali confronti**
	- le **foglie** (rettangoli bianchi) sono le **risposte dell'algoritmo**

![[Pasted image 20241105200726.png]]

>[!summary]- spiegazione dettagliata degli step
>Guardando dalla radice e spostandoci al figlio di sinistra:
> - confronta il primo elemento con il secondo `(1:2)`
> 	- se il primo è $\le$ del secondo, scende a crea il figlio a sinistra `(2:3)`
> - confronta il secondo con il terzo `(2:3)`
> 	- se il secondo è $\le$ del terzo darà come input `PRIMO, SECONDO, TERZO`
> 	- se il secondo è $>$ del terzo crea un altro figlio `(1:3)`
> - confronta il primo con il terzo `(1:3)`
> 	- se il primo è $\le$ del terzo darà come input `PRIMO, TERZO, SECONDO`
> 	- se il primo è $>$ del terzo darà come input `TERZO, PRIMO, SECONDO`


ci da una descrizione compatta di tutte le decisioni possibili da fare
>[!warning] al posto dei **:** dobiamo mettere il simbolo sulla freccia(>, <, ecc...)

avremo quindi le varie ==permutazioni== della sequenza
Varie osservazioni utili

##### OSSERVAZIONI
>[!bug]- L'albero di decisione ***non è*** associato a un problema
>questo perché non rappresenta il problema da risolvere ma i passi decisionali che un algoritmo potrebbe eseguire per risolvere il problema.

>[!bug]- L’albero di decisione ***non è*** associato ***solo*** ad un algoritmo
>non è associato AL SINGOLO algoritmo ma mostra i passaggi che ALGORITMI DIVERSI potrebbero fare

>[!bug]- L’albero di decisione è associato ad un ***algoritmo*** e a una ***dimensione dell’istanza***
>nel punto 2 abbiamo detto che di per sé l'albero di decisione non è associato ad un solo algoritmo; ma se noi costruiamo un albero di decisione per un ***algoritmo specifico*** e per una ***determinata istanza***, allora l'albero sarà ***ottimizzato*** per quel singolo algoritmo.
 
 >[!bug]- L’albero di decisione descrive le diverse sequenze di confronti che un certo algoritmo può eseguire su istanze di una ***data dimensione***
 >
> l'albero mostra **tutte le possibili sequenze di scelte o confronti** che l’algoritmo potrebbe fare per risolvere il problema per un input di una certa dimensione.

>[!bug] L'albero di decisione è una descrizione alternativa dell'algoritmo (customizzato per istanze di una certa dimensione)


>[!question]- Esercizio sull'albero
>![[Pasted image 20241105201340.png]]
>>[!Solution]- ecco la soluzione
>>![[Pasted image 20241105201410.png|600]]
> 
> 

#### Proprietà
1. Per una particolare istanza, i confronti eseguiti dall’algoritmo su quella istanza rappresentano un ***cammino radice –> foglia***

2. L’algoritmo segue un cammino diverso a seconda delle caratteristiche dell’istanza (input)
	 - Caso peggiore: cammino più lungo

3. Il numero di confronti nel caso peggiore è pari ***all’altezza dell’albero di decisione***

4. Un albero di decisione di un algoritmo (corretto) che risolve il problema dell’ordinamento di `n elementi` deve avere necessariamente almeno `n! foglie`
	- se ce ne fossero meno vorrebbe dire che c'è una permutazione che non compare mai.

>[!bug] l'istanza peggiore è quella che innesca il cammino più lungo

#### Lemma che ci serve per dimostrare il lower-bound
>[!info]
>Un albero binario T con k  foglie, ha un altezza di almeno $log_2(k)$ 

- k lo poniamo all'inizio
#### Caso base
Abbiamo una radice che ovviamente ci porta un albero lungo 0 

#### Caso induttivo con almeno $2$ foglie
Ci poniamo un nodo $v$ che rappresenta il primo padre più vicino alla radice
inevitabilmente $v$ deve avere due figli e uno dei due figli potrebbe essere un sotto albero $u$ che avrà almeno $k/2$ foglie minori del numero di $k$
applico l'ipotesi induttiva e avrò $log_2(k/2)$
- 1 approssimazione di tutti i nodi prima che arrivi a $v$
- faccio formule matematiche
![[Screenshot_2024-11-05-21-39-49-35_45415775811cea13943236d9369df411.jpg|700]]

>[!bug] TUTTO QUESTO RIGUARDA GLI ALBERI PER CONFRONTO

### Dimostrazione lower bound $\Omega (nlog(n))$ con lemma

considerando un albero di decisione di un generico algoritmo di ordinamento avremo che 
- è almeno alto $log_2(n!)$ per il punto 4 delle proprietà
- Applico formula di Stirling : $n! \approx 2(\pi \space n)^{\frac 1 2} \times (\frac n e)^n$    
- faccio delle semplificazioni varie e ottengo che
$$ h \geq n \ log(n)$$
>[!info]- semplificazioni varie
>![[Screenshot_2024-11-05-21-57-32-71_45415775811cea13943236d9369df411.jpg]]


>[!info]- Esercizio sul lower bound
>![[Pasted image 20241105215941.png|500]]


==53 questo all'orale ci sventra==
### Algoritmi non basati su confronti
### IntegerSort
##### Come funziona?
per ordinare $n$ elementi con valori posizionati in un array fatto da $[1,k]$
- usiamo un array $y$ con $k$ contatori che conteranno quante volte appare il numero in quella data posizione
in poche parole
$$Y[x]= numero \ di \ volte \ in \ cui \ appare \ il \ numero \ x \ nell'array \ X$$
quanti confronti? zero
#### Inserimento in y
![[integersort_contatore.gif]]

#### Ricostruzione in x
![[integersort_ordinamento.gif]]

#### PSEUDOCODICE

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
- il primo for mette ad ogni posizione di $Y$ zero
- il secondo for incrementa in base alle volte in cui appare l'elemento nella posizione
- faccio un for per ricostruirmi l'array $X$
- decremento $Y$ con un while finchè non diventa 0
### COSTI COMPUTAZIONALI
- da riga $7 \ a \ 11$ ho costo $1+Y[i]$ $k$ volte perché ogni volta il while lo faccio almeno una volta Ogni iterazione del `while` ha costo $O(1)$, quindi il totale è proporzionale a $1+Y[i]$

![[Pasted image 20241105223352.png|400]]

#### IntegerSort: analisi
- Tempo $O(1) + O(k) = O(k)$, per inizializzare `Y` a 0 (righe `2-3` del codice)
- Tempo $O(1) + O(n) = O(n)$, per calcolare i valori dei contatori (righe `4-5` del codice).
- Tempo $O(n+k)$, per ricostruire `X` (righe `6-11`)
COSTO TOTALE:$$O(n+k)$$Quindi abbiamo un tempo lineare se $$k = O(n)$$
Questo non contraddice il lower-bound di $\Omega(n \space log(n))$ perché L'INTEGER SORT NON È UN ALGORITMO BASATO SU CONFRONTI! 

se fa cagare dipende da k se k supera n avremo una cosa non lineare


[[cap4.7.pdf|pdf della lezione 9]]
## Altri algoritmi che non usano i confronti
### Spiegazione del bucket sort
- è una variante dell'integer sort
- verrà poi usato per il Radix Sort che vedremo in questa lezione
#### Obiettivo
ordinare $n$ record basandosi su una chiave interna $[1,k]$

>[!tip]- Esempio
>Supponiamo di voler ordinare una lista di studenti (ogni studente è un **record**) con i seguenti `campi`:
>- nome
>- cognome
>- anno di nascita
>- matricola
>
Vogliamo ordinarli in base alla loro **matricola**, e sappiamo che tutte le matricole sono numeri interi tra **1** e **1000**. Quindi:
>- `n` rappresenta il numero totale di studenti.
>- ogni studente ha una `campo chiave` (la **matricola**) rispetto al quale ordinare.
>- le chiavi (matricole) vanno da `1 a k`, con $k = 1000$ 
>- ogni studente ha poi altri campi associati alla chiave (`informazioni satellite`)

Sembra facile ma ci sono delle complicanze
>[!bug]- complicanze
>visto che con l'integer contavamo quante volte appariva quell'elemento non possiamo definire a 
>quale record appartiene quella determinata chiave
>per risolvere collego ad ogni chiave il record usando degli array di lunghezza 2 
> $[chiave,lista]$
### Come Funziona
- creo una array `Y`, dove in `Y[i]` inserirò tutti gli elementi con chiave uguale a `i`
	- nel senso, se io voglio ordinare una array di prodotti in base al loro prezzo, nella posizione `Y[4]` (che è di per sé una lista) metterò tutti i `record` (i prodotti) che costano 4.

- concateno le liste `Y[i]` in ordine, così da ottenere una array ordinato correttamente
![[bucketsort.gif]]

##### PSEUDOCODICE
```scss
BucketSort (X, k)
1. Sia `Y` un array di dimensione `k`
2. for i = 1 to k do          // creazione dell'array con liste vuote
3.	   Y[i] = lista vuota

4. for i = 1 to n do
5.	   appendi il record X[i] alla lista Y[chiave(X[i])]  
       // appendo (inserisco alla fine) l'elemento nella lista corretta

6. for i = 1 to k do
7.	   copia ordinatamente in `X` gli elementi della lista Y[i]
      // inserisco gli elementi nell'array originale nell'ordine corretto
```
- creo un array e ad ogni posizione creo una lista vuota
- faccio un for che si gira tutta la lista X mettendo il record $X[i]$ nella lista $Y$ in posizione $chiave$ 
- faccio un'altro for che sta volta metterà gli elementi di $Y[i]$ in $X$ nell'ordine corretto
#### COMPLESSITÀ
complessità uguale a integer sort $O(n+k)$ buona quando k è piccolo 

>[!info]- stabilità di un algoritmo
>tutte le volte che nell'input abbiamo due elementi con stessa chiave in output li troviamo messi 
>comunque nello stesso ordine in cui stavano
>>[!tip]- Esempio
>>Immagina di avere una lista del genere, sempre con prodotti e costi
>>`[Pane, 4`
>>`Pasta, 6`
>>`Yogurt, 4`
>>`Zucchine, 6`
>>`Carote, 4]`
>>
>>Se l'algoritmo è stabile, ordinando in base ai costi avremo
>>`[Pane, 4`
>>`Yogurt, 4`
>>`Carote, 4`
>>`Pasta, 6`
>>`Zucchine, 6]`

>[!question]- Algoritmo di bucket è stabile?
>Dipende dall'implementazione su come gestiamo le liste, ad esempio guala fa append in 
>ordine di lettura e le mette in ordine (nello pseudocodice questo avviene nelle righe `4-5`).
### Radix Sort
Il radix prende in input un vettore con k elementi e da in output quegli elementi
- definisco una base(importante per capire la complessità)
- prendo i numeri e li ordino dalla cifra meno significativa a quella più significativa
![[Pasted image 20241106172807.png]]
- andiamo avanti finché la cifra più significativa è 0 quindi non c'è e siamo alla fine
- Ogni volta che facciamo una passata di ogni cifra usiamo il bucket per ordinare dei record in cui la chiave sono i numeri di quella cifra e nella lista avremo gli altri numeri
- se abbiamo una base possiamo capire le chiavi in che range appartengono con $[0,b-1]$
### Dimostrazione di correttezza
dopo $t$ passate di bucket sort i numeri sono tutti ordinati rispetto alle ultime $t$ cifre meno significative
- prendiamo due numeri $x$ e $y$
- se siamo alla $t-esima$ passata avremo due casi
	- se sono uguali il bucket è stabile quindi saranno ordinati in base alle cifre meno significative controllate prima per induzione
	- se sono diverse il più grande verrà messo adeguatamente
- ordiniamo in ordine da dx->sx perché dobbiamo applicare un algoritmo stabile che non ci distrugge l'ordinamento precedente

#### Che succede se ho una base piccola?
faccio confronti meno costosi con basi più piccole ma magari ho numeri generalmente più lunghi quindi devo avere uno sweet-spot tra le due

#### Complessità Radix Sort
- se abbiamo una serie di numeri interi in $[1,k]$ il numero più grande è $k$ 
- se questi numeri saranno rappresentati con base $b$ per trovare il numero di cifre massimo di cui ho bisogno, devo fare la formula inversa di $b^{x}$ ovvero $x=log_bk$ 
	- In **base 10**, il numero **999** richiede 3 cifre (perché il massimo numero a 3 cifre in base 10 è 999), infatti $$log_{10}(999) \approx 3$$
		- In **base 2** (binario), il numero **7** richiede 3 cifre binarie (111 in binario è 7), infatti $$log_{2}(7) \approx 3$$
- quindi questo vuol dire che per ordinare completamente i numeri devo eseguire $log_{b}(k)$ passate di BucketSort
	- ad esempio se devo ordinare dei numeri in base decimale e il massimo è `999`, devo eseguire `3` volte il **BucketSort**

- ciascuna passata di **BucketSort** ha n record quindi costerà ogni passata $O(n)$
	- - $O(n)$ per distribuire `n` elementi nei bucket (ovvero scorro l'array originale e li inserisco in quello d'appoggio)
- Ogni bucket che abbiamo fatto è in un array d'appoggio e ora dobbiamo rimetterlo al suo posto $b$ volte, ovvero quante cifre abbiamo
	- avremo quindi un costo $O(b)$

- quindi sicuramente avremo $O(n+b)$

numero di passate=$O(log_bk)$
costo di ogni passata=$O(n+b)$

$numero \ di \ passate*il \ costo \ di \ ogni \ passata$
$$O((n + b) \times log_{b}(k))$$

### come scelgo b?
b lo scelgo grande più o meno quanti numeri sono 
![[Screenshot_2024-11-06-18-22-58-89_45415775811cea13943236d9369df411.jpg]]

### ESERCIZIO IN AULA
![[Pasted image 20241106182351.png]]
Strutture dati= oracolo perché risponde a domande(query)
Facciamo un IntegerSort che si ricorda quanti valori abbiamo nelle posizioni precedenti

![[Pasted image 20241106184353.png]]
- ad ogni passaggio sommo l'elemento precedente della struttura dati IntegerSort 
>[!info] ogni elemento a sua volta avrà la somma del precedente della somma del precedente ecc...
- metto $a-1$ perché devo contare anche in quel momento quanti numeri ho aggiunto


### ALTRO ESERCIZIO PER CASA
![[Pasted image 20241106184628.png]]
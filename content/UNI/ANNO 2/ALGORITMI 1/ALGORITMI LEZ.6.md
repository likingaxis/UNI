[[cap4.pdf|pdf della lezione 6]]
## Algoritmi di ordinamento
gli algoritmi di ordinamento hanno un insieme di n numeri in input e in output devono stamparli in ordine crescente quindi dove ogni numero precedente deve essere più piccolo del successivo
![[Pasted image 20241028115319.png|400]]

### Algoritmo 1 _**Selection Sort**_
- Algoritmo semplice da applicare ma poco efficiente
#### Come funziona?
Ci scorriamo il nostro array e ad ogni elemento facciamo un controllo su qual è l'elemento più piccolo in quella determinata posizione
![[Pasted image 20241028124756.png|500]]
![[selection-600.gif|400]]

#### PSEUDOCODICE
![[Pasted image 20241028123608.png|500]]

- Il primo ciclo for scorrerà tutto l'array partendo da una posizione definita
- Ad ogni posizione del primo ciclo for faremo un confronto tra tutti i successivi dettati da `j` e li confrontiamo con la posizione m, se troviamo un numero più piccolo di quello in posizione m la nuova m diventerà la posizione che abbiamo trovato essere la più piccola
- la m sostanzialmente indica lo smallest e la k del for iniziale i round(vedi gif sopra)
- sostituirà la posizione del più piccolo di quel momento con la posizione del successivo, quindi
- piccola precisazione, per il prof la posizione 0 non si scambia.
- n-2 alla condizione del primo for perché controllare l'ultima posizione è inutile
### Parentesi sulle _**invarianti**_
le invarianti sono delle proprietà che devono rimanere immutate nella fase di esecuzione dell'algoritmo e che ci servono per capire se un algoritmo è corretto perché permette di isolare proprietà dell’algoritmo, spiegarne il funzionamento, capire a fondo l’idea su cui si basa. 
in questo caso abbiamo due  _**invarianti**_ definite su un generico passo k:
1. i precedenti di $k+1$ sono già ordinati
2. i precedenti di $k+1$ sono gli elementi più piccoli dell'array

#### Complessità temporale del seguente algoritmo
Vedremo solo upper-bound e lower-bound
##### Nel caso di upper-bound
- il for sopra lo facciamo al più n volte 
- e quello dentro anche al più n volte in modo molto approssimato
per il nostro modello RAM ogni riga di codice ci costa tempo costante
noi avremo quindi 5 righe di codice che saranno eseguite al più $n^2$ volte
![[Pasted image 20241028151816.png|500]]
##### caso lower-bound
prendiamo per fare il lower-bound la parte che ci esegue più operazioni
- ovviamente è il for interno 
per calcolare il numero di passaggi dentro a quel for faremo una sommatoria che va da k=0 a n-2 ovvero il numero dei passaggi del for superiore,
successivamente so che il primo elemento dell'array non viene confrontato quindi ho n-1 confronti quindi so che il ciclo for dentro è $n-(k+2)$ ma visto che il nostro array lo prendiamo come se partisse da 1 sommiamo 1 e quindi avremmo $n-k-1$
![[Screenshot_2024-10-28-15-49-20-13_45415775811cea13943236d9369df411.jpg|500]]

quindi abbiamo in tutto $\Theta (n^2)$


### Algoritmo 2 _**Insertion Sort**_
- Algoritmo simile al precedente funziona tipo con le carte
#### Come funziona?
Si scorre l'array fino a n-1 confrontando l'elemento nella posizione corrente con i precedenti finché non trova un punto in cui risulta maggiore del precedente controllato
![[Pasted image 20241028160418.png|450]]

![[insertion-600.gif|400]]

#### PSEUDOCODICE

#### Complessità temporale del seguente algoritmo
$\Theta(n^2)$
### Algoritmo 3 _**Bubble Sort**_
- gli elementi più grandi vengono spinti verso destra confrontando gli elementi adiacenti tra loro
#### Come funziona?
Si scorre l'array n-1 volte per un numero di i volte, dovuto al fatto che dobbiamo ogni volta scorrere il nostro array diverse volte, ad ogni posizione nell'array confrontiamo il numero di quella posizione con il numero nella posizione precedente, e andiamo avanti così finché l'array non è ordinato
![[Pasted image 20241028163330.png|450]]
![[bubble-640.gif|400]]

#### PSEUDOCODICE


#### Complessità temporale del seguente algoritmo
$\Theta(n^2)$
## Algoritmi sotto il quadrato
### Algoritmo 4 _**Merge Sort**_
- Il merge sort è un algoritmo che applica il divide et impera e ha un costo più basso degli altri
#### Come funziona?
![[merge-sort-400.gif|center]]

PSEUDO-CODICE
```scss (MESSO A CASO)
MergeSort(A, i, f)
1.  if(i < f)  then
2.     m = PARTE_INFERIORE[(i + f) / 2]
3.     MergeSort(A, i, m)
4.     MergeSort(A, m+1, f)
5.     Merge(A, i, m, f)

6.  if(i = f) then return A[i] 
```
1. se gli indici `inizio < fine` entro nell'`IF`
2. trovo la metà
3. calcolo ricorsivamente il `MergeSort` della prima metà
    
    - fintanto che `i < f` (quindi fino a quando non ho UN SINGOLO ELEMENTO DA PASSARE AL `MERGESORT`) calcolo ricorsivamente;
    - quando ho un singolo elemento vuol dire `i = f`, quindi ritorno quel valore
    - a questo punto ho i risultati della riga 3 e 4 del penultimo MergeSort chiamato
    - ripercorro tutto tornando sopra e avrò il risultato finale della riga 3 chiamata la prima volta (in pratica ho la prima metà ordinata)
    
4. calcolo ricorsivamente il MergeSort della seconda metà
    
    - rifaccio la stessa cosa che ho scritto nel punto 3
    
5. QUANDO HO IL RISULTATO DEL PUNTO 3 E 4 posso eseguire il merge.

#### Algoritmo 4.5 _**Merge**_
- Il merge è quell'algoritmo che ci consente di fondere due array A e B e che sono entrambi ordinati singolarmente
##### Come funziona?
- estrai ripetutamente il minimo di A e B e copialo nell’array di output, finché A oppure B non diventa vuoto 
- copia gli elementi dell’array non vuoto alla fine dell’array di output
![[ciao/content/UNI/ANNO 2/ALGORITMI 1/fotoalg/ezgif.com-animated-gif-maker.gif]]
![[ezgif.com-animated-gif-maker 1.gif|500]]

##### PSEUDOCODICE
![[Pasted image 20241028222805.png|500]]
- La funzione Merge prende come argomento 
	- l'array($A$)
	- la posizione iniziale($i_1$)
	- la posizione al centro($f_1$) 
	- la posizione finale($f_2$)
- crea un array lungo quanto la posizione $finale-inizio+1$
- $i$ è uguale a $1$ perché alcune volte lo pseudo codice si fa con array che partono da $1$
- $k_1$ prende il valore iniziale $k_2$ prende il valore dell'inizio della seconda parte dell'array
- inseriamo gli elementi dei vari array scambiando in base alla necessità quale prendere in considerazione dei due per l'inserimento
	- ad ogni assegnazione nell'array incremento $i$ e $k_1$ se uso l'array1 oppure $k_2$ se uso array2
- se alla fine del for $k_1$ deve ancora finire di inserirsi del tutto metterò per completezza gli ultimi elementi alla fine dell'array, oppure copio gli ultimi elementi di $k_2$
- mettiamo x nelle posizioni dell'array che avevamo
- fine.
##### Complessità temporale del Merge
Ogni passaggio costa un elemento delle due sequenze che abbiamo che saranno rispettivamente lunghe $n_1$ e l'altra $n_2$, visto che ogni passaggio costa un elemento delle due avremmo sicuramente il while che costa tutto $n_1$ e un po' di $n_2$ oppure viceversa, poi i restanti elementi del vettore che manca da mettere dentro X saranno aggiunti con una funzione di copia che avrà tempo lineare 
quindi alla fine avremmo $\Theta (n_1+n_2)$

#### Complessità temporale del Merge Sort
Abbiamo due chiamate ricorsive che ogni volta diminuiscono proporzionalmente di $n/2$ e ad ogni chiamata di funzione faremo un merge che costa $O(n)$ $O$ perché alle ultime chiamate non facciamo esattamente n
poi applichiamo il teorema master per svolgere questa equazione di ricorrenza
![[Screenshot_2024-10-29-17-53-26-01_45415775811cea13943236d9369df411.jpg|500]]

#### Quanta memoria (ausiliaria) usiamo?
$\Theta(n)$ perché l'unica cosa che occupa memoria è la creazione dell'array ausiliario ad ogni chiamata del merge, ogni chiamata del merge avviene singolarmente e non se ne eseguono più di una nello stesso tempo perciò il costo rimarrà sempre $\Theta (n)$, anche se vedessimo il costo di tutte le chiamate contemporanee di merge sort avremmo $logn$ dato dal $T(n/2)$, comunque $logn$ è asintoticamente più lento di $n$ e quindi non lo consideriamo in memoria




### Algoritmo 5 _**Quick Sort**_
- Il quick sort è un algoritmo che ha un costo sotto $n^2$ e che usa la tecnica del **divide et impera**
#### Come funziona?
ricorsivamente chiamo _***Partition***_ dove si pone un perno e si fanno scorrere due controlli 
1. da sinistra verso destra dell'array controllo se il numero preso in quel momento è maggiore del perno
2. da destra verso sinistra dell'array se il numero preso in quel momento è minore del perno
se si verificano quelle condizioni avviene uno scambio tra i due 
![[quicksort-600-1.gif|500]]
##### Funzionamento algoritmo **Partition**
![[Pasted image 20241029194955.png|600]]

##### PSEUDOCODICE **Partition**
![[Pasted image 20241029200738.png]]
- ogni volta viene creato un perno $x$ dato dalla posizione $A[i]$
	- la parte inferiore è data da i
	- la parte superiore dalla fine +1
- facciamo un ciclo while che continua finché non si attiva il break
- abbiamo quei due cicli che dicevamo prima che scorrono da dx a sx e viceversa che si fermano se trovano una contraddizione della richiesta di una tipica lista ordinata
	- ha senso il fatto che da sx verso dx cerchi il maggiore perché così se abbiamo sempre numeri minori significa che siamo su un punto già ordinato e che non dobbiamo togliere
	- stessa cosa vale da dx a sx
- una volta terminato i due cicli procediamo a fare uno scambio se inf continua a essere più piccolo del sup(significa che i due non si stanno incrociando)
- se si incrociano usciamo e mettiamo il perno "al centro" ovvero il punto dove doveva stare perché sup sarà arrivato dove doveva arrivare
- restituiamo la posizione del perno
#### PSEUDOCODICE **Quick Sort**
![[Pasted image 20241029201649.png]]

Il quicksort principalmente serve per andare a fare il partition e le varie chiamate ricorsive una a sx dell'array e una a dx, partition ogni volta inserisce nella posizione corretta il perno mettendo nell'emisfero sinistro dell'array i numeri più piccini del perno e a dx i più grandicelli


##### Funzionamento algoritmo **Quick Sort**
![[Pasted image 20241030164542.png]]
- applica il partition e ordina in base al perno facendo quella cosa sx e dx
- chiama ricorsivamente due chiamate quick una con gli elementi a sx e una con gli elementi a dx del perno
- fa la cosa ricorsivamente modificando l'array
### Complessità
- Ad ogni invocazione il perno scelto in quel momento viene posizionato correttamente
- dopo n invocazioni di costo $O(n)$ ho il vettore ordinato, se lo vedessi su un albero farei $n*O(n)$ e quindi $O(n^2)$
- i due casi peggiori sono che ho il perno scelto come numero più piccolo o più grande in assoluto e quindi ho difficoltà a fare un confronto con il < o >
- quindi avrei complessità
$$T(n) = T(n-1) + T(0) + O(n)$$ $$= T(n-1) + O(1)+O(n)$$ $$= T(n-1) + O(n)$$
 $$= T(n) = O(n^2)$$
#### Caso Migliore
È facile intuire che il miglioramento di costo avviene quando le partizioni sono bilanciate ovvero il perno viene posto al centro dell'array, mentre all'aumentare dello sbilanciamento il tutto si complica.
#### Caso Medio

![[Pasted image 20241030180955.png]]
Nel caso medio si osserva che anche se il 90% degli elementi sta a sinistra del perno e il restante 10% a destra il QuickSort ha comunque un costo di $nlog(n)$
Tutti i vari casi medi dello stesso problema avranno la medesima altezza dell'albero.

#### quicksort randomizzato
- Scegli un perno a caso
- il costi non cambiano
- ma il caso medio non esiste
![[Pasted image 20241030181503.png|500]]

[[cap8.pdf|pdf della lezione]]
Il problema della coda con priorità in parte coperto con l'heap sort
#### Cosa è la Coda con priorità
un insieme di elementi $(elem,chiave)$ non si può fare la ricerca in tempo costante
Serve per mantenere l'insieme di elementi con una priorità dove di solito il più piccolo è quello con priorità maggiore. 
Nella maggior parte di questi algoritmi l'obiettivo è ricercare l'elemento con priorità maggiore
###### Operazioni possibili
- individuare la chiave minima `findmin()` in S 
- inserire in $S$ l'elemento e con chiave $k$ `insert(elem e,chiave k`
- cancellare un elemento, mi aspetto un riferimento all'elemento diretto, quindi un indirizzo o qualcosa che sicuramente intende QUELLO `delete(elem e)`
- cancellare il minimo, cancellare da S l'elemento con chiave minima `deleteMin()`
OPERAZIONI AGGIUNTIVE
- aumentare la chiave di un elemento $increaseKey(elem e,chiave d)$
- diminuire la chiave di un elemento $decreaseKey(elem e,chiave d)$
- operazione di merge tra due code $c_3=c_2+c_1$ `merge(codapriorità c1, codapriorità c2)`

##### A che cazzo servono?
per fare altri algoritmi che vedremo poi 
ad es: calcolo cammini minimi di un grafo


>[!BUG]- se proviamo a implementare la coda priorita con
>- array
>- liste
>ci sara una roba simile con i dizionari con una determinata struttura dati ho qualcosa lineare e costante(tabella)
>![[Pasted image 20241203185820.png|600]]
>noi invece vogliamo tutta la roba costante

>[!success]- tre implementazioni evolute che vedremo passo passo nel corso di questa lez
>- d-heap
>- Heap binomiali
>- Heap di Fibonacci(cenni)

#### d-heap
###### Definizione d-heap
>[!info]- gli heap si dividono in 
>min heap e max hip, uno se vogliamo estrarre con più facilità i min e uno i max

ora per tutta la lezione ci baseremo con la definizione di min heap
- un albero d-ario
- è completo fino al penultimo livello 
- tutte le foglie sono compattate a $sx$
- ogni nodo $v$ contiene un elemento ed una chiave presa da un dominio ordinato
- vige questa regola: per ogni nodo diverso dalla radice $chiave(v)$ $\geq$  $chiave(parent(v))$ 
noi in passato abbiamo visto il max heap
##### Esempio di albero d-ario con d=3 e 18 nodi
![[Pasted image 20241203190544.png]]

###### Proprietà del d-heap
- con n nodi è alto $\Theta(log_dn)$
	- usiamo d per compattare o meno l'altezza dell'albero
- la radice contiene l'elemento con chiave minima
- rappresento con vettore posizionale


CI SONO DELLE PROCEDURE AUSILIARIE SIMILI AL NOSTRO VECCHIO AMICO FIXHEAP

1. MUOVI ALTO
		serve per ripristinare le proprietà dette prima
		scambia gli elementi andando in alto ripristinando le cose
		costano l'altezza dell'albero $O(log_dn)$

![[Pasted image 20241204165409.png|600]]

>[!info]- esempio grafico
>![[Pasted image 20241204170116.png|600]]
>- passo 1 scambio 6 con 10
>- passo 2 scambio 6 con 9


2. MUOVI BASSO
		fa una cosa simile ma scende in basso
		questo deve pure scendere nei vari sotto alberi ricorsivamente quindi $O(dlog_dn)$
		
![[Pasted image 20241204165449.png|600]]
prendi il figlio $u$ con la chiave più piccola del nodo $v$, verifica se v non ha figli oppure se la condizione comunque è verificata, sennò scambia i due
il codice tiene il riferimento diretto e quindi ogni volta prende il nodo che in caso ipotetico scende giù


>[!info]- esempio grafico
>![[Pasted image 20241204172118.png|600]]
>- passo 1 controllo i figli del primo livello
>- passo 2 scambio 10 con 6
>- passo 3 faccio confronto del min tra 9 e null (i figli di 10)
>- passo 3 scambio 10 e 9




#### APPLICHIAMO LE FANTOMATICHE PROPRIETA CON IL D-ARIO
##### findmin
ez tocca solo prende la radice
![[Pasted image 20241204172827.png]]
###### costo: costante$O(1)$
##### inserimento elemento
devo rispettare la proprietà che il penultimo livello deve essere completo e che devo essere compattato a sx
quindi metto 8 all'ultimo livello disponibile piu a sinistra
poi faccio fix muovi alto
`insert(e,8)`
![[ezgif.com-crop.gif]]
###### costo: $O(log_dn)$

###### cancellare un elemento
sostituisco con l'ultima foglia l'elemento che voglio eliminare e faccio un fix in base alle necessità
- se sei un'anomalia che va messa in alto fai muovi alto
- se sei un'anomalia che va spostata in basso fai muovi basso
fix dall'alto:
![[ezgif.com-speed_8.gif|600]]

fix dal basso:
![[ezgif.com-speed_7.gif|600]]
###### costo: $O(dlog_dn)$ oppure $O(log_dn)$

viene usato anche per **<font color="#c0504d">cancellare il minimo</font>** prendendo la radice
COSE AGGIUNTIVE
###### decremento chiave
prendiamo un elemento lo decremento e faccio muovi in alto 
![[pages_32_to_36_looping-ezgif.com-speed.gif|600]]
###### costo: $O(log_dn)$
###### incremento chiave
![[pages_38_to_42_looping-ezgif.com-speed.gif|600]]
incremento e muovo in basso
###### costo: $O(dlog_dn)$ 
###### merge costosa con il d-heap
fare il merge con il d-heap non è il massimo
- si distruggono le due code e se ne crea una nuova con entrambe
- perche farli esplodere entrambi se posso scegliere chi è più piccolo e aggiungerlo volta per volta delle due strutture
1) faccio una sorta di heapify O(n)
- genero un heap d-ario partendo da tutti gli elementi di $c_1$ e $c_2$
- mette gli elementi in questa nuova coda e poi fa una sorta di heapify muovendo in basso dalla radice
![[Pasted image 20241204182043.png|500]]

2) nel secondo caso faremo k inserimenti in un d-heap con n elementi
	- $k=min \{ |c_1|,|c_2| \}$ e $n=|c_1|+|c_2|$
![[Pasted image 20241204182637.png|600]]

>[!attention] i due costi dipendono dalla dimensione del d-heap


|                                         | Find Min | Insert        | Delete          | DelMin          | Incr. Key       | Decr. Key     | Merge  |
| --------------------------------------- | -------- | ------------- | --------------- | --------------- | --------------- | ------------- | ------ |
| **Array non ord.**                      | Θ(n)     | O(1)          | O(1)            | Θ(n)            | O(1)            | O(1)          | O(n)   |
| **Array ordinato**                      | O(1)     | O(n)          | O(n)            | O(1)            | O(n)            | O(n)          | O(n)   |
| **Lista non ordinata**                  | Θ(n)     | O(1)          | O(1)            | Θ(n)            | O(1)            | O(1)          | O(1)   |
| **Lista ordinata**                      | O(1)     | O(n)          | O(1)            | O(1)            | O(n)            | O(n)          | O(n)   |
| **<font color="#c0504d">d-Heap</font>** | $O(1)$   | $O(log_d(n))$ | $O(d log_d(n))$ | $O(d log_d(n))$ | $O(d log_d(n))$ | $O(log_d(n))$ | $O(n)$ |

#### NON CI ACCONTENTIAMO QUINDI FACCIAMO Heap binomiali
##### come è fatto
prima definiamo un concetto di un albero binomiale $B_i$
è definito ricorsivamente  sapendo che $B_0$ è un nodo unico
e invece i successivi saranno il merge dei precedenti 
$B_{i+1}=B_i+B_i$  il figlio di una radice sarà l'altro albero
![[Pasted image 20241204185758.png]]
##### proprietà strutturali abbiamo $B_i$
- nodi $2^i$ 
- il grado della RADICE è $log_2n$
- altezza =h=$log_2n$
- figli della radice sono i sottoalberi quindi tipo $B_4$ avrà come sottoalberi $B_3, \ B_2,\  B_1$

>[!success] un  heap binomiale è una foresta di alberi binomiali

- nella foresta possiamo avere massimo un albero di una determinata dimensione $i$ quindi un unico $B_i$ 
- ogni nodo $v$ contiene un elemento e una rispettiva chiave
- Bisogna anche qui rispettare l'ordinamento heap per ogni nodo v diverso dalla radice 
	- $chiave(v)$ $\geq$ $chiave(padre(v))$
###### ESEMPIO
esempio di un heap binomiale con $n=13$
![[Pasted image 20241204191336.png]]
>[!question]- con quanti alberi binari diversi posso rappresentare n nodi?
>rappresento in binario il numero di nodi ad esempio $13=2^0+2^2+2^3$ -> 1101
>infatti avremo $B_0 \rightarrow  B_2 \rightarrow B_3$
>![[Pasted image 20241204191831.png|400]]
>- Poiché la rappresentazione binaria di un numero n ha al massimo $\lceil log_2n \rceil$ bit, vi saranno **al più $\lceil log_2n \rceil$ alberi** nella foresta.
>	- ne consegue che in un heap binomiale abbiamo al più $\lceil logn \rceil$ alberi binomiali ognuno con altezza $O(logn)$ perché crescono logaritmicamente rispetto a $n$
###### come si rappresentano
con una struttura collegata con puntatori
![[Pasted image 20241204192625.png]]
##### Tutte le procedure 
con una funzione ausiliaria potrò fare tutto
###### Ristruttura
![[Pasted image 20241204194335.png]]
cerca di sistemare una foresta con alberi binomiali non unici
- faccio una sorta di merge degli alberi vicini
	- tipo prendo i primi 2 
	- poi prendo i successivi 2 rispettando sempre la regola del max e min
	- ogni volta che li fondo diminuisco di 1 gli alberi
quindi faro un numero di fusioni lineari al più come il numero di alberi
$T(n)$-> il numero di alberi è $O(log(n))$
![[Pasted image 20241204194459.png]]

data una foresta $H$ con $n$ nodi ciascuno contiene elemento e chiave 

##### findmin
scorre tutte le radici che tanto sono quelle il min
##### inserimento 
aggiunge ad $H$ un nuovo $B_0$ $(elem \ e, chiave \ k)$e poi fa ricostruisci
###### Cancellazione minimo
elimino la radice di un albero, che a sua volta si spezzerà in sotto alberi, aggiungo tutti questi alberi in $H$ e faccio ricostruisci
![[Pasted image 20241204195300.png|400]]

###### Decremento chiave
decrementi e fai muovi in alto del singolo alberello $O(log_n)$ altezza albero
![[slides_65_66_slower_looping-ezgif.com-speed.gif|500]]
###### Cancellazione 
richiamo decreaseKey finche non diventa il minimo e faccio la cancellazione del minimo perché diventa il minimo $O(logn)$
###### incremento chiave
faccio delete e poi inserisco l'elemento con la chiave aggiornata
###### merge
aggiungo la foresta e faccio ristruttura
![[Pasted image 20241204195337.png|400]]
### Heap di Fibonacci
>[!warning] bisogna sapere solo cosa è e quanto costa


inventato da Tarjan esperto di strutture dati
![[tarzan-jump.gif]]

il concetto principale è: perché fare subito le ristrutturazioni quando potrei farle alla fine?

|                      | FindMin  | Insert   | Delete    | DelMin    | IncKey    | DecKey   | Merge    |
| -------------------- | -------- | -------- | --------- | --------- | --------- | -------- | -------- |
| **d-Heap (d cost.)** | O(1)     | O(log n) | O(log n)  | O(log n)  | O(log n)  | O(log n) | O(n)     |
| **Heap Binom.**      | O(log n) | O(log n) | O(log n)  | O(log n)  | O(log n)  | O(log n) | O(log n) |
| **Heap Fibon.**      | O(1)     | O(1)     | O(log n)* | O(log n)* | O(log n)* | O(1)*    | O(1)     |

quelle con asterisco indicano che quella non è la complessità nel caso peggiore ma la complessità in senso ammortizzato(solo intuizione)
###### Costo ammortizzato
Il costo ammortizzato di un’operazione è il costo “medio” rispetto a una sequenza qualsiasi di operazioni
Quando facciamo una serie di operazioni e calcoliamo il costo alla fine
in casi in cui facessimo $k$ operazioni, se ha costo ammortizzato costante avrò $O(k)$
Molto utile quando si vogliono buone prestazioni sull’intera sequenza e non garanzie sulla singola operazione – esempio: progettare algoritmi veloci attraverso strutture dati efficienti

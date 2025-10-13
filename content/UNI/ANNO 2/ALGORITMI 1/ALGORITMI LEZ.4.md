[[cap2.pdf|pdf della lezione 4]]
### Esercizio per casa
==N-1n/2==

## ALGORITMI DI RICERCA
##### ALGORITMO DI RICERCA DI UN ELEMENTO IN UN ARRAY NON ORDINATO
- alg1. Scorriamo tutto il vettore finché  non troviamo il numero
![[Pasted image 20241020115403.jpg|500]]

$T_{worst}=n$ ovvero n passaggi del for nel caso peggiore
$T_{avg}=n+1/2$
>[!question]- pk n+1/2?
>![[Screenshot_2024-10-21-10-13-51-39_51606159b24eff83e24a54116878fe3e.jpg|400]]

Quindi
$T_{worst}=\Theta n$
$T_{avg}=\Theta n$
##### ALGORITMO DI RICERCA DI UN ELEMENTO IN UN ARRAY ORDINATO BINARIA
Tecnica divide and conquer
Parto con una una posizione nel mezzo dell'array e confronto ricorsivamente se ci troviamo dopo o prima della nostra posizione attuale, così da ridurre le possibili "celle" dell'array da cercare
- i e j sono degli indici 
- la funzione è di tipo ricorsivo

![[Pasted image 20241020122910.jpg|500]]
>[!example]-
>![[6dfb4b_66a3da91653a4291a160c17419a4d20c~mv2.gif|400]]

 $T(n)=T(n/2)+O(1)$
 $T(n)=log_n$
 >[!question]- perchè log?
 >Per spiegarlo mi riprendo alle slide del prof della [[ALGORITMI LEZ.2]]
 >L'obiettivo è quello di usare lo srotolamento srotolando n/2 portando le cose al passo i
 >Se mi aprissi la $T$ avrei ogni volta degli $O(1)$
>![[Pasted image 20241020131812.png|500]]
 
 ##### LE EQUAZIONI DI RICORRENZA
Le equazioni di ricorrenza servono per calcolare i relativi costi computazionali di algoritmi ricorsivi.
Le abbiamo usate fino ad ora e si possono svolgere in diversi modi
### Metodi per svolgere equazioni di ricorrenza

#### Metodo dell'iterazione
**Obiettivo: srotolare la ricorsione finché non arrivi ad avere $T(1)$**
>[!info]- ESEMPIO 1:
>![[Pasted image 20241021110819.png|500]]

>[!info]- ESEMPIO 2:
>![[Pasted image 20241021110748.png|500]]

>[!info]- ESEMPIO 3:
>![[Screenshot_2024-10-21-11-05-00-69_51606159b24eff83e24a54116878fe3e 1.jpg|400]]
>quindi alla fine scappa fuori $\Theta (1)$
>

>[!question]- Esercizi per casa su questo metodo
>![[Pasted image 20241021111535.png|300]]
>
>
>
>![[Screenshot_2024-10-21-21-28-38-56_45415775811cea13943236d9369df411.jpg|400]]
>
>![[Screenshot_2024-10-21-22-20-58-15_45415775811cea13943236d9369df411.jpg|500]]
#### Metodo dell'albero della ricorsione
**Obiettivo: disegnare un albero con tutte le varie chiamate ricorsive indicando la dimensione di ogni nodo e stimare il costo di ogni nodo e sommarlo con tutti i nodi**
- T(n) è proporzionale al numero di nodi
>[!info]- ESEMPIO 1:
>![[Screenshot_2024-10-21-11-36-46-78_51606159b24eff83e24a54116878fe3e.jpg|460]]
>l'albero ha n nodi $\Theta (n)$ per il discorso della proporzionalità

>[!info]- ESEMPIO 2
>Simile all'esempio 1 ma avremmo un costo per nodo al più n quindi con un upper-bound con $O(n^2)$
>ora si chiede se è un $\Theta$ per dimostrarlo userà il doppio confronto con $\Omega$
>![[Pasted image 20241021115134.png]]
>per dimostrare l'omega si prende la metà superiore dei nodi e definisce che ognuno di quei nodi costa almeno n/2, poi moltiplica il num di nodi per il costo di ogni nodo e visto che esce $\ge$ 
>useremmo $\Omega$ 

>[!info]- ESEMPIO 3
>h è uguale al cammino(num collegamenti) più lungo quindi n-1
>![[Pasted image 20241021122450.png|600]]
>per fare $T(n)$ moltiplica la somma dei nodi con il costo di ogni nodo sostituendo ad h l'altezza
>![[Pasted image 20241021122611.png]]

>[!info]- ESEMPIO 4
>uguale all'esempio 3 ma con costi di un nodo con n
>visto che abbiamo n il costo è al più n quindi useremo $O$ 
>![[Pasted image 20241021122821.png]]

>[!info]- ESEMPIO 5
>Per definire il costo di un algoritmo uso un'altro algoritmo come confronto
>![[Pasted image 20241021152247.png|500]]
>![[Pasted image 20241021152606.png|500]]

>[!question]- esercizi per casa su questo metodo
>![[Pasted image 20241021152723.png|300]]
>
>per Esempio 1 fare 

>[!bug] il professore ogni volta che ha dei log in qualche base visto che la base è una non la scrive

>[!info]- ESEMPIO 6
>![[Pasted image 20241021162931.png]]
>ci rendiamo conto che a sx scende di meno di quello a dx e che a sx cresce con i fratti di 3 invece a dx con i fratti di 2/3 per dei calcoli matematici sx log3 e dx log 3/2
>moltiplicheremo il costo di ogni livello per i livelli dell'albero con upper-bound quindi con il ramo che si estende di più a dx
>![[Pasted image 20241021163256.png]]
>per fare il lower-bound bisogna invece prendere i rami più corti e moltiplicarli sempre con i costi di ogni livello quindi al più n
>una volta verificati entrambi potremmo dire che si parla di $\Theta$

altri metodi sulla [[ALGORITMI LEZ.5|lezione 5]]

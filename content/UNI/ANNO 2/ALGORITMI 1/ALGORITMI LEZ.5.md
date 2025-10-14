[[cap2.pdf|pdf della lezione5]] (31)
I due metodi visti in precedenza sono intuitivi e semplici ma a volte rischiosi perché poco preciso.
Ci sono altri metodi più precisi
## Metodo della sostituzione
Abbiamo una equazione di ricorrenza, prima dobbiamo intuire la forma della soluzione al livello asintotico(guess)
1. abbiamo una equazione di ricorrenza 
2. troviamo una forma della soluzione al livello asintotico(guess) ad es.$O(n^3)$
3. utilizziamo l'induzione per verificare l'ipotesi
4. risolviamo per le costanti
>[!tip]- come posso capire la mia ipotesi?
>- utilizzo in modo raffazzonato le conoscenze che ho dagli esercizi precedenti con equazioni di ricorrenza simili e faccio una stima dell'andamento della funzione
>- vado a tentativi partendo da una O meno efficiente

>[!info]- esempio 1
>Poniamo un upper-bound molto generico e prendiamo la sua c per evitare di fare notazioni asintotiche nelle induzioni che sono estremamente difficili
>
>![[Screenshot_2024-10-22-19-28-49-14_45415775811cea13943236d9369df411.jpg|600]]
>faccio il passo base e pongo $T(n)$ in base alla mia ipotesi(cerchio in blu)
>per il passo induttivo pongo una k esprimerlo
>sostituisco c alla mia T nella parte destra e raccolgo per escludermi la n
>

>[!info]- esempio 2
>Il goal è vero se e solo se il residuo è $\geq 0$ perché significherebbe che ho una cosa più 
>grande del mio upper-bound(goal) che mi sono posto 
>Al posto di T(n/2) sostituire c k al cubo
>![[Screenshot_2024-10-22-22-01-39-98_45415775811cea13943236d9369df411.jpg|500]]

>[!info]- esempio 3
>= a esempio 2 ma con $O(n^2)$
>La dimostrazione non si riesce a chiudere quindi non posso concludere né che sia vera né
>che sia falsa non funziona perché l'ipotesi induttiva non è abbastanza grande, 
>![[Pasted image 20241023112920.png|400]]
>conviene usare qualcosa di più forte quindi proviamo a dimostrare per qualcosa che ci fa uscire una cosa maggiore per mangiare il termine che ci dava fastidio
>
>![[Screenshot_2024-10-23-11-27-46-80_45415775811cea13943236d9369df411.jpg|500]]

Mettiamo che si scopre che l'algoritmo costi O(n^3) ma poi si scopre che valga anche O(n^2) per farlo non c'è un modo per capirlo subito ma bisogna andare a tentativi con tecniche di analisi per un algoritmo
## Tecnica del divide et impera
la tecnica del divide et impera si utilizza il 99% delle volte per una forma di questo tipo
- dividi il problema (di dimensione n) in a sotto-problemi di dimensione n/b 
- risolvi i sotto-problemi ricorsivamente - ricombina le soluzioni
![[Screenshot_2024-10-23-11-38-58-82_45415775811cea13943236d9369df411.jpg|500]]
>[!info]- problema di Fibonacci6 con divide et impera
>![[Pasted image 20241023114352.png|500]]
>
>![[Screenshot_2024-10-23-11-42-27-62_45415775811cea13943236d9369df411.jpg|500]]
>una vola trovata l'equazione di ricorrenza possiamo procedere ad individuare $a,b\ e\ f(n)$

>[!tip] la tecnica del divide et impera riguarda la suddivisione in $a,b\ e\ f(n)$

### teorema master enunciato(easy)
- Noi facciamo un confronto asintotico su chi va più velocemente a infinito tra una funzione che ci creiamo basandoci sulla suddivisione del divide et impera e una $f(n)$
	- Se hanno stesso ordine asintotico → $T(n)$ $=$ $\Theta$ $(f(n) \ log \ n)$ 
	- Se una delle due è “polinomialmente” più veloce → T(n) ha l’ordine asintotico della più veloce
![[Screenshot_2024-10-23-11-59-54-17_45415775811cea13943236d9369df411.jpg|400]]
##### Entrando un po' più nello specifico avremo i seguenti casi
![[Screenshot_2024-10-23-12-27-58-82_45415775811cea13943236d9369df411.jpg|600]]
Enunciato hard teorema master sul libro → non chiederà la dimostrazione

>[!info]- ESEMPIO 1 
>Definisco  $a,b\ e\ f(n)$
>faccio un confronto asintotico e sono identici
>Ovviamente esce theta di $nlogn$
>![[Screenshot_2024-10-23-12-38-18-62_45415775811cea13943236d9369df411.jpg|500]]

>[!info]- ESEMPIO 2
>facciamo i passaggi uguali all'esercizio precedente solo che ora ha vinto $n^{1/2}$ e quindi rientriamo nel caso 1
>![[Screenshot_2024-10-23-12-52-44-04_45415775811cea13943236d9369df411.jpg]]

>[!info]- ESEMPIO 3
>rivedere meglio la parte finale
> ![[Screenshot_2024-10-23-13-01-29-89_45415775811cea13943236d9369df411.jpg]]

>[!info]- Esempio 4
>non si può fare il teorema master perchè al variare di $\epsilon$ cambia il confronto asintotico
>![[Screenshot_2024-10-23-13-15-11-25_45415775811cea13943236d9369df411.jpg]]

>[!info]- ESEMPIO 5
>Nlogn +2tn/2
>Uso il caso 3 ma non scappa bene quindi non ci dice la soluzione
## Cambio di variabile
Presto lo dimenticheremo ci dobbiamo solo ricordare questo esempio e basta (GODO)
- effettuo una sostituzione di variabile per ricondurmi a una forma nota
- una volta rappresentata la sostituzione ne effettuo un'altra con R(x) per rappresentarla consiglio di vedere gli argomenti della funzione $R$ rispetto a $T$ 
- ora sono in una forma notevole che già conosco e costa $O(log \ x)$
- sostituisco la x con la vera x
- fine
![[Pasted image 20241023132417.png|700]]

>[!question]- due problemi per casa
>
>- 1 algoritmo ricorsivo e analisi con equazioni di ricorrenza
>
>- 2 trovare un algoritmo ricorsivo e vedere quanti spostamenti fa con equazioni ricorrenza ecc

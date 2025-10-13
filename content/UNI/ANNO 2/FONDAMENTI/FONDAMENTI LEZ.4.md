# Diversi tipi di macchine
- Macchine con testine indipendenti e tanti nastri
- Macchine con tanti nastri e testine solidali
- Macchine con un solo nastro 
- Macchine con alfabeto con tanti simboli
- Macchine con alfabeto binario
e si dimostra che <font color="#c0504d">“tutto quello che riusciamo a fare con una macchina di uno qualsiasi di questi modelli, riusciamo a farlo anche con una macchina di uno qualsiasi degli altri modelli”</font>
## Teorema 1
![[Pasted image 20250313175828.png]]
## Dimostrazione testine solidali=indipendenti
È ovvio definire che una macchina con testine indipendenti può lavorare come una macchina con testine solidali ma dimostriamo l'opposto con una macchina con 2 nastri con testine solidali
Sia T una macchina a 2 nastri con testine indipendenti una sua quintupla è 
$< q1 , (a,b), (c,d), q2 , (m1,m2) >$dove $m1$ è il movimento della testina sul primo nastro e $m2$ è il movimento della testina sul secondo nastro 
Trasformiamo questa quintupla in una serie di quintuple che possono funzionare su più nastri con una macchina con testine solide
la serie di quintuple ci riporta a voler shiftare prima un nastro poi l'altro della direzione desiderata per poi rimettere le testine in modo correndo usando un terzo nastro per il pinning

![[Pasted image 20250313174900.png]]
In questo caso stiamo parlando di una simulazione a scatola aperta
- per quella chiusa si intendeva quando fai una simulazione ma non sai precisamente come sono fatte le macchine che utilizzerai ma sai solo le specifiche
- in questo caso fai una simulazione cercando di emulare un'altra macchina che funziona in modo diverso
Su questa tecnica è basata la dimostrazione di un sacco di teoremi che vedremo in questo corso 
- fra i quali gli altri due che seguono
>[!tip]- un po di esempi dei passaggi per le quintuple di T'
>![[Pasted image 20250313180548.png|500]]


## Teorema 2
![[Pasted image 20250313180621.png]]
### Dimostrazione di una macchina $T_3$ che funziona su $T'$
Scriviamo un indirizzo(colonna) di $T_3$  per lungo
$T_3$ ha come procedura definita questa quintupla
$\langle \mathbf{q}_1, (\mathbf{x}_{11}, \mathbf{x}_{12}, \mathbf{x}_{13}), (\mathbf{y}_{11}, \mathbf{y}_{12}, \mathbf{y}_{13}), \mathbf{q}_2, m \rangle$

![[Pasted image 20250313181218.png]]
quello che faccio con la mia macchina $T'$ è andare a salvarmi tutti i singoli stati che si conseguono per fare una sorta di lettura continua
appena verifico che ho letto x11 x12 e x13 allora significa che posso procedere con la scrittura delle varie y definendo quanto tornare indietro 
![[Pasted image 20250313183736.png|700]]
#### Passaggio per poi andare a fare la write e i vari spostamenti a sinistra
![[Pasted image 20250313183802.png|700]]
#### Scrittura con i vari spostamenti a destra
![[Pasted image 20250313184300.png]]
>[!tip]- esempi quintuple che farebbe T'
>![[Pasted image 20250313182905.png]]
>- il nastro inizialmente aveva a1 b1 c1 ma poi viene modificato con le varie lettere greche
>- scrive gli stati con la potenza e non come 5 elemento

## Teorema 3
![[Pasted image 20250313184955.png|600]]

Mi raccomando usare la parola <font color="#9bbb59">CODIFICA</font>
Usiamo anche qui una macchina che simula la macchina con più lettere
![[Pasted image 20250313190613.png]]
Cominciamo con lo scrivere sui k nastri di $T_{01}$ la codifica binaria dell’input scritto sull’unico nastro di $T$
![[Pasted image 20250313191431.png]]
ovviamente sarà $log_2 8=3$ 
![[Pasted image 20250313192051.png]]
Questo è il risultato della macchina dove
b1(a) significa la prima cifra di a ovvero 0 e così via per ogni nastro su cui siamo posizionati

Quando una macchina fa le stesse cose di una macchina si esprime con
>[!quote] l’esito della computazione di una macchina su un input coincide con l’esito della computazione dell’altra macchina sullo stesso input (eventualmente codificato)

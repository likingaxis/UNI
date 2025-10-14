[[cap6.pdf|pdf della lezione]]
Questa lezione è un continuo della [[ALGORITMI LEZ.11|lezione 11]]

nella lezione precedente abbiamo visto i BST(alberi binari di ricerca)
con i BST il problema è che non abbiamo controllo sull'altezza dell'albero e quindi potremmo avere un albero sbilanciato
#### Alberi AVL per avere una struttura che sia alta sempre $O(logn)$
sono come alberi BST ma hanno dei **<font color="#ff0000">fattori di bilanciamento</font>**
- un **<font color="#ff0000">fattore di bilanciamento</font>** $\beta(v)$ può essere visto come un campo aggiunto a il singolo nodo 
- si calcola per ogni nodo facendo $Altezza \ sottoalbero\ sinistro \ \ - \ \ Altezza \ sottoalbero \ destro$

>[!warning] un albero è bilanciato se ogni nodo ha 
>|fattore di bilanciamento| $\leq 1$


#### ESEMPIO 1 è un AVL?
![[Pasted image 20241127154705.png]]
possiamo notare che le foglie hanno $\beta(v)= 0$
e essendo completo ogni sottoalbero $sx$ e $dx$ se viene sottratto per trovare il bilanciamento darà $0$
#### ESEMPIO 2 è un AVL?
![[Pasted image 20241127154954.png]]
la foglia sarà sempre $0$ ma il nodo 20 ha $\beta=2$ che è $> \ di \ 1$ quindi <font color="#ff0000">non è bilanciato</font>


#### ESEMPIO 3 è un AVL?
![[Pasted image 20241127155238.png]]
si è un AVL perché ogni nodo ha $\beta \leq 1$

### DIMOSTRARE CHE UN ALBERO AVL con n nodi ha altezza $O(logn)$
Anche se abbiamo degli alberi che sono estremamente sbilanciati essi saranno comunque $O(log(n))$.
###### ESEMPIO DI ALBERO SBILANCIATO
- Un albero sbilanciato è un albero che massimizza l'altezza in base al numero di nodi: 
	- ad esempio. se ho 6 nodi voglio avere l'albero più alto possibile.
potrei vederlo in modo un po' opposto per creare un albero sbilanciato:
- CERCO DI CREARMI UN ALBERO PARTENDO DA UNA ALTEZZA PREFISSATA E METTO UN NUMERO DI NODI MINORE POSSIBILE 
in poche parole pochi nodi altezza un botto
Questo tipo di albero sbilanciato si chiama di <font color="#f79646">Fibonacci</font> (vedremo perché)
#### Albero sbilanciato di <font color="#f79646">Fibonacci</font>
##### come è fatto?
![[Pasted image 20241127160149.png]]
- se dopo l'ultimo step togliamo un nodo cambia la sua altezza e potrebbe diventare sbilanciato
	- l'altezza di un albero deve rimanere invariata 
##### Rappresentazione dei primi 5 alberi di Fibonacci 
![[Pasted image 20241127160435.png]]
- sono $T_i$ dove $i$ è l'altezza
praticamente possiamo notare che per fare $T_h$ dovremmo porre
- una radice
- a $sx$ $T_{h-1}$
- a $dx$ $T_{h-2}$
![[Pasted image 20241127161302.png|280]]
ecco perché di Fibonacci perché è tipo la somma dei precedenti
###### Come trovare il numero di nodi $n_h$ di un albero $T_h$di Fibonacci?
per trovarlo si fa $n_h=F_{n+3}-1$ dove F è la funzione di Fibonacci
##### Per dimostrare questa cosa di $n_h$
si prova a fare per induzione
poniamo come induzione che
$n_h=1+n_{h-1}+n_{h-2}$
il che effettivamente ha senso perché noi sostanzialmente ad ogni albero andiamo ad aggiungere la radice e i nodi dei due precedenti
>[!info] N.B Un albero AVL con n nodi ha altezza h=O(log n)

per dimostrarlo andiamo a rivedere questa formula
$n_h=F_{n+3}-1$ notando che $F_{n+3}-1=\Theta(\phi^h)$ dove $\phi^k=F_k \ e \ \phi \ è \ la \ sezione  \ aurea \ 0,618...$
cercando una relazione tra altezza e numero di nodi
possiamo dire che $h$ è uguale a $O(log \ {nh})$ e quindi sarà $O(log n)$ 
il numero di nodi di un albero di Fibonacci è $O$ del numero di nodi n di un generico albero AVL

#### POSSO IMPLEMENTARE L'AVL PER UN DIZIONARIO?
la risposta è si perché stiamo comunque parlando di un albero BST
##### METODI GIÀ VISTI MA CON AVL

###### SEARCH
per la ricerca non fa niente perché e uguale ad un [[ALGORITMI LEZ.11#<font color=" d83931">LA RICERCA</font>|BST]]


quello che cambia invece con altri metodi è che potrei incorrere in sbilanciamenti 
- aumentati di 1(insert) o sottratti di 1(delete)
	- i nodi presi in causa saranno quelli del sottoalbero preso in considerazione
###### INSERT e DELETE
![[Pasted image 20241127164515.png|500]]
potrei incorrere in sbilanciamenti 
- aumentati di 1(insert) o sottratti di 1(delete)
	- i nodi presi in causa saranno quelli del sottoalbero preso in considerazione

>[!success] per risolvere questi sbilanciamenti devo fare delle operazioni di rotazione dei nodi 
>![[Pasted image 20241127171454.png]]
>
> il trucco per capire la rotazione e spostare la radice a sx o dx e sostituire con il nodo sotto.  una 
> volta fatto rimettere tutto in ordine logico
> costo della rotazione:tempo costante $O(1)$

##### ROTAZIONI SU NODI
Ci sono 4 tipi di sbilanciamenti
che vertono su nodi v con profondità massima che hanno bilanciamento +-2
per ribilanciare devo andare a modificare il sottoalbero T del nodo v

ci sono 4 casi del sottoalbero T
![[Pasted image 20241127175545.png]]
##### CASO SS
![[Pasted image 20241128101018.png|400]]
il coso grigio indica 2 casi che vedremo poi
abbiamo delle altezze definite
- L’altezza di $T(v)$ è $h+3$, 
- l’altezza di $T(u)$ è $h+2$, 
- l’altezza di $T3$ è $h$,
- l’altezza di $T1$ è $h+1$ con $\beta(v)=+2$ e 
- lo sbilanciamento è provocato da $T_1$ poiché aumenta l'altezza di 1 e facendo la sottrazione dei due sotto nodi di v avremo 2
se noi abbiamo il problema a $sx$ dovremmo ruotare a $dx$
ora per definire $T_2$ ci sono 2 sotto casi possibili: 
![[Pasted image 20241127180648.png]]
**(i)** l’altezza di $T2$ è $h$: l’altezza dell’albero coinvolto nella rotazione passa da $h+3$ a $h+2$ 
- solo nel caso (i) potremmo aver fatto un inserimento perché altrimenti nel caso (ii) sarebbe stato già un albero sbilanciato
![[Pasted image 20241127181613.png]]
**(ii)** l’altezza di $T2$ è $h+1$ : l’altezza dell’albero coinvolto nella rotazione rimane pari a $h+3$


##### CASO SD
in questo caso abbiamo un figlio a $sx$ di $v$ che ha un sotto albero a $dx$ che provoca uno sbilanciamento
![[Pasted image 20241128104342.png|500]]
il problema viene causato da $T(w)$ che è alto $h+1$

![[Pasted image 20241128105611.png]]
possiamo fare una rotazione del sottoalbero $sx$ a $sx$  e poi dell'albero principale a $dx$ 
il caso SD può essere provocato da 
- inserimenti in $T_2$ e in $T_3$
- eliminazioni in $T_4$
#### Inserimento

- inserisco il nodo come in un BST
- per ribilanciare il tutto e fare la rotazione prendo il nodo critico(il nodo piu in basso sbilanciato)
Esempio `insert(10,e)`
![[ezgif.com-speed_4 1.gif|600]]
##### Costo di insert
insert ha costo $O(logn)$ poiché la rotazione costa $O(1)$ invece l'inserimento è come nel BST

#### Eliminazione
funziona come nel BST ma bisogna ribilanciare le cose facendo rotazioni singole o doppie
qui avrò uno sbilanciamento dovuto a una riduzione dell'altezza
Esempio `delete(8)`
![[slides_animation_slower-ezgif.com-crop.gif]]

##### Costo di delete
delete ha costo $O(logn)$ poiché la rotazione potrebbe costare $O(logn)$ perché potrei fare $logn$ rotazioni invece il delete è come nel BST



tutto $completamente$ logaritmico


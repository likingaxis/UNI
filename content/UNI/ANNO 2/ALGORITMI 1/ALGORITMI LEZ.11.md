[[cap6.pdf|pdf della lezione]]
## IL PROBLEMA DEL DIZIONARIO
![[Pasted image 20241125114548.png]]
**obiettivo**:mantenere questa collezione di oggetti con chiave e eseguire operazioni in modo coerente
- insert
- delete
- search
>[!question]- cosa sono i campi satellite?
>i Campi Satellite sono tutti quei campi aggiuntivi che non dipendono dalla chiave
>tipo nome cognome ecc...

#### PSEUDOCODICE
- se faccio la ricerca posso avere piu chiavi e l'algoritmo di ricerca trova un elemento qualsiasi che ha quella chiave
#### GARANZIE DI EFFICIENZA
- bisogna prima di tutto garantire che tutte le operazioni su un dizionario con $n$ elementi costino almeno $O(logn)$ abbiamo due idee per applicarlo e verificarlo:
	1. definire un albero binario t.c ogni operazione costi $O(altezza \ albero)$ (**ALBERI BINARI DI RICERCA**)
	2. fare in modo che l'altezza dell'albero sia $O(logn)$ (**ALBERI AVL**, I SUPER SAYAN)
### OGGI VEDREMO I BST
>[!info]- questi alberi prevedono delle proprietà
>- ogni nodo $v$ contiene un elemento $elem(v)$ cui è associata una chiave $chiave(v)$ con un dominio ordinato
>- ogni nodo a sx deve avere chiavi piu piccole della radice, ogni nodo a dx deve avere chiavi piu grandi
>![[Pasted image 20241125122132.png]]
>![[Pasted image 20241125120444.png|500]]

>[!quote]- piccolo catch per l'esame
>quando si chiede la definizione di sta roba, non si deve fare 
>
>![[Pasted image 20241125122149.png|300]]
>
>perché bisogna giustificarlo per ogni sottoalbero

###### Altro esempio di un BST
![[Pasted image 20241125122911.png]]
#### Ordinamenti del BST
possiamo quindi notare che per forza di cose la disposizione cosi delle chiavi ha una sorta di "ordinamento" delle chiavi, dico una sorta perché non sono per forza le foglie a essere le più piccoli
- mettiamo per esempio che nell'albero sopra io facessi esplodere $2$ in quel caso il minimo sarebbe il nodo $3$ che non è una foglia
##### VISITA IN ORDINE SIMMETRICO AL BST
>[!info]- definizione di visita simmetrica
>visito $figlio \ sx$ poi $padre$ poi $figlio \ dx$

se lo visitiamo in ordine simmetrico il BST ritornerà chiavi ordinate
potrà sembrare un caso ma non lo è->verifica per induzione
ordine di visita dell'albero sopra:
![[Pasted image 20241125123742.png|300]]

>[!bug] RICORSIVAMENTE OGNI RADICE AVRA A SX E DX I RISPETTIVI > E <
###### VERIFICA CORRETTEZZA VISITA SIMMETRICA DEL BST
![[Pasted image 20241125124703.png|600]]
![[Pasted image 20241125124717.png|600]]


#### LE IMPLEMENTAZIONI DEL DIZIONARIO SU UN BST

##### <font color="#d83931">LA RICERCA</font>
- parto dalla radice e faccio dei confronti mettendo $elemento$ che cerco $\geq$ o $\leq$ della $chiave$ in quel dato sottoalbero
`Search(7)`
![[Pasted image 20241125125235.png|500]]

###### PSEUDO
![[Pasted image 20241125125206.png]]
- $T$ albero
- $chiave(k)$ non cambia sarà la chiave che cerchiamo
- $v$ ogni volta assume il valore del figlio $sx$ o $dx$ 
###### COSTO
$O(altezza \ albero)$
- perché **<font color="#f79646">al più</font>** si ripete fino al nodo che vale null e termina il codice, quindi quando sono arrivato all'ultimo nodo dell'albero in termini di lunghezza

##### <font color="#d83931">INSERIMENTO</font>
- il nuovo elemento diventerà sempre figlio di una foglia
- simulo una ricerca del nodo che voglio aggiungere
- facciamo tutto il $while$ della ricerca, appena arrivo alla foglia giusta faccio una condizione per metterlo o a $sx$ o a $dx$ di essa
`Insert(e,8)`
![[Pasted image 20241125151335.png|500]]
###### COSTO
$O(altezza albero)$
- per gli stessi motivi
##### <font color="#d83931">LA CANCELLAZIONE</font>
- devo implementare tre procedure per applicare la cancellazione
##### <font color="#6425d0">MAX</font>
![[Pasted image 20241125152032.png|500]]
- tiriamo dritti ai vari figli destri di $v$ ovvero
![[Pasted image 20241125152920.png|500]]
##### <font color="#6425d0">MIN</font>
cosa analoga ma vado a sinistra
##### <font color="#6425d0">PREDECESSORE</font>
il predecessore è quel nodo $k$ che viene numericamente prima di un nodo $v$ definito all'interno di $TUTTO$ l'albero
###### PSEUDOCODICE
![[Pasted image 20241125155837.png|500]]
- per il predecessore dipende se stiamo parlando di un nodo che ha un figlio a $sx$ oppure no
	- se la ha allora prende il $max$ dei nodi a $sx$
	- altrimenti sale su con i padri finché non trova un padre $q$ che sia un figlio $dx$ di un padre $p$ e che quindi per definizione sappiamo che, se un figlio è a $dx$ del padre allora é maggiore, così facendo abbiamo trovato il predecessore di $u$, ovvero il padre del figlio a $dx$
	- ritorniamo il padre di quel determinato nodo perché si verifica la condizione 2 del while
Esempio grafico dei due casi
![[Pasted image 20241125160643.png|400]]
###### COSTO
$O(altezza \ albero)$

##### <font color="#6425d0">SUCCESSORE</font>
il successore è quel nodo $k$ che viene numericamente dopo di un nodo $v$ definito all'interno di 
$TUTTO$ l'albero
sarà simile al predecessore quello che cambia è che 
- in questo caso vado a cercare i padri che sono figli $dx$ finchè non trovo quello che è figlio $sx$ e suo padre sarà il succesore
- oppure cerco il minimo di quelli a $dx$ del nodo
![[Pasted image 20241125160903.png|500]]
###### COSTO
$O(altezza \ albero)$

Ora che abbiamo tutti questi blocchetti applichiamo la vera e propria operazione di eliminazione
Ci sono tre casi:
1. se $u$ è una foglia allora posso eliminarla e sticazzi **costo costante** $O(1)$
2. se $u$ non è una foglia ma ha solo un figlio faccio puntare $v$ al figlio di $u$  **costo costante** $O(1)$
![[Pasted image 20241125162224.png|350]]
3. se $u$ ha due figli 
	- cerco il predecessore o successore(che ha max un figlio) di $u$ e lo sostituisco con $v$,  facendo il secondo delete 
	- eliminando $u$ che è stato scambiato con $v$ ritorneremo alla normalità collegando il figlio di ${u_{nuovo}}$  con il padre di ${u_{nuovo}}$ (step 3)
	- **costo  $O(altezza \ albero)$
![[Pasted image 20241125162709.png|600]]


>[!info]- ESEMPIO
>![[Pasted image 20241125163306.png]]

###### COSTO
dipende dal tipo di cancellazione
di solito $O(altezza \ albero)$
a volte $O(n)$ se l'albero è estremamente sbilanciato
##### CASO BILANCIATO $O(logn)$
![[Pasted image 20241125164247.png]]

##### CASO LINEARIZZATO $O(n)$
![[Pasted image 20241125164322.png]]
è più profondo che largo quindi sarà $O(n)$
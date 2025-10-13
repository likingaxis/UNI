[[usi_dfs_2024.pdf|pdf della lezione]]
Il BFS serve per calcolare i cammini minimi da una sorgente
###### Il DFS no quindi a che serve?
Oggi risponderemo a questa domanda

Rivediamo l'algoritmo DFS [[ALGORITMI LEZ.15]]
- algoritmo ricorsivo
- restituisce l'albero DFS, inizialmente vuoto
- albero che verra riempito con tutti gli archi visitati

#### Algoritmo DFS con aggiunta di clock
![[Pasted image 20241215114303.png|700]]
questa aggiunta ci consente di tenere conto
- il tempo di visita iniziale
- il tempo che intercorre tra la visita iniziale e finale
	- dove in mezzo ci saranno state ipotetiche visite
- possiamo vedere come nell'algoritmo visitaDFS inizializziamo clock a 1 globalmente

- che succede se alcuni vertici non sono raggiungibili da S?
	- non li conta
	- ci sono delle situazioni in cui invece conta visitarli quindi ora vedremo un codice modificato che visita tutti i vertici
##### Codice
![[Pasted image 20241215115449.png|500]]
- lui si scorre prima tutti i nodi anche quelli non collegati 
- poi fa la chiamata ricorsiva per ogni nodo $v$ che non è stato già marcato dalle precedenti chiamate
>[!info]- esempio grafico un pò storto
>![[Pasted image 20241215120643.png]]
##### ESEMPIO GRAFICO
![[Pasted image 20241215120808.png]]
##### I contatori pre e post hanno delle proprietà particolari:
prendiamo due nodi $u$ e $v$ e giochiamoci un po'
- se prendiamo gli intervalli $[pre(u),post(u)]$ e  $[pre(v),post(v)]$
	- succede che se i valori si incrociano uno è contenuto nell'altro(non sono disgiunti)
- $u$ è antenato di v se $pre(u)<pre(v)<post(v)<post(u)$
	- il $pre(v)$ e il $post(v)$ sono compresi tra u
- sfruttando queste cose possiamo capire di un arco$(u,v$) il suo tipo
	- <font color="#00b050">in avanti</font>. quando un nodo v è compreso in uno v
	- <font color="#00b0f0">indietro</font>, quando un grafo 
	- <font color="#d99694">trasversali</font>, quando non si incrociano
![[Pasted image 20241215125015.png|400]]
![[Pasted image 20241215124008.png|400]]
##### RICONOSCERE UN CICLO IN UN GRAFO G
- facciamo una visita DFS e capiamo se c'è un arco all'indietro
>[!info] PROPRIETÀ
>un grafo diretto G si dice che ha un ciclo se e solo se la visita DFS rivela un arco all'indietro

>[!tip] DIMOSTRAZIONE
><= se c'è un arco all'indietro allora c'è ciclo
>=> supponiamo che esista un ciclo $<v_0,v_1,...v_k=v_0>$  in G
>visto che $v_k$ è uguale a $v_0$ significa proprio che abbiamo un ciclo
>- supponiamo che $v_i$ sia il primo nodo che visitiamo, visto che $v_{i-1}$ è raggiungibile da $v_i$ allora prima del termine delle visite di $v_i$ 
>- $v_{i-1}$ andrà da $v_i$ facendo verificare un arco all'indietro $(v_{i-1},v_i)$
>![[Pasted image 20241215132138.png]]

### ORDINAMENTO TOPOLOGICO UN'ALTRO UTILIZZO DEI DFS 
###### Definizione di DAG
Un Grafo G diretto si dice <font color="#d99694">DAG</font> quando è un grafo diretto senza cicli
###### Definizione di <font color="#d99694">ORDINAMENTO TOPOLOGICO</font>
- è un ordinamento di vertici in un certo ordine o $sx$ o $dx$ in modo che tutti gli archi vanno solo o a $sx$ o a $dx$ 
<font color="#4f81bd">formalmente:</font>
È una funzione biettiva che mappa i vertici fra $1...n$ tale che per ogni arco$(u,v)$ il 
- **$\sigma(u)<\sigma(v)$**

La funzione σ  serve per assegnare un numero a ogni nodo in modo che rispetti la direzione degli archi nel grafo. Se un nodo punta a un altro, deve venire prima nell’ordine.

in poche parole mette gli archi in ordine dei vertici con le posizioni in ordine
- il nodo deve essere in una posizione precedente di quelli con cui ha un arco
![[Pasted image 20241215133341.png]]
>[!warning] Ricorda molto la roba delle dipendenze

>[!success] infatti l'ordine topologico ci consente di vedere le dipendenze sfruttabili
>(creare un software che ordini le cose da progettare con le varie dipendenze)

se non ti ricordi:
[[ALGORITMI LEZ.14#Reti delle dipendenze|lezione sulle reti delle dipendenze]]
###### Quali grafi non ammettono ordinamento topologico?
- un ciclo sicuramente no perché ci sono dipendenze infinite
- UN DAG ammette sempre un ordinamento topologico? si
Dimostriamolo per assurdo -> 

Dimostriamo che per ogni DAG abbiamo un ordinamento topologico
=> 
per assurdo poniamo $\sigma$ come ordinamento topologico di $G$ 
e sia  $<v_0,v_1,...v_k=v_0>$ un ciclo
allora $\sigma(v_0)$<$\sigma(v_1)$<...<$\sigma(v_{k-1})$<$\sigma(v_k)$=$\sigma(v_0)$ 
così stiamo dimostrando che per ognuno di questi abbiamo un ordinamento topologico ovviamente senza contare quel nodo che forma il ciclo che poi verrà uguale

>[!bug] ordinamento topologico di un G non è per forza 1
##### Come aggiunta alla dimostrazione ora vedremo degli algoritmi che ordinano in modo topologico
ALGORITMO 1
- fai una visita DFS e ordina in modo decrescente rispetto ai tempi di fine visita post
CODICE
![[Pasted image 20241215151129.png|600]]
- ogni volta che finisce il primo vertice sarà quello più piccolo, quindi gli altri li aggiungiamo alla lista nello stesso tempo in cui finiscono
###### COSTA UGUALE ALLA VISITA IN PROFONDITA $\Theta(n+m)$
ESEMPIO GRAFICO
![[Pasted image 20241215151855.png|500]]
È CORRETTO?
- Si ma non dobbiamo prendere i passi all'indietro ovviamente

###### Un algoritmo alternativo
![[Pasted image 20241215152909.png|600]]

- troviamo un vertice senza archi entranti-> rimuoviamo tutti i suoi vertici incidenti 
- troviamo il prossimo vertice senza archi entranti
- finchè non abbiamo più vertici senza archi entranti
- ha il vantaggio di far capire meglio la sua correttezza
- da implementare è piu difficile in tempo lineare
#### Tempo $O(n+m)$
![[ezgif.com-animated-gif-maker 2.gif|500]]


##### COMPONENTI FORTEMENTE CONNESSE
Un grafo è fortemente connesso se per ogni nodo v abbiamo una coppia $(u,v$) ordinata possiamo avere che $u$ raggiunge $v$ e che $v$ raggiunge $u$
- Le componenti fortemente connesse sono quelle tratteggiate
Una componente fortemente connessa è una proprietà associabile a un grafo G con un insieme C di vertici che è massimale.
Il numero massimo di vertici che formo con quei determinati nodi forma un insieme da mettere in C(i tratteggi)
>[!info]- def del prof
>![[Pasted image 20241215162958.png|400]]

- **CFC sorgente**: una componente che **non ha archi entranti da altre CFC**.
- **CFC pozzo**: una componente che **non ha archi uscenti verso altre CFC**.

<font color="#c0504d">massimale:</font> se tu all'istanza C aggiungi un nodo non risulta più vera la proprietà  della componente fortemente connessa

![[Pasted image 20241215162536.png|400]]

**N.B E può raggiungere F ma F non E**

Il grafo delle CFC **rappresenta un DAG**
![[Pasted image 20241215163513.png]]

Questo problema per trovare tutte le CFC si può risolvere in O(n)
#### Diverse proprietà
##### Proprietà 1:
Se facessi partire la visita in uno dei vertici CFC raggiungerei solo i vertici di quella determinata componente pozzo
Il codice termina quanto hai visitato tutti i nodi raggiungibili da $u$

##### Proprietà 2:
Se $C$ e $C'$ hanno un vertice che collega $C$ in $C'$ allora inevitabilmente $C$ avrà una variabile 
$post \ > \ di \ C'$ 
- deve prima scorrersi tutto $C'$ e poi $C$ finirà
- se partiamo da $C'$ non ci arriva mai in C

![[Pasted image 20241215164611.png|300]]
##### Proprietà 3:
Ci basta vedere chi ha il post più grande della singola visita DFS su un insieme CFC per trovare una  componente di tipo sorgente

>[!success] Noi ora abbiamo capito come trovare una sorgente abbiamo bisogno di una componente pozzo?
#### Invertiamo gli archi
invertiamo le direzioni per ottimizzare le cose del componente puzzo
Rimane tutto invariato in termini di proprietà 
- abbiamo il Grafo G-> 
	- ->creiamo il suo inverso $G^r$
![[Pasted image 20241215170213.png|700]]
- Calcoliamo i valori di post visita e prendiamo il piu grande e ora troviamo la componente pozzo
##### ALGORITMO che mette insieme tute le idee
CODICE lo fa vedere dopo la spiegazione grafica alle slide dopo
![[Pasted image 20241215170813.png|600]]
- inverto il grafo(nelle foto sopra  è già invertito)costa lineare
Fa una visita DFS completa del grafo $G^r$
Andiamo a fare una visita partendo da H, andiamo a prendere quindi tutti i componenti del suo CFC
- poi vediamo il valore piu piccolo del suo post 24 subito dopo e che non sia marcato e quindi di un'altra CFC

quindi tutto lineare


###### CODICE
![[Pasted image 20241215170347.png|400]]
Il resto $\Theta(n+m)$

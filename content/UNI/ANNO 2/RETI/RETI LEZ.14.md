### piano di dati e di controllo di una rete
principalmente una rete fa 2 cose:
- inoltro(forwarding)
	- sposta i pacchetti dall'ingresso del router alla sua appropriata uscita
		- fa parte del PIANO DEI DATI
- instradamento(routing)
	- determina il percorso migliore che i pacchetti devono eseguire dalla sorgente alla destinazione
		- fa parte del PIANO DI CONTROLLO
##### PIANO DI CONTROLLO su un router tradizionale
Ogni router:
- Calcola autonomamente la propria **tabella di instradamento**.
- Comunica con gli altri router (scambio di informazioni di routing).
- Quando riceve un pacchetto, consulta la tabella e decide dove inoltrarlo.

💡 In questo modello, ogni router partecipa attivamente all'elaborazione delle decisioni di instradamento.
![[Pasted image 20250429102216.png]]
##### PIANO DI CONTROLLO di tipo SDN
Con **SDN (Software Defined Networking)**:
- Il **controllo è centralizzato**: un **controller remoto** (software) calcola le tabelle di instradamento.
- I router non prendono decisioni: ricevono le tabelle già pronte e si limitano all’inoltro.
💡 Questo approccio separa completamente il **piano di controllo** (gestito dal controller centrale) dal **piano dei dati** (nei router/switch).
![[Pasted image 20250429102400.png]]
## Algoritmi di instradamento
servono per trovare il percorso migliore da far fare al pacchetto
- Percorso: sequenza di router che i pacchetti attraversano dall'origine alla destinazione 
- Migliore: con meno costo
![[Pasted image 20250429105050.png|300]]
#### Uso dei grafi per rappresentare il tutto
Per rappresentare una rete si usano i grafi dove:
- i nodi
	- sono i router
- gli archi
	- sono il collegamento con un peso
	- possono avere una direzione
![[Pasted image 20250429105432.png]]
###### Collegamento diretto
per collegamento diretto si intende un collegamento che non ha nodi intermezzi
![[Pasted image 20250429105525.png]]
## Classificazione degli algoritmi di instradamento
Si basa su due criteri fondamentali
- **1. Tipo di informazione usata**
	- **Globali (link state):**
	    - Ogni router conosce l’intera mappa della rete.
	    - Il calcolo del percorso ottimale è centralizzato.
	- **Decentralizzati (distance vector):**
	    - Ogni router conosce inizialmente **solo i costi verso i suoi vicini**.
	    - Con successive iterazioni, apprende gradualmente i costi verso tutti gli altri router.
-  **2. Frequenza di aggiornamento dei percorsi**
	- **Statici:**
	    - Cambiano raramente.
	    - Richiedono intervento umano.
	- **Dinamici:**
	    - Si aggiornano automaticamente al variare dei costi dei link.
- 3. Adattamento in base ai costi
	- alcuni algoritmi adattano il percorso in base a eventuali congestioni o altro
## 2 tipi di algoritmi
in questa lezione vedremo due tipi di algoritmi
- Dijkstra
- Distance Vector

### Algoritmo link-state: Dijkstra
è un algoritmo GLOBALE che consente di trovare il percorso migliore(con costo minimo) a partire da un nodo u verso tutti gli altri nodi

- È globale perché ogni router condivide le informazioni dei suoi collegamenti vicini a tutti gli altri router
	- lo fa in broadcast
- quindi tutti i router conoscono la rete completa e possono calcolare il percorso migliore
🔁 Funzionamento iterativo
- L’algoritmo mantiene un insieme `N'` di nodi per cui ha già trovato il cammino minimo.
- Ad ogni passo aggiunge un nuovo nodo a `N'`, quello raggiungibile con il **minimo costo attuale**.
- Dopo `k` passi, avrà trovato i cammini migliori verso `k` nodi.
Notazioni utilizzate:
![[Pasted image 20250429111622.png]]
#### Pseudocodice dell'algoritmo
![[Pasted image 20250429111830.png]]
- inizializzazione
	- parte da `u`
	- mette il costo di quelli vicini ad `u`
	- tutti gli altri a $\infty$ 
- ciclo
	- prende tutti i nodi che non sono in `N'`
	- tipo si prende un nodo `w` con distanza minima da `u` a `w`
		- inizialmente questo nodo `w` è tra quelli conosciuti quindi adiacente a `u`
	- aggiungiamo `w` a `N'` che inizialmente aveva solo `u`
	- prende i nodi adiacenti a `w` e trova la loro distanza minima
		- ripeto il ciclo finché `N'` è pieno
### Esempio
###### passo 0
- aggiorno le distanze da u per ogni nodo adiacente
![[Pasted image 20250429112912.png]]
###### passo 1.1
- prendo la distanza minima da u
	- quindi x
![[Pasted image 20250429113017.png]]
###### passo 1.2
- vedo se a partire da x ho un costo inferiore
	- tipo da v mi conviene rimanere con u
	- con w no
	- con y no
![[Pasted image 20250429113119.png]]
###### passo 2.1
- ora prende la distanza minima da x e rifà i calcoli
	- tocca a y
![[Pasted image 20250429113313.png]]
###### passo 2.2
- calcolo nuovi possibili distanze migliori
![[Pasted image 20250429113400.png]]
###### passo 3.1
- prendo le distanze adiacenti a v e vedo se sono migliori
![[Pasted image 20250429113652.png]]
###### passo 3.2
- notiamo che sono tutte uguali o peggiori
![[Pasted image 20250429113741.png]]
###### passo 4.1
- prendo il nodo minore adiacente a v
- in questo caso w
![[Pasted image 20250429113842.png]]

###### passo 4.2
- mi accorgo che sono tutti uguali o peggiori
![[Pasted image 20250429113938.png]]
###### passo 5.1
- cerco nodo minimo adiacente
- in questo caso z
![[Pasted image 20250429114133.png]]
###### passo 5.2
- mi accorgo che non posso migliorare nulla da z
- il risultato finale sarà:
![[Pasted image 20250429114209.png]]
![[Pasted image 20250429114300.png]]

### Altro esempio
![[Pasted image 20250429114240.png]]

#### Costi di questo algoritmo
- ogni volta vado a visitare n-1 nodi quindi costo $O(n^2)$
	- la prima volta n
	- poi n-1
	- poi n-2
	- e così via
- se usassi un heap come struttura dati avrei $O(nlogn)$
- per il costo dei messaggi
	- ad ogni iterazione faccio un broadcast che costa $O(n)$
		- perché deve arrivare a tutti gli $n$ nodi(router)
	- visto che abbiamo $n$ router costa $O(n^2)$
### Algoritmo distance vector (decentralizzato)
si basa su un'equazione ideata da Bellman-Ford
![[Pasted image 20250429115720.png]]
Dove: 
- $dₓ(y)$ → costo del percorso minimo da x a y 
- $Cₓ,ᵥ$ → costo collegamento diretto da x a v 
- $dᵥ(y)$ → costo cammino minimo da v a y
#### Esempio
Nodo `x` vuole raggiungere `y`. 
![[Pasted image 20250429115814.png]]
Ha tre vicini diretti:
1. **Via `v₁`**:
    - `c(x,v₁) = 4`
    - `d(v₁,y) = 8`
    - Totale: `4 + 8 = 12`
2. **Via `v₂`**:
    - `c(x,v₂) = 3`
    - `d(v₂,y) = 10`
    - Totale: `3 + 10 = 13`
3. **Via `vₙ`**:
    - `c(x,vₙ) = 9`
    - `d(vₙ,y) = 7`
    - Totale: `9 + 7 = 16`
🔍 Quindi `x` sceglie il percorso con **costo minimo**, cioè `12` passando per `v₁`.

📋 **Come funziona il Distance Vector nella rete**
- Ogni router mantiene una **tabella delle distanze** (distance vector) verso tutte le destinazioni.
- Inizialmente conosce **solo i costi verso i vicini diretti**.
- I router si **scambiano le tabelle con i loro vicini**.
- Quando un router riceve la tabella di un vicino, **aggiorna la propria** con la formula di Bellman-Ford.
- Se ci sono cambiamenti nei costi, **inviano di nuovo la tabella**.
- Il processo si ferma quando nessuna tabella cambia più → la rete ha **convergenza**.
### Esempio specifico ma astratto
#### T=0 inizializzazione
![[Pasted image 20250429120235.png]]
- La tabella in alto a sx mostra il distance vector di a cioè quanto a stima che costi raggiungere ogni altro nodo. 
- Ovviamente come per prima per raggiungere sé stesso è 0, per raggiungere i suoi vicini è 8 e 1. Gi altri li mette a inf perché non sa chi sono
Cosa succede: 
- A invia la sua tabella a b e d 
- D la invia a a, e, g 
- Ecc…

#### T=1 Ascolto e aggiornamento e invio dei nuovi vettori
![[Pasted image 20250429121959.png]]
i nodi ricevono le tabelle dai loro vicini
![[Pasted image 20250429122043.png|500]]

step successivo -> aggiornamento delle varie tabelle dopo il ricalcolo con la formula detta prima
![[Pasted image 20250429122201.png]]
ora avviene un reinvio con i calcoli aggiornati
![[Pasted image 20250429122416.png]]
questa cosa andrà in loop con T=1-> 2 -> 3 ecc... finché non ci saranno più aggiornamenti da fare
### Esempio decente fatto da chat gpt
🧪 **Esempio di aggiornamento del Distance Vector – Nodo `d`**
#### 🔹 Situazione iniziale:
Il nodo `d` ha come vicini diretti:
- `a`, `e`, `g`, tutti con **costo diretto = 1**.
Riceve i rispettivi distance vector:
- Da `a`: sa che `a → b = 8`
- Da `e`: sa che `e → b = 1`
- Da `g`: **non ha informazioni su `b`** → considera ∞
#### ✏️ **Applicazione della formula Bellman-Ford:**
![[Pasted image 20250429122852.png]]
#### 🔍 **Valutiamo le opzioni:**
1. **Via `a`:**
    - `c(d,a) = 1`, `dₐ(b) = 8` → totale = 9
2. **Via `e`:**
    - `c(d,e) = 1`, `dₑ(b) = 1` → totale = 2 ✅
3. **Via `g`:**
    - `d_g(b)` non è noto → costo = ∞

🔧 Il **percorso migliore è tramite `e`**, con **costo totale = 2**.
✅ Risultato:

$D_d(b) = 2$
Il nodo `d` ora conosce una nuova stima più efficiente per raggiungere `b`, passando da `e`.

#### Prendiamo l'esempio di prima delle slide e vediamo nello specifico cosa succede
cosa avviene esattamente al livello di calcoli?
- qui sotto b riceve i distance vector dai suoi vicini
	- per poi fare un ricalcolo adeguato alla sua tabella
![[Pasted image 20250429123521.png]]
- effettua i calcoli
- possiamo vedere come dopo i ricalcoli la tabella cambi(quella sotto)
![[Pasted image 20250429123558.png]]
visto che siamo ancora in t=1
- se c riceve il DV da b non otterrà la tabella aggiornata
![[Pasted image 20250429123622.png]]
- c effettua i calcoli e cambia la tabella
![[Pasted image 20250429124011.png]]
- poi tocca ad e che si chiederà...
![[Pasted image 20250429124054.png]]
e così va avanti...

### Comunicazione iterativa sullo stato
![[Pasted image 20250429124307.png]]
possiamo vedere che ad ogni t 
- le informazioni di un singolo router vengono diffuse a più router
#### Aggiornamento costi dei collegamenti
ogni nodo ha una tabella con i vari costi degli altri nodi
- se un nodo cambia il suo costo
- il nodo deve aggiornare la sua tabella delle distanze e rinviarla a tutti gli altri
### le buone notizie viaggiano in fretta
![[Pasted image 20250429124538.png]]
ora vediamo cosa succede se il collegamento da x-y passa da 4 a 1:
- a tempo 0
	- y si accorge che il collegamento x-y è cambiato
		- aggiorna il suo DV e lo manda a tutti i vicini
		- sia x che z
- a tempo 1
	- z si accorge che può passare per y per pagare meno
	- aggiorna il suo DV e lo invia ai vicini
- a tempo 2 
	- y riceve il nuovo DV ma si accorge che per lui non fa differenza
	- non aggiorna nulla
	- non invia nulla
si dice che:
- Il Distance Vector **reagisce solo quando qualcosa cambia**.
- Le buone notizie (cioè percorsi migliori) **si propagano in fretta** perché ogni aggiornamento genera altri aggiornamenti **solo se migliorativi**.
### le cattive notizie viaggiano piano
![[Pasted image 20250429125120.png]]
qui il percorso x-y peggiora da 4-> 60
- a tempo 0
	- y deve cercare una soluzione migliore per arrivare a x
	- pensa di passare per z pagando 1+4
		- perché z arriva a x passando per y(non aggiornato a 60)
	- aggiorna il DV e lo invia ai vicini
- a tempo 1
	- z riceve il DV di y 
	- y dice di passare a x con costo 5
	- z allora calcola che gli ci vuole 6 per raggiungere x
- a tempo 2
	- y riceve il DV di z
	- pensa che z impiega 6 per passare a x
	- quindi pensa di metterci 6+1=7
in poche parole si crea un loop infinito chiamato
"problema del conteggio infinito"

##### Altro problema
![[Pasted image 20250429132054.png]]
in questo caso viene rotto il collegamento x-y
sia y che z non capiscono cosa stia succedendo perché ognuno pende dall'altro nell'aggiornamento del DV
`y` prova a raggiungere `x` passando per `z`, che a sua volta si basa su `y`.
#### Soluzione parziale al problema(inversione avvelenata)
- Se `z` **instrada verso `x` tramite `y`**, allora **non deve mai dire a `y` che ha una via verso `x`**.
- Invece, dice a `y`:
	- $D_z(x)=+∞$
- Così `y` **non viene ingannato** nel momento in cui perde il collegamento diretto con `x`.
👉 Questo **blocca il ciclo prima che inizi**.  
Ma funziona **solo se il ciclo è tra due nodi adiacenti.**
![[Pasted image 20250429132354.png]]
![[Pasted image 20250429132427.png]]
### Quando invece non funziona(fail)
- Con topologie più complesse (più di due nodi nel ciclo), **l’inversione avvelenata non riesce a bloccare tutto**.
- L’esempio mostra un ciclo tra `x`, `y`, `z`, `w`.
	- Anche con poisoned reverse, si forma un **loop a tre nodi**, e i costi continuano a salire
![[Pasted image 20250429132542.png]]
🛑 Per reti più grandi si usano **altri meccanismi**: limite di costo massimo, split horizon, ecc.

### confronto
![[Pasted image 20250429133605.png]]

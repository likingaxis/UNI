## Misura di complessità
Una misura di complessità è una funzione `c` che associa un valore numerico ad una macchina di Turing T e ad un suo input.

>[!tip] `c(T,x)` rappresenta il "costo" della computazione `T(x)`

#### Due proprietà fondamentali da dover rispettare (Assiomi di Blum)
1) `c` è **definita per TUTTE E SOLE le computazioni che terminano**
	- anche perché, se una computazione non termina non ha senso considerare un costo "finito"
2) `c` deve essere **calcolabile**
	- deve esistere una macchina di Turing M che, ricevendo come input una macchina di Turing `T` e un suo input `x`, calcola `c(T,x)` ogniqualvolta `c(T,x)` è definita (ossia quando `T(x)` termina


---

## Misure deterministiche 
Queste sono misure di complessità che si riferiscono a computazioni deterministiche.

Quindi
- per ogni macchina di Turing deterministica T (riconoscitore o trasduttore) definita su un alfabeto $\Sigma$
- e per ogni $x \in \Sigma^{*}$
definiamo le due funzioni associate alla computazione `T(x)`
![[Pasted image 20250423191242.png]]

>[!tip] OSSERVAZIONE 
>Le due funzioni sono PARZIALI: non sono definite quando `T(x)` non termina

#### Dimostriamo ora che `dtime` e `dspace` rispettano i due assiomi di Blum
1) ==`c` è **definita per TUTTE E SOLE le computazioni che terminano**==
	LO ABBIAMO GIÀ DIMOSTRATO IN "OSSERVAZIONE"
	- Per ogni macchina di Turing deterministica `T` e per ogni $x ∈ Σ^{*}$, `dtime(T,x)` e `dspace(T,x)` sono definite **se e solo se `T(x)` termina**. 

2) ==`c` deve essere **calcolabile**==
	Partiamo da `dtime`
per verificare se rispetta i due assiomi di Blum andiamo a vedere U'
una classica macchina Universale U ma con un nastro in più che conta 1 ogni volta che facciamo una quintupla
- ovviamente la simulazione avviene a scatola aperta
	- OGNI quintupla deve essere modificata per mettere 1 e poi andare a destra
	- dovremmo prendere tutte le quintuple di U e farlo
![[Pasted image 20250423191404.png]]
	
>[!example]- Dimostriamo che `dspace` è calcolabile
> ### 🔧 Idea
>
Costruiamo una modifica $U_{dspace}$ della macchina di Turing universale `U`.
>
>### 🔹 Modifiche rispetto a `U`
>
>- Aggiungiamo a `U` un nuovo **nastro `N₅`** che fungerà da **contatore del numero di celle diverse utilizzate** nella computazione di `T(x)`
>- `U_dspace(T, x)` si comporta come `U(T, x)`, **con la differenza che:**
>  - Tiene traccia dell’insieme delle celle di lavoro visitate almeno una volta
>  - Ogni volta che visita **una nuova cella non ancora raggiunta**, scrive un `1` sul nastro `N₅` e la registra
>  - Alla fine della computazione, il nastro `N₅` contiene in **unario** il numero di celle di memoria usate da `T(x)`
>
>### 🔚 Risultato
>
>- Se `T(x)` **termina**, allora `U_dspace(T,x)` termina e sul nastro `N₅` c’è il valore `dspace(T,x)`
>- Quindi **`dspace(T, x)` è una funzione calcolabile**
>- Se `T(x)` **non termina**, anche `dspace(T,x)` **non è definita** (è una funzione parziale)
>
>## ✅ Conclusione
>
La funzione `dspace` soddisfa i due assiomi di Blum e **è calcolabile**.


---

## Misure non deterministiche
ora lavoriamo su macchine non deterministiche
Queste sono misure di complessità che si riferiscono a computazioni NON deterministiche.

Quindi
- per ogni macchina di Turing deterministica T (riconoscitore pefforza!!) definita su un albero $\Sigma$
- e per ogni $x \in \Sigma^{*}$
	- tali che `NT(x)` ACCETTA
definiamo le due funzioni seguenti
![[Pasted image 20250423191841.png]]

>[!question] perché prendiamo il minimo?
>possono esserci diverse computazioni che accettano con tempi diversi
>- il genio è burlone pasticcione ma anche pigro quindi prende le minime

>[!tip] OSSERVAZIONE
>Queste due funzioni sono MOLTO PARZIALI
>questo perché sono accettanti, ovvero non decidono un linguaggio ma lo accettano
>- questo significa che ci sono ancora più spazi non definiti
>	- spazi dove termina ma non accetta


>[!question] perché diciamo solo che accettano e non che decidono pure?
>perché in realtà le macchine di Turing non deterministiche non decide un linguaggio nel senso classico, questo è dovuto a una asimmetria tra la accettazione e il rigetto, infatti diciamo per semplificare le cose che:
>- una macchina non deterministica
>	- accetta se in una qualche computazione accetta
>	- rigetta se per qualsiasi computazione termina(non va in loop) e non accetta
>questo però non significa che decide il linguaggio però almeno termina e da qualcosa in output
>- ricorda bene che se va in loop allora rientriamo nel caso loop, perché non sapremo mai l'esito finale di quel ramo
>
>📌 **In sintesi**: una NTM **accetta**, ma **non sempre decide**, perché **l'eventuale presenza di loop rende impossibile determinare l’esito complessivo** in certi casi.

#### Cambio delle definizioni `nspace` e `ntime`
oltre a ciò che è stato detto prima aggiungiamo anche i casi di rigetto:

![[Pasted image 20250423193508.png]]

>[!bug] possiamo notare che precedentemente le definizioni di entrambi non rispettavano gli assiomi di Blum visto che prendevamo in considerazione solo i casi di accettazione, non era definita per i casi di rigetto, ricordando ciò che diceva il primo assioma
>==`c` è definita per TUTTE E SOLE le computazioni che terminano==
>- possiamo quindi dire che in questo caso non era definita per i rigetti

![[Pasted image 20250423193945.png]]


#### Procediamo a dimostrare se queste due funzioni rispettano gli assiomi
scherzetto! non lo chiede all'esame pappapero pappapa!
il primo assioma già abbiamo visto perché ha senso
per definire se rispetta il secondo assioma, ovvero se è calcolabile si fa una sorta di macchina universale come `dtime` di prima
- ma tanto non lo chiede
nspace(NT,x)
uguale a ntime

#### Relazione tra queste 4 funzioni temporali e spaziali
ricapitolando abbiamo:
`dtime, dspace, ntime, nspace`
quali di questi possiamo mettere in relazione?

una macchina non deterministica può anche essere deterministica
- quindi $dtime(T,x)=ntime(T,x)$
poi con il teorema 6.1 mettiamo in relazione tutto il resto
>[!tip] Teorema 6.1
> 
> Sia T una macchina di Turing deterministica, definita su un alfabeto Σ (non contenente il simbolo $\square$  ) e un insieme degli stati Q, e sia x ∈ $Σ^∗$ tale che T(x) termina. Allora
> $$dspace(T,x)\leq dtime(T,x)\leq {dspace(T,x)} *|Q| *(|\Sigma| +1)^{dspace(T,x)}$$

ora risolviamo piano piano tutto il teorema
### Risoluzione teorema 6.1(in parti)
##### Parte 1
$$dspace(T,x) ≤ dtime(T,x)$$
- questo perché per fare una scrittura comunque devi usare almeno il tempo della macchina
	- la prof la scrittura la chiama anche sporcatura del nastro
		- perché è come se stai scrivendo qualcosa su una tela vuota, la sporchi
quindi: se T(x) utilizza dspace(T,x) celle di memoria, quelle celle deve almeno leggerl
- questa definizione non prende i casi anomali che distruggono questo $\leq$ 

##### Parte 2
$$dtime(T,x)\leq {dspace(T,x)} *|Q| *(|\Sigma| +1)^{dspace(T,x)}$$
per facilità di lettura andiamo a definire che $dspace(T,x)=H$
cosa indica quella cosa a destra del $\leq$ ?
$H *|Q| *(|\Sigma| +1)^H$ 

è il numero di stati globali possibili di T nel caso in cui non più di $dspace(T,x)$ celle del nastro vengano utilizzate dalla computazione T(x)
scomponiamo le lettere

possiamo dire sicuramente che H è il numero di elementi nel nastro
- quindi avremo come numero di parole nelle H celle come $\leq (|\Sigma|+1)^H$
	- tutti i caratteri + il blank
	- elevato alla H ovvero il numero di celle
	- se non capisci rivediti l'argomento di probabilità tipo sul calcolo combinatorio
- come numero di stati globali in H avremo $(|\Sigma |+1)^H$ 
- $H*|Q|$ 
		- |Q| perché possiamo essere in qualsiasi stato
		- combinato anche al fatto che può essere in una delle qualsiasi celle $H$ 
quindi alla fine avremo $H *|Q| *(|\Sigma| +1)^H$ 
poniamo $H *|Q| *(|\Sigma| +1)^H$ = k(T,x)
quindi ora sappiamo che k(T,x) è il numero di stati globali possibili in T
- ora, ricordiamo che una computazione (deterministica) è una successione di stati globali tali che si passa da uno stato globale al successivo eseguendo una quintupla
se in una sequenza di stati globali DISTINTI raggiungiamo K+1 significa che siamo in un loop!
$SG_0 \rightarrow SG_1 \ ... SG_K \rightarrow SG_{K+1}$ 
- K doveva essere l'ultimo stato
- ma visto che siamo in K+1 siamo in un loop e allora non termina 
![[Pasted image 20250423205449.png]]
Ma **noi sappiamo che T(x) termina** (è una computazione valida e finita),  
quindi **non può entrare in loop**,  
quindi **non può durare più di k(T,x)) passi**.
➡️ **Questo limita il tempo in funzione dello spazio.**
🧠 Quindi **dtime** conta solo le computazioni che **terminano**



##### ora facciamo il caso non deterministico del teorema 6.1
per le non deterministiche è uguale ma scambi d con n

#### Relazione tra queste 4 funzioni
dtime, dspace, ntime, nspace
quali di questi possiamo mettere in relazione?
dati T e x dtime(T,x)
una macchina non deterministica può anche essere deterministica
quindi dtime(T,x)=ntime(T,x)
possiamo dire che dspace(T,x)$\leq$ dtime(T,x)
- questo perchè per fare una scrittura comunque devi usare almeno il tempo della macchina

se definiamo che dspace(T,x)=H 
possiamo dire sicuramente che H è il numero di elementi nel nastro
- quindi avremo come numero di parole nelle H celle come $\leq (|\Sigma|+1)^H$
- come numero di stati globali in H avremo $\leq H * |Q| *(|\Sigma |+1)^H$ mettiamo che questo sia uguale  a K
se in una sequenza di stati globali DISTINTI raggiungiamo K+1 significa che siamo in un loop!
$SG_0 \rightarrow SG_1 \ ... SG_K \rightarrow SG_{K+1}$ visto che siamo in K+1 siamo in un loop e allora non termina 
quindi tutto questo per definire che
dspace(T,x)$\leq$ dtime(T,x)$\leq$ $H *|Q| *(|\Sigma| +1)^H$ 
però abbiamo detto che dspace(T,x)=H 
quindi...
dspace(T,x)$\leq$ dtime(T,x)$\leq$ $H *|Q| *(|\Sigma| +1)^{dspace(T,x)}$ 

per le non deterministiche è uguale ma scambi d con n
![[Pasted image 20250423205543.png]]
la dimostrazione non è da fare


## Definizione dei tempi
Sia f : ℕ → ℕ una funzione totale calcolabile.
Serve a esprimere **limiti di tempo o spazio** in funzione della **lunghezza dell’input** ∣x∣|x|∣x∣
Sia Σ un alfabeto finito e sia x ∈ $Σ^∗$
- indichiamo con |x| il numero di caratteri di x

$L \subseteq \Sigma^*$ è <font color="#f79646">deciso</font> in un tempo deterministico f(n) se:
esiste una macchina di Turing deterministica T che decide L e tale che
- per ogni x ∈ $Σ^∗$, $dtime(T,x) ≤ f(|x|)$
	- e abbiamo che invece $( dspace(T,x) = f(|x|) ).$

Per le non deterministiche è un po' più difficile perché c'è quella roba dei due stati di accetto e rigetto
Un linguaggio L ⊆ $Σ^∗$ è <font color="#c0504d">accettato</font> in tempo (spazio) non deterministico f(n) se:
esiste una macchina di Turing non deterministica NT che accetta L e tale che
- per ogni x ∈ L, $ntime(NT,x) ≤ f(|x|)$ 
	- dove per lo spazio è uguale $( nspace(NT,x) ≤ f(|x|) )$
qui è accettato se la macchina NT non termina sempre ma accetta quindi basta che sia un riconoscitore

invece è deciso:
Un linguaggio L ⊆ $Σ^∗$ è deciso in tempo (spazio) non deterministico f(n) se:
esiste una macchina di Turing non deterministica NT che accetta L e tale che
- per ogni x ∈ $\Sigma^*$, $ntime(NT,x) ≤ f(|x|)$ 
	- dove per lo spazio è uguale$( nspace(NT,x) ≤ f(|x|) )$
qui la macchina deve essere di tipo trasduttore quindi termina sempre e quindi decide


##### piccole precisazioni su quanto detto prima
📌 1. Deterministico ⇒ nessun problema
Nel caso **deterministico**, tutto è semplice:
- Se una macchina **accetta** sempre decidendo correttamente (termina su ogni input), allora **accettare = decidere**
- Non c’è distinzione tra “accettato” e “deciso” in un tempo/spazio f(n)

 ⚠️ 2. Non deterministico ⇒ distinzione tra accettare e decidere
- Si **distingue** tra:
    - Linguaggi **accettati**: basta che **esista un cammino accettante**
    - Linguaggi **decisi**: **tutte le computazioni terminano**, e rigettano correttamente $se \  x∉L$ 
- Questo porta a pensare che:
    > ci siano linguaggi accettabili in tempo/spazio non deterministico, **ma non decidibili** nello stesso tempo/spazio


 **La distinzione tra accettare e decidere non ha più rilevanza pratica quando si impone un limite di risorse**, ad esempio un numero massimo di passi f(∣x∣)  
In questo caso, **anche se una macchina non deterministica accetta un linguaggio**, tutte le sue computazioni **devono comunque terminare entro f(∣x∣)**  
Di conseguenza, **non ci sono loop infiniti**, e quindi la macchina **si comporta come un decisore**.
➤ In altre parole, **accettare in tempo/spazio limitato equivale a decidere in tempo/spazio limitato.**

Ossia, la teoria della complessità computazionale si occupa solo di linguaggi decidibili

##### Teorema 6.2
Quindi risolviamo il Teorema 6.2
>[!tip] Teorema 6.2 (intanto espresso nel tempo): 
> Sia f : ℕ → ℕ una funzione totale calcolabile. Se L ⊆ $Σ^∗$ è accettato da una macchina di Turing non deterministica NT tale che, 
> - per ogni x ∈ L, $ntime(NT,x) ≤ f (|x|)$
> 	 - allora L è decidibile.

### Risoluzione teorema 6.2(nel tempo)
##### 🧠 Intuizione:
Abbiamo una macchina non deterministica che **accetta** le stringhe in $L$ entro tempo $f(|x|)$,  
ma **non dice nulla** su cosa succede per $x \notin L$ (potrebbe anche non fermarsi mai!).

Il nostro obiettivo è **costruire una nuova macchina NT′ che decide L**: cioè che **termina sempre** e **accetta se e solo se** $x \in L$.
##### 🛠️ Strategia della dimostrazione
1. **Costruiamo una macchina $T_f$​** che calcola $f(n)$ in **unario** (cioè una stringa di 1 ripetuti)
    - Esempio: se $f(5)=4$, allora $T_f$​ scrive `1111`

2. **Costruiamo una nuova macchina NT′**, a **3 nastri**, che decide $L$:
    - Nastro 1: contiene l’input $x$
    - Nastro 2: usato per calcolare $|x|$
    - Nastro 3: conterrà $f(|x|)$ in unario (numero di passi massimi concessi)

🧩 PASSAGGI DELLA COSTRUZIONE
###### 🔧 FASE 1: Calcoliamo f(|x|)
1. $NT'$ prende in input `x`.
2. Scrive $|x|$ (la lunghezza di x) su un nastro.
3. Chiede a una macchina calcolatrice $T_f$​ di calcolare $f(|x|)$ e scriverlo in **unario** su un altro nastro (questo qui sarà il tempo massimo utilizzabile)
###### 🔧 FASE 2: Simuliamo $NT(x)$
1. $NT^{′}$ **simula** $NT$ su input `x`.
2. Ogni volta che fa una mossa della simulazione, **cancella un `1`** dal nastro dove c'è f(|x|).
3. Se:
    - $NT(x)$ accetta → anche $NT^{′}(x)$ accetta.
    - $NT(x)$ rigetta → anche $NT^{′}(x)$ rigetta.
    - Finisce il tempo (il nastro è vuoto, ma $NT$ non ha ancora terminato) → $NT^{′}$ **rigetta**.

> Quindi $NT^{′}$ simula il comportamento di $NT$, ma si ferma dopo f(|x|) passi.

quindi 
- ✅NT accetta nei tempi prestabiliti, e visto che NT' la simula accetta
- ❌NT non accetta in tempo, NT' rigetta perché è scaduto il tempo
	- oppure rigetta a prescindere NT quindi anche NT' rigetta

###### ❓ Ma... c'è un problema?
> Quanto tempo impiega `NT'` per calcolare `f(|x|)`?
- Non lo sappiamo!
- Sappiamo solo che **termina**, perché `f` è **totale calcolabile**
- Ma **non possiamo sapere quanto tempo impiega**

✅ Conclusione
- La macchina `NT'` **decide** il linguaggio `L` (cioè **termina sempre** e dà una risposta corretta)
- ❌ **Non possiamo dire** che lo decide **in tempo `f(n)`**, perché non sappiamo quanto tempo ci vuole per calcolare `f(n)`
###### 🔚 Quindi:
🔴 `L` è **decidibile**  
🟡 Ma **non necessariamente** in **tempo `f(n)`**

### Risoluzione teorema 6.2(nello spazio)
uguale a ntime, non serve studiarla
## Correlazione polinomiale
Qui si dimostra che che tutti i modelli di calcolo deterministici sono fra loro polinomialmente correlati 
- Macchine di Turing ad un nastro
- Macchine di Turing a quanti nastri ci pare
- Macchine di Turing su alfabeto binario
- Macchine di Turing su alfabeti grandi quanto ci pare

>[!question] cosa significa che sono polinomialmente correlati?
>che per ogni macchina di Turing T di uno di questi tipi esistono una macchina di Turing T’ di uno qualunque degli altri tipi ed un polinomio p tali che 
>- T’ risolve lo stesso problema risolto da T e, per ogni x,
>	- $dtime(T’,x) ≤ p( dtime(T,x) )$ e
>	- $dspace(T’,x) ≤ p( dspace(T,x) )$
>
>in poche parole puoi fare le stesse computazioni di una qualsiasi macchina di quelle sopra con un'altra di quelle là in un tempo $\leq$ 

E possiamo anche dire che il modello Macchina di Turing è polinomialmente correlato con il PascalMinimo

>[!question] a cosa serve sapere questo?
>Che possiamo risolvere un problema utilizzando il modello che più ci aggrada
>- con costi uguali o addirittura inferiori!
>- quindi possiamo creare un algoritmo in pascal minimo e sapere che poi funzioni anche in una Macchina di Turing ad un nastro
>	- basta che lo risolva in f(|x|) istruzioni almeno in una istanza

$|x|$ è la lunghezza dell'input quindi il numero di celle dell'input del rispettivo modello di calcolo
- ad esempio i bit di una RAM

## Questa lezione parte da un problema
Arriverà sempre qualcuno che dimostrerà che un linguaggio è decidibile in un tempo o spazio inferiore a quello che abbiamo deciso f(n), magari in f(n/3) o f(n/k)

per definire ciò andiamo ad applicare dei teoremi
### Teorema di accelerazione lineare
>[!tip] Teorema 6.7
>![[Pasted image 20250424171859.png]]
>Questo teorema ci dice che, dato un qualunque algoritmo, esiste sempre un algoritmo più veloce del primo di un fattore costante!


>[!question] a cosa servono quei due addendi 
>$O(|x|^2)$ e $O(|x|)$?
>- servono perché le macchine per essere più veloci devono codificare tutto il nastro di input
>   - se abbiamo un solo nastro impiegheremo tempi di cancellazione e riscrittura
>   - se abbiamo più di un nastro basta riscrivere sotto e basta
>
>di questo teorema non c'è da studiare la dimostrazione!
>

### Teorema di compressione lineare
>[!tip] Teorema 6.6
>medesimo Teorema del precedente ma con dspace
>![[Pasted image 20250424172852.png]]
>Questo teorema ci dice che, dato un qualunque algoritmo, esiste sempre un algoritmo che usa una frazione costante della memoria del primo!
>- in questo caso anche se con solo un nastro
>	- occupiamo $O(|x|)$
>	- questo perché non teniamo conto delle riscritture sullo stesso spazio di memoria

>[!quote] **Lo spazio usato da una macchina di Turing è la quantità massima di celle diverse scritte o lette durante l’esecuzione**, **non quanto spesso** **ci si muove tra esse.**

- avremo quindi un $T_1$ che comprime il nastro di input di T 
in poche parole $T_1$ avrà un linguaggio che sarà $\Sigma \cup (\Sigma \cup \{\square \})^K$
- unire Sigma all'insieme quello elevato a K serve per definire anche l'alfabeto originale che effettivamente è ancora incluso
praticamente se abbiamo K=2 lui compatterà l'input in 2 a 2 ovvero:
- se (x1),(x2) occupava due celle ora (x1,x2) sul nastro occupa 1 sola cella
- Se l’input originario occupava ∣x∣ celle, ora viene **codificato in circa** $\frac{|x|}{K}​$celle.
	- La computazione poi avviene su questo **nastro compresso**, quindi usa **meno spazio complessivo**.

## Classi di complessità (deterministiche)
Siamo pronti a raggruppare i linguaggi in base all'efficienza delle macchine che li decidono.

>[!question] Cosa vuol dire che una macchina che decide un linguaggio ha una certa efficienza?
>Significa che la macchina che decide un linguaggio $L \subseteq \Sigma^{*}$ si comporti "bene" su <u>ogni</u> parola $x \in \Sigma^{*}$

Però ovviamente non possiamo trovare la macchina "migliore", perché tanto sappiamo che se ne prendo una ne esisteranno altre più potenti (teoremi di prima).

Per risolvere questa questione utilizziamo la notazione $O$ e diciamo che 
	==Un linguaggio `L` appartiene all'insieme caratterizzato dalla "efficienza temporale" individuata dalla funzione totale e calcolabile `f`, se esiste una macchina `T` che decide (o accetta) `L` e che, per ogni `x` sull'alfabeto di `L`, termina in `O(f(|x|))` istruzioni.==

E discorso analogo per "efficienza spaziale".

#### Effettive classi di complessità deterministiche
##### Efficienza temporale - DTIME
Le classi che misurano "efficienza temporale" nel caso deterministico si chiamano <font color="#ff0000">DTIME</font>: data una <font color="#245bdb">funzione totale e calcolabile f</font> 
![[Pasted image 20250424192546.png]]
ATTENZIONE:
- <font color="#245bdb">dtime</font> (minuscolo) è la **misura di complessità**, ossia, una <u>funzione</u>
- <font color="#ff0000">DTIME</font> (MAIUSCOLO) è una **classe di complessità**, ossia, una sorta di <u>insieme</u>

##### Efficienza spaziale - DSPACE
Le classi che misurano "efficienza spaziale" nel caso deterministico si chiamano <font color="#ff0000">DSPACE</font>: data una <font color="#245bdb">funzione totale e calcolabile f</font> 
![[Pasted image 20250424192558.png]]


---

## Classi di complessità (non deterministiche)
Facciamo le stesse considerazioni delle deterministiche.
##### Efficienza temporale - NTIME
Le classi che misurano "efficienza temporale" nel caso non deterministico si chiamano <font color="#ff0000">NTIME</font>: data una <font color="#245bdb">funzione totale e calcolabile f</font>
![[Pasted image 20250424192614.png]]
Qui si parla di ACCETTAZIONE perché sappiamo che se un linguaggio è accettato entro un certo numero di istruzioni, sappiamo che è decidibile; <u>MA NON SAPPIAMO QUANTO CI METTE A RIGETTARE</u>.
E, per di più, a noi interessa solo accettare le parole del linguaggio.

##### Efficienza spaziale - NSPACE
Le classi che misurano "efficienza spaziale" nel caso non deterministico si chiamano <font color="#ff0000">NSPACE</font>: data una <font color="#245bdb">funzione totale e calcolabile f</font>
![[Pasted image 20250424192635.png]]


---

## Classi di complemento
![[Pasted image 20250424192650.png]]


---

### Un paio di questioni
1) Qui stiamo considerando linguaggi sull'alfabeto $\{0,1\}$ per comodità ma possiamo considerare anche altri alfabeti (e lo faremo)
2) Alla funzione f che definisce una classe di complessità (ad esempio `DTIME[`<font color="#245bdb">fn</font>`]`) diamo il nome di <font color="#245bdb">funzione limite</font>
	- che ovviamente deve essere totale e calcolabile sennò, per definizione, avremo una funzione che ci dice quante istruzioni esegue una computazione MA di cui non sappiamo il reale valore (inutile se ci pensi!)


---

## Relazioni fra classi di complessità
>[!lemma] Teorema 6.8
>![[Pasted image 20250424192707.png]]

La dimostrazione è facile.
Una macchina deterministica è **una particolare macchina non deterministica con il grado di non determinismo pari a `1`** e, inoltre
- una parola decisa in un certo numero di passi è anche accettata in quel certo numero di passi
- una parola decisa utilizzando un certo numero di celle è anche accettata in quel certo numero di celle

>[!lemma] Teorema 6.9
>![[Pasted image 20250424192721.png]]

Questa dimostrazione segue direttamente dal [[FONDAMENTI LEZ.21#Risoluzione teorema 6.1(in parti)|teorema 6.1]]
Sia $L \subseteq \{0,1\}^{*}$ tale che $L \in DTIME[f(n)]$.
Sappiamo, per il Teorema 6.1, che $$\text{spazio} \le \text{tempo}$$ per ogni macchina di Turing:
	se una macchina fa al massimo `t` passi, non può usare più di `t` caselle

Perciò $$\text{dspace(T,x)} \le \text{dtime(T,x)}$$e dato che $$\text{dtime} \in O(f(|x|))$$ (per [[FONDAMENTI LEZ.22#Efficienza temporale - DTIME|definizione DTIME]]) 
Allora possiamo scrivere $$\text{dspace(T,x)} \le \text{dtime(T,x)}  \in O(f(|x|))$$e quindi anche $$\text{dspace(T,x)} \in O(f(|x|))$$
## ✅ **Conclusione**

> Se $L \in \text{DTIME}[f(n)]$, allora $L \in \text{DSPACE}[f(n)]$

Cioè: $$\text{DTIME}[f(n)] \subseteq \text{DSPACE}[f(n)]$$
✅ **Vale anche nel caso non deterministico**: $$\text{NTIME}[f(n)] \subseteq \text{NSPACE}[f(n)]$$

>[!lemma] Teorema 6.10
>![[Pasted image 20250425114633.png]]

##### 📘 Teorema 6.10 (detto in parole semplici)

> Se usi **al massimo `f(n)` celle di memoria** per decidere un problema, allora esiste un modo per risolverlo che richiede **tempo al massimo `2^O(f(n))`** (cioè tempo esponenziale rispetto allo spazio).

###### Formalmente:
```
DSPACE[f(n)] ⊆ DTIME[2^O(f(n))]
NSPACE[f(n)] ⊆ NTIME[2^O(f(n))]
```

##### 🧠 Ok, ma perché?
Immagina che la macchina di Turing T usi al massimo `f(n)` celle del nastro per un input lungo `n`.

> 🔍 Ogni "configurazione" della macchina è:  
> stato + contenuto del nastro + posizione della testina

Quante possibili **configurazioni diverse** può assumere T?

##### Le combinazioni sono tante, ma **finite**! E in particolare:
- Gli **stati** sono un numero fisso, diciamo `|Q|`
- Le celle usate sono al massimo `f(n)`
- Ogni cella può contenere uno dei simboli dell’alfabeto `|Σ|` (più il blank)
- La testina può stare in una delle `f(n)` celle

Allora il numero totale di configurazioni è al massimo:

```
|Q| × |Σ + 1|^f(n) × f(n)
```

📌 **Questo è un numero esponenziale rispetto a `f(n)`**  
⇒ diciamo che è **al massimo `2^O(f(n))` configurazioni**

##### 🔁 E come ci serve questo?
Se conosci **tutte le configurazioni possibili**, puoi:
- simulare la macchina T "dall’esterno"
- esplorare tutte le possibili sequenze di configurazioni (tipo albero di esecuzione)
- controllare se si arriva a uno stato di accettazione

Questo è un algoritmo che **decide il linguaggio**, anche se **è più lento**, perché deve controllare tutte le configurazioni.

Ma è comunque **un algoritmo deterministico** che termina!

##### ✅ Conclusione:

> Se un problema si può decidere usando al massimo `f(n)` celle di memoria,
> allora **esiste un algoritmo deterministico** che risolve lo stesso problema in **tempo `2^O(f(n))`**

E lo stesso vale anche nel caso **non deterministico**.
### in calcoli
![[Pasted image 20250425115910.png]]

### Teorema 6.11
>[!tip] Teorema 6.11
>![[Pasted image 20250425115947.png]]

🧠 **Cosa significa?**

Significa che **ogni linguaggio decidibile in tempo deterministico f(n)f(n)f(n)** ha **complemento** decidibile nello **stesso tempo deterministico f(n)f(n)f(n)**. Lo stesso vale per lo spazio.

> ✳️ In altre parole: **le classi deterministiche sono chiuse per complemento.**

---
🛠️ **Dimostrazione semplificata**

Partiamo dal caso temporale, cioè $DTIME[f(n)]=coDTIME[f(n)]$
Tanto quello spaziale è analogo

✳️ 1. Sia $L∈DTIME[f(n)]$

- Esiste una macchina di Turing deterministica T che decide L e impiega al massimo $O(f(∣x∣))$ passi su ogni input $x∈{0,1}^∗$.
    

---

### ✳️ 2. Costruisci una nuova macchina T′

- È **identica a T**, tranne per una cosa:
    
    - Inverte lo stato di **accettazione e rifiuto**:
        
        - se T(x)=$q_A$​ (accetta), allora T′(x)=$q_R$(rigetta)
        - e viceversa

👉 Quindi T′ **decide il complemento di L, cioè $L^C$ 

---

### ✳️ 3. Quanto tempo impiega T′?

- Fa **esattamente gli stessi passi** di T, quindi:
    
    $$dtime(T′,x)∈O(f(∣x∣))$$

---

### ✅ **Conclusione:**

- $L^C \in \text{DTIME[f(n)]}$
    
- Questo implica che ogni linguaggio $L∈DTIME[f(n)]⇒L^C∈DTIME[f(n)]$quindi:
    
    $$DTIME[f(n)]=coDTIME[f(n)]$$
🔁 **Per lo spazio?**
Stesso ragionamento:

## E per le non deterministiche?
>[!warning] non possiamo definirle a partire da una macchina!(quello fatto prima non vale per quelle non deterministiche)

### ⚠️ Uso della notazione $O$ nella teoria della complessità
## 1. Il problema dell'uso di $O$ nelle classi di complessità
L’uso della notazione **$O$-grande** (ad esempio `DTIME[f(n)]`) implica che:
> Le classi **non caratterizzano esattamente** i linguaggi, ma solo **asintoticamente**.
Infatti, se un linguaggio $L$ appartiene a $\text{DTIME}[f(n)]$, allora:
- Esiste una macchina di Turing che lo decide in tempo al più $c \cdot f(n)$, per qualche costante $c$ e per $n$ sufficientemente grande.
- Questo significa che $L$ **è contenuto in una serie infinita di classi DTIME più grandi**, perché:
$$
f(n) \in O(g(n)) \Rightarrow \text{DTIME}[f(n)] \subseteq \text{DTIME}[g(n)]
$$

---

## 2. Definizione formale di $f(n) \in O(g(n))$

Date due funzioni totali calcolabili $f, g : \mathbb{N} \to \mathbb{N}$, si dice che:

$$
f(n) \in O(g(n)) \quad \text{se} \quad \exists n_0 \in \mathbb{N}, \exists c \in \mathbb{N} \text{ tali che } \forall n \geq n_0, \; f(n) \leq c \cdot g(n)
$$

In parole semplici:
> $f$ cresce al massimo quanto $g$, a partire da un certo punto e fino a costanti moltiplicative.
---

>[!tip] Teorema 6.12
>![[Pasted image 20250425130406.png]]
>- Ok, allora il Teorema 6.12 ci dice che, se collochiamo un linguaggio L, ad esempio, in $DTIME[f(n)]$, allora L appartiene anche a tutte le classi $DTIME[g(n)]$ tali che, definitivamente, $f(n) ≤ g(n)$


Teorema 6.12 — Conseguenze pratiche
Il Teorema 6.12 ci dice che:
> Se collochiamo un linguaggio $L$, ad esempio, in $\text{DTIME}[f(n)]$,  
> allora $L$ appartiene anche a **tutte** le classi $\text{DTIME}[g(n)]$  
> tali che, definitivamente, $f(n) \leq g(n)$.

🤔 Ma attenzione!

> Se diciamo che $L \in \text{DTIME}[f(n)]$, **questo NON implica** che $L$  
> **non possa appartenere anche a una classe $\text{DTIME}[r(n)]$**  
> tale che, definitivamente, $r(n) \leq f(n)$!

In parole semplici:
> Potrebbe esistere un **algoritmo più efficiente** per decidere lo stesso linguaggio!

🧠 Conclusione operativa
Dire che $L \in \text{DTIME}[f(n)]$ **è solo metà del lavoro**.
- L’altra metà sarebbe dimostrare che **non esiste** alcuna funzione $r(n)$ tale che:
  $$
  r(n) \leq f(n) \quad \text{definitivamente}, \quad \text{e} \quad L \in \text{DTIME}[r(n)]
  $$

> Ma questo è **molto difficile da provare**, perché significherebbe escludere **tutti gli algoritmi possibili** più efficienti.

✅ Facciamo il punto

1. Gerarchia tra classi di complessità

Abbiamo già visto che, se collochiamo un linguaggio $L$ in $\text{DTIME}[f(n)]$,  
allora $L$ appartiene anche a **tutte** le classi $\text{DTIME}[f(n)^k]$ per ogni $k \in \mathbb{N}$

- perché, definitivamente: $f(n) \leq f(n)^k$
2. Esiste quindi una gerarchia infinita di classi

$$
\text{DTIME}[f(n)] \subseteq \text{DTIME}[f(n)^2] \subseteq \text{DTIME}[f(n)^3] \subseteq \cdots \subseteq \text{DTIME}[f(n)^k] \subseteq \mathcal{D}
$$

(dove $\mathcal{D}$ rappresenta l’insieme delle classi decidibili)
3. Teorema generale di inclusione
Data una funzione totale e calcolabile $f$, vale:
$$
\text{DTIME}[f(n)] \subseteq \text{DTIME}[g(n)]
$$

per ogni altra funzione totale e calcolabile $g$ tale che,  
definitivamente: $f(n) \leq g(n)$

4. Ma per rendere significativa la teoria della complessità...

> Sarebbe **auspicabile** che $\text{DTIME}[f(n)] \not\subseteq \text{DTIME}[g(n)]$  
> **quando $f(n)$ è molto più grande di $g(n)$**, ad esempio:

$$
f(n) = 2^{g(n)}
$$
🎯 Perché?

Perché, in definitiva, ciò che ci interessa è **poter distinguere** i problemi in base alla loro difficoltà:
> “Questo problema è **più difficile** di quest’altro”.

Da questo problema ci viene incontro il GAP THEOREM
>[!tip] GAP THEOREM
>![[Pasted image 20250425132855.png]]

Significa che **anche se la funzione $2^{f(n)}$ è molto più grande di $f(n)$** non ci sono nuovi problemi che si possono risolvere in $2^{f(n)}$ che **non erano già risolvibili** in $f(n)$

In altre parole: quella differenza di tempo **non ha effetto sulla potenza computazionale**

#### Andiamo a definire due insiemi di definizioni
>[!tip] Definizione 6.1
>![[Pasted image 20250425133450.png]]


>[!tip] Definizione 6.2
>![[Pasted image 20250425133508.png]]

Per intendere n 1 scriveremo $1^n$
- $1^5$ = 11111
visto che deve essere espresso in notazione unaria:
- la lunghezza dell’input è uguale al valore dell’input: |n| = n

Una funzione time-constructible è molto più che una funzione totale e calcolabile 
- è una funzione che può essere calcolata in tempo proporzionale al suo valore 
	- in soldoni, scrivere un ‘1’ sul nastro di output richiede alla macchina che la calcola di eseguire un numero costante di istruzioni (in media)

#### tutte le funzioni "regolari" che usiamo normalmente lo sono:

|Tipo|Esempio|
|---|---|
|**Polinomi**|f(n)=nkf(n) = n^kf(n)=nk, con kkk costante|
|**Esponenziali**|f(n)=2nf(n) = 2^nf(n)=2n, f(n)=nnf(n) = n^nf(n)=nn|
|**Altre**|Logaritmi, funzioni razionali, iterazioni di log, etc.|

📌 In pratica: **se puoi scriverla con una formula familiare, probabilmente è constructible**.

## 💣 Il problema del Gap Theorem

Il **Gap Theorem** ci dice che:
> Esiste una funzione calcolabile $f(n)$ **non time-constructible**  
> tale che:
> $$\text{DTIME}[2^{f(n)}] \subseteq \text{DTIME}[f(n)]$$

😱 Questo è controintuitivo!  
Aumentare le risorse **non sempre** significa poter risolvere più problemi.


✅ La salvezza: funzioni "ben comportate"
Se però **restringiamo l'attenzione** a funzioni:
- **time-constructible** per il tempo
- **space-constructible** per lo spazio
...allora **vale davvero l’intuizione** che:
> Più risorse ⇒ più potere computazionale


---

#### Teorema 6.14
>[!tip] Teorema 6.14 
>![[Pasted image 20250425135002.png]]

🔁 Esistono problemi risolvibili in $f(n)$ spazio ma **non** in $g(n)$.

---
#### Teorema 6.15
>[!tip] Teorema 6.5
![[Pasted image 20250425135048.png]]

🔁 Esistono problemi risolvibili in tempo $f(n)$ ma **non** in $g(n)$.
## 🔍 Significato dei limiti

Quando:

- $\displaystyle \lim_{n \to \infty} \frac{g(n)}{f(n)} = 0$
- oppure $\displaystyle \lim_{n \to \infty} \frac{g(n) \log g(n)}{f(n)} = 0$

...allora $f(n)$ cresce **molto più velocemente** di $g(n)$:  
la **distanza asintotica** tra le due funzioni diventa enorme.

✨ Conclusione
Il **Gap Theorem** mostra che esistono **collassi** tra classi di complessità,  
ma solo se usiamo **funzioni non-constructible**

Invece, i **teoremi di gerarchia** ci dicono:
> Se usiamo funzioni constructible e crescenti in modo regolare,  
> **aumentare le risorse permette davvero di risolvere problemi più complessi**.

✅ Quindi:

- Quando $f(n)$ è time-constructible:
  $$
  f(n) \gg g(n) \Rightarrow \text{DTIME}[f(n)] \not\subseteq \text{DTIME}[g(n)]
  $$
- Quando $f(n)$ è space-constructible:
  $$
  f(n) \gg g(n) \Rightarrow \text{DSPACE}[f(n)] \not\subseteq \text{DSPACE}[g(n)]
  $$

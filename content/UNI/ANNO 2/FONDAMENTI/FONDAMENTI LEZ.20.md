Dobbiamo continuare il discorso dell'ultima volta
![[Pasted image 20250423172024.png]]

## PASSO 2 (inverso)
per inverso si intende che per una grammatica ci sarà un automi a stati finiti non deterministico che la riconosce
#### Automa a stati finiti NON DETERMINISTICO
Un automa a stati finiti non deterministico (ASFND) è una quintupla $$\langle \Sigma, Q, q_{0}, Q_{F}, \delta \rangle$$dove:
- $\Sigma$ è l’alfabeto
- $Q$ è l’insieme degli stati
- $q_0$ è lo stato iniziale
- $Q_F$ è l’insieme degli stati finali
- $\delta$ è la **funzione di transizione non deterministica** 

>La differenza sostanziale con un ASFD sta nella funzione di transizione $\delta$:
>	invece di associare *un solo stato* come nei deterministici, qui associa ***un insieme di stati***

Formalmente: $$\delta: Q \times \Sigma \rightarrow P(Q)$$cioè: per ogni coppia (stato, simbolo), ti restituisce un insieme di stati possibili.
Questa è una funzione **TOTALE**.
- **una funzione totale** è una funzione che **è definita per ogni possibile input nel dominio**.

🔁 Le definizioni (configurazione, transizione, funzione estesa) sono simili.

##### ✅ Quando un ASFND accetta una parola?
> Se esiste almeno una sequenza di scelte che ti porta in uno stato finale.

Formalmente:
- Sia $x = x_1 x_2 \ldots x_n$
- L’ASFND **accetta** $x$ se **esistono** stati $q_1, \ldots, q_n$ tali che:
    - $q_1 \in \delta^*(q_0, x_1)$
    - $q_2 \in \delta^*(q_1, x_2)$
    - ...
    - $q_n \in \delta^*(q_{n-1}, x_n)$
    - $q_n \in Q_F$

📌 Cioè: **almeno un percorso porta in uno stato finale**.

>[!question]- Significato effettivo di $\delta^{*}$
>###### 📌 Cosa significa "$q_1 \in \delta^*(q_0, x_1)$"?
>- $\delta(q_0, x_1)$ = insieme degli stati raggiungibili leggendo un singolo simbolo
>
>- $\delta^*(q_0, x_1)$ = insieme degli stati raggiungibili leggendo una stringa (in questo caso di lunghezza 1)
>
👉 Quindi in questo caso specifico, $\delta^*(q_0, x_1)$ coincide con $\delta(q_0, x_1)$,  
ma la notazione con l’asterisco viene usata per uniformità, perché può generalizzare a stringhe più lunghe.

##### ✳️ Conclusione
Il **linguaggio accettato da un ASFND** è l’insieme delle parole per cui esiste almeno un cammino che termina in uno stato finale.

#### Altro modo (più compatto) per dire quello che abbiamo detto ora
> “Un **ASFND $A$** accetta una parola $x$ se $\delta^*(q_0, x) \cap Q_F \neq \emptyset$”
###### Tradotto
L'automa accetta la parola $x$ se, leggendo $x$ dallo stato iniziale $q_{0}$, esiste almeno un cammino che porta in uno stato finale.

In simboli:$$ L(A) = \{ x \in \Sigma^* : \delta^*(q_0, x) \cap Q_F \neq \emptyset \}$$

## Passo 3
>[!lemma] Teorema G.15
>Per ogni grammatica regolare $G = \langle V_N, V_T, P, S \rangle$ 
>esiste un ***ASFND*** $A_G = \langle \Sigma, Q, q_0, Q_F, \delta \rangle$ tale che $$L(G) = L(A_{G})$$
##### In parole semplici
Il teorema dice che **ogni grammatica regolare può essere simulata da un automa a stati finiti non deterministico**, cioè che i linguaggi generati da grammatiche regolari possono anche essere riconosciuti da questi automi non deterministici.

#### 🔍 Come funziona la dimostrazione
1. Costruzione dell'automa a partire dalla grammatica
	- Supponiamo di avere le produzioni nella forma $$B_{i} \rightarrow aB_{j} \ | a$$
	- L'automa $A_{G}$ verrà costruito in questo modo
		- L'alfabeto dell'automa è $\Sigma = V_T$
		- Gli stati $Q$ corrispondono ai simboli non terminali della grammatica, più uno stato $q_{F}$ 
		- Lo stato iniziale $q_{0}$ corrisponde a $S$
		- Le transizioni sono definite
			- $\text{se } B_i \rightarrow a B_j \text{ è una produzione, allora } q_j \in \delta(q_i, a)$
			- $\text{se } B_i \rightarrow a \text{ è una produzione, allora } q_F \in \delta(q_i, a)$
			- $\text{se } \varepsilon \in L(G), \text{ allora } q_F \in \delta(q_0, \varepsilon)$

#### 📍Dimostrazione
###### ✍️ Passaggi chiave:
Supponiamo che:
- La grammatica G abbia produzioni nella forma: $$
B_0 \rightarrow x_1 B_1, \quad
B_1 \rightarrow x_2 B_2, \quad
\dots, \quad
B_{n-2} \rightarrow x_{n-1} B_{n-1}, \quad
B_{n-1} \rightarrow x_n
$$
- Allora la parola $x = x_1 x_2 \dots x_n$ è derivabile da G, cioè $x  \in L(G)$

###### 🔁 Traduzione in termini di automa:

- Ai simboli $B_0, B_1, ..., B_{n-1}$​ della grammatica corrispondono stati $q_0, q_1, ..., q_{n-1}$​ nell’automa.
    
- Se la grammatica ha le produzioni viste sopra, allora l’automa ha le transizioni: $$
q_1 \in \delta(q_0, x_1), \quad
q_2 \in \delta(q_1, x_2), \quad
\dots, \quad
q_{n-1} \in \delta(q_{n-2}, x_{n-1}), \quad
q_F \in \delta(q_{n-1}, x_n)
$$
##### ✅ Conclusione:
La sequenza di produzioni nella grammatica corrisponde a una sequenza di transizioni dell’automa che porta dallo stato iniziale $q_0$​ allo stato finale $q_F$​, leggendo esattamente i simboli della parola $x$.

Quindi:
> $x \in L(G) \iff x \in L(A_G)$


## Passo 4
>[!lemma] Teorema G.16
>Per ogni *ASFND* $N A = \langle \Sigma, Q, q_{0}, Q_{F}, \delta \rangle$ esiste un ASFD $A = \langle \Sigma, Q_{D}, q_{0D}, Q_{FD}, \delta_{D} \rangle$ 
>tale che $$L(NA) = L(A)$$ 
##### In parole semplici
Il teorema dice che **qualsiasi automa a stati finiti non deterministico (ASFND)** può essere trasformato in un **automa deterministico (ASFD)** che riconosce esattamente lo stesso linguaggio.

##### ⚙️ Costruzione dell’automa deterministico A
Dati
- sia dato $NA = \langle \Sigma, Q, q_0, Q_F, \delta \rangle$
- costruiamo $A = \langle \Sigma, Q_{D}, q_{0D}, Q_{FD}, \delta_{D} \rangle$
- Nota come $A$ opera sullo stesso alfabeto di $NA$

Struttura
- Gli stati del nuovo automa deterministico $Q_D$​ sono tutti i **sottoinsiemi** degli stati di $NA$
	Ossia, se indichiamo $Q_{D} = \langle \omega_{1,} \dots, \omega_{H} \rangle$, ciascun $\omega_{i}$ è un sottoinsieme di $Q$ dell'automa $NA$
	
- poniamo $q_{0D} = q_{0}$
- poniamo $\{ \omega_{i} \subseteq Q : \omega_{i} \cap Q_F \neq \emptyset \}$
	Ossia gli stati finali di A sono tutti quei sottoinsiemi di $Q$ che contengono **almeno uno stato finale** di $NA$

- per ogni $a \in \Sigma$ e $\omega \in Q_{D}$, poniamo $\delta_D(\omega, a) = \omega'$ tale che $\omega' = \bigcup_{q \in \omega} \delta(q, a)$
	La frase significa:
		"Per calcolare la transizione dell’automa deterministico da un insieme di stati $\omega$, leggendo il simbolo $a$, guarda dove può andare ciascuno dei singoli stati in $\omega$ nell’automa originale non deterministico, e poi metti insieme tutti i risultati: quello sarà il nuovo stato."

- la U indica l'unione di tutti gli insiemi delle transizioni delta
- la macchina non deterministica ha una w che è un insieme di stati perché deve simulare la macchina non deterministica che ovviamente ne ha più di uno
	- è una sorta di stratagemma per avere più stati in una macchina deterministica

![[Pasted image 20250423174412.png]]

	

Ora che abbiamo definito A, dobbiamo dimostrare che $$x \in L(NA) \iff x \in L(A)$$ossia che la parola $x$ è accettata dall’automa non deterministico se e solo se è accettata da quello deterministico che abbiamo costruito.

Lo vediamo informalmente
![[Pasted image 20250423175216.png]]

Come vedi
- a sinistra abbiamo la computazione dell'automa NON DETERMINISTICO, il quale può avere più scelte
- a destra abbiamo la computazione dell'automa DETERMINISTICO


### Possiamo quindi concludere che
>[!lemma] Teorema G.17
>La classe dei linguaggi regolari coincide con la classe dei linguaggi decisi da automi a stati finiti deterministici.


### Chiusura: Unione, Intersezione e Complemento
Ci occupiamo ora di studiare se la proprietà di essere regolari si trasporta all’unione, all’intersezione e al complemento.

#### Unione
>[!example] Se due linguaggi $L_1$​ e $L_2$​ sono regolari, allora anche $L = L_1 \cup L_2$​ è regolare.
##### 🧠 Come lo si dimostra?
L’idea è usare un automa non deterministico (ASFND) per costruire un automa che riconosce $L_1 \cup L_2$, dato che conosciamo automi deterministici per $L_1$ e $L_2$.

##### ⚙️ Costruzione tecnica
Supponiamo di avere
- $A_1 = \langle \Sigma, Q_1, q_{01}, Q_{F1}, \delta_1 \rangle$: l’automa che decide $L_1$
    
- $A_2 = \langle \Sigma, Q_2, q_{02}, Q_{F2}, \delta_2 \rangle$: l’automa che decide $L_2$

Costruiamo un ASFND (automa non deterministico)  
$$NA = \langle \Sigma, Q, q_0, Q_F, \delta \rangle$$tale che riconosce $L_1 \cup L_2$.

##### Dettagli della costruzione
##### 🧩 Stati
L’insieme degli stati è: $Q = Q_1 \cup Q_2 \cup {q_0}$

Aggiungiamo un nuovo stato iniziale $q_0$, che non c’era né in $A_1$ né in $A_2$.

##### ✅ Stati finali
L’insieme degli stati finali è: $Q_F = Q_{F1} \cup Q_{F2}$

Cioè: sono finali tutti gli stati finali di $A_1$ e $A_2$.

##### 🔁 Funzione di transizione
Definita così:
- Dal nuovo stato iniziale $q_0$, per ogni simbolo $a \in \Sigma$:
    
    $\delta(q_0, a) = \delta_1(q_{01}, a) \cup \delta_2(q_{02}, a)$
👉 Cioè: da $q_0$, l’automa può **non deterministicamente** iniziare a comportarsi come $A_1$ o come $A_2$.

- Per tutti gli altri stati:
    - Se $q \in Q_1$, allora: $\delta(q, a) = \delta_1(q, a)$
    - Se $q \in Q_2$, allora: $\delta(q, a) = \delta_2(q, a)$

##### 🎯 Risultato
Questo automa $NA$ può decidere $L_1 \cup L_2$ perché:
- Dallo stato iniziale $q_0$, può simulare sia $A_1$ che $A_2$.
- Se la stringa appartiene a $L_1$ o a $L_2$, esiste una computazione che porterà a uno stato finale.
- E quindi $NA$ accetterà la parola.


#### Complemento
>[!example] Se $L$ è un linguaggio regolare, allora anche $L^C$ (il suo **complemento**) è regolare.
##### 🧠 Come si dimostra?
L'idea è
- partire da un automa $A$ che accetta $L$, linguaggio regolare
- costruire un automa $A^{C}$, complementare ad $A$, che accetta $L^{C}$
- dimostrare che questo nuovo automa è deterministico (ASFD) -> $L^{C}$ **è regolare**

Infatti, si vuole sfruttare il fatto che i **linguaggi regolari sono riconoscibili da automi deterministici (ASFD)**.

##### ⚙️ Costruzione dell’automa per il complemento
Supponiamo di avere un ASFD che riconosce $L$:
$$A = \langle \Sigma, Q, q_0, Q_F, \delta \rangle$$
→ questo è l’automa che accetta solo le parole di $L$.

##### ✨ Come si costruisce $A^C$?
Si mantengono **tutti gli elementi invariati**, **tranne gli stati finali**.
I nuovi stati finali saranno:  $$Q - Q_F$$
→ cioè **tutti e soli** gli stati dell’automa che **non erano finali** in $A$.
- quindi praticamente gli stati finali di $A^C$ sono gli stati non finali di $A$ 

Formalmente:  $$A^C = \langle \Sigma, Q, q_0, Q - Q_F, \delta \rangle$$
##### ✅ Conclusione
- L’automa $A^C$ accetta tutte le stringhe che **non** vengono accettate da $A$.
- Quindi $A^C$ accetta $L^C$, il **complemento** di $L$.
- Essendo $A^C$ un ASFD, allora **anche** $L^C$ è **regolare**.


#### Intersezione
>[!example] Se $L_1$ e $L_2$ sono due linguaggi regolari, allora $L = L_1 \cap L_2$ è regolare.
##### 🧠 Strategia (usando complementi e unione)
La dimostrazione sfrutta le due proprietà di chiusura già dimostrate
- la classe dei linguaggi regolari è chiusa rispetto al **complemento** <span style="background:#ff4d4f">*</span>
- la classe dei linguaggi regolari è chiusa rispetto all'**unione** <span style="background:#40a9ff">*</span>

E usa una **legge di De Morgan** dell'algebra degli insiemi $$L_1 \cap L_2 = (L_1^C \cup L_2^C)^C$$
##### ✨ Passaggi della dimostrazione
1. Se $L_{1}$ e $L_{2}$ sono regolai, allora anche i loro complementi $L_{1}^{C}$ e $L_{2}^{C}$ **sono regolari** <span style="background:#ff4d4f">*</span>
	
2. Dato che i linguaggi regolari è chiusa rispetto all'**unione** <span style="background:#40a9ff">*</span>, allora anche $L_{1}^{C} \cup L_{2}^{C}$ **è regolare**
	
3. Ora che abbiamo formato un linguaggio unico (regolare), per la proprietà <span style="background:#ff4d4f">*</span> sappiamo che il complemento di quel linguaggio **è regolare** $$(L_1^C \cup L_2^C)^C$$
4. Ma questo è proprio l'intersezione $$L_1 \cap L_2 = (L_1^C \cup L_2^C)^C$$
##### ✅ Conclusione:
👉 Quindi anche l’intersezione $L_1 \cap L_2$ è regolare.


---


## Espressioni regolari
Le espressioni regolari sono uno strumento che permette di descrivere una particolare classe di linguaggi

#### Definizione
Dati
- un insieme di caratteri $\Sigma$
- una parola `r` sull'alfabeto $\Sigma \cup \{+, *, (, ), \cdot, \emptyset\}$
	dove
	- $+$ → unione (scelta di accettazione tra due alternative)
		- Alternativa: `a + b` accetta "a" **o** "b"
	- $\cdot$ → concatenazione
		- Sequenza: `a · b` accetta "ab"
	- $*$ → chiusura di Kleene (ripetizione 0 o più volte)
		- Ripetizione: `a*` accetta "", "a", "aa", "aaa", ...
	- $(,)$ → per raggruppare
		- Come nelle operazioni matematiche: `(a + b)*`
	- $\emptyset$ → il linguaggio vuoto
		- Non accetta **nessuna parola**

Abbiamo un'espressione regolare se
1) $r = \emptyset$, oppure
2) $r \in \Sigma$, oppure
3) dato due espressioni regolari `s` e `t`, abbiamo che
	- $r = (s + t)$, oppure
	- $r = (s \cdot t)$, oppure
	- $r = s^{*}$

![[Pasted image 20250423180707.png]]

>[!example]- Secondo esempio
>Andiamo per parti
>- Tutte le `a` e le `b` sono espressioni regolari ($\in \Sigma$)
>- $(a \cdot b)$ -> **concatenazione** di due espressioni regolari -> regolare
>- $(a \cdot b)^{*}$ -> **chiusura di Kleene** -> regolare
>- $b \cdot (a \cdot b)^{*}$ -> **concatenazione** di due espressioni regolari ->  regolare
>- $(b \cdot (a \cdot b)^{*})$ -> **chiusura di Kleene** -> regolare
>- $a + (b \cdot (a \cdot b)^{*})$ -> **unione** di due espressioni regolari ->  regolare
>- $(a + (b \cdot (a \cdot b)^{*}))$ -> **raggruppamento** -> regolare


### Interpretazione e significato
Se interpretiamo i simboli speciali (`+`, `*`, `·`, `∅`) come **operazioni su insiemi di parole**, e se consideriamo ogni carattere dell’alfabeto come un "**singleton**" 
-> allora possiamo usare le **espressioni regolari per definire linguaggi** (insiemi di stringhe).

>[!question]  **Cosa significa "singleton" in questo contesto?**
> 
> Un **singleton** è un **insieme che contiene un solo elemento**.
> Nel contesto delle espressioni regolari:
> 
>- Ogni **carattere dell’alfabeto** (ad esempio `a`, `b`, `0`, `1`, ecc.) viene **interpretato come un insieme** contenente **solo quella parola**.
>     Per esempio:
>     - Il simbolo `a` rappresenta il linguaggio {a} → un **singleton**
>     - Il simbolo `b` rappresenta {b} → un **singleton**
>     - Il simbolo `0` rappresenta {0} → un **singleton**
##### 🔣 Interpretazione degli elementi di base
1. **Simbolo $\emptyset$**  
	L’espressione regolare $\emptyset$ definisce il **linguaggio vuoto**: $$
L = \emptyset$$→ cioè **nessuna stringa è accettata**.

2. **Simbolo $a \in \Sigma$**
	L'espressione regolare $a$ definisce il linguaggio $$L = \{a\}$$-> cioè un singleton che contiene solo la parola formata da $a$

##### 🔁 Operatori composti
Date due espressioni regolari `s` e `t`, che definiscono i linguaggi $L(s)$ e $L(t)$, allora:

1. **Unione `+`**
	- $(s + t)$ definisce: $$L = L(s) \cup L(t)$$-> ossia l'unione tra due parole

2. Concatenazione `·`
	- $(s \cdot t)$ definisce: $$
L = \{ xy : x \in L(s),\ y \in L(t) \}
$$-> ossia tutte le parole ottenuta concatenando una parola di $L(s)$ con una parola di $L(t)$
		💬 Ad esempio, se $L(s) = \{a\}$ e $L(t) = \{b\}$, allora $$L = \{ab\}$$

3. **Chiusura di Kleene `*`**
	- $s^{*}$ definisce: $$
L = \text{tutte le concatenazioni di } 0 \text{ o più parole in } L(s)
$$
	- include
		- $\varepsilon$ (stringa vuota → 0 ripetizioni)
		- tutte le stringhe ottenute concatenando **1, 2, 3, ...** elementi di $L(s)$
			così come, ad esempio, $Σ*$ è l’insieme delle parole che sono concatenazione di  (0 o più) caratteri di $Σ$

![[Pasted image 20250423181308.png]]


>[!question] Ma possiamo definire un qualunque linguaggio mediante una espressione regolare?
> **NO**, per il seguente teorema.

>[!lemma] Teorema G.18
>Un linguaggio è generato da una grammatica di tipo 3 $\iff$ **esso è definito da una espressione regolare**.

Riprendendo, e collegando a G.18, il teorema G.17, che dice 
	**grammatica regolare ↔ automa a stati finiti**

Possiamo affermare che
##### Un linguaggio regolare è:
- ✅ un linguaggio **generato da una grammatica di tipo 3**
- ✅ un linguaggio **deciso da un automa a stati finiti (deterministico o non)**
- ✅ un linguaggio **definito da un’espressione regolare**

##### 🧠 In pratica:
Se riesci a scrivere un’espressione regolare, allora esiste **un automa finito che la riconosce**, e **una grammatica regolare che la genera**, e viceversa.
Hai quindi **tre modi equivalenti** per descrivere un linguaggio regolare!


---

#### Introduzione alla complessità e Torre di Hanoi

>[!tip] Riassunto di tutto ciò
>Ci sono problemi che sappiamo risolvere ma non lo facciamo perché ci vuole talmente tanto tempo che sarebbe infattibile.
>
>Un esempio è quello della torre di Hanoi a 64 dischi, che dopo il relativo calcolo di complessità temporale $(2^n)$ si scopre ci vorrebbe talmente tanto tempo per risolverla che non basterebbe la vita umana sulla terra fino allo spegnimento del sole.

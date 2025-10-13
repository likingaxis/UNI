#### Come è strutturato un problema
Dato un quesito abbiamo inoltre
1) un <u>insieme</u> di oggetti conosciuti
	definito ***insieme delle istanze***
2) all'interno di un secondo <u>insieme</u> di oggetti
	definito ***insieme delle soluzioni possibili*** 
3) dobbiamo cercare gli <u>oggetti che soddisfano certi dati vincoli</u>
4) e, sulla base degli oggetti trovati, dobbiamo <u>rispondere al quesito posto</u>

### Esempio 1
>[!problema] PROBLEMA: dato un numero intero $n$, trovare tutti i divisori di $n$
1) L'insieme delle istanze del problema le definiamo con la lettera $𝕴$ 
	<u>un elemento</u> di $𝕴$ corrisponde ad una istanza del problema.
	
	Nel nostro esempio abbiamo che $$𝕴 = \mathbb{N}$$ossia tutti i numeri naturali
2) Abbiamo poi l'***insieme delle soluzioni possibili***, che definiamo come $S(n)$   
	$S(n)$ descrive tutti gli oggetti che dobbiamo testare per verificare se soddisfano i vincoli del problema
	
	Nel nostro esempio abbiamo che $$S(x) = \{y \in \mathbb{N} : y \le n\}$$ossia tutti i numeri che vanno da `1` a `n` sono candidati da controllare per trovare i divisori di `x`
	
3) All'interno dell'insieme delle *soluzioni possibili* dobbiamo andare a trovare le ***soluzioni effettive*** ossia quelle soluzioni che soddisfano effettivamente i vincoli del problema.
	Andiamo a definire questo insieme $\eta (S(n))$.
	
	Nel nostro caso abbiamo che $$\eta(S(n)) = \{y \in S(n) : \exists \ h \in N \ [n = y \cdot h]\}$$Ossia 
	- presa una `y` dall'insieme delle soluzioni possibili 
	- se esiste una `h` che, moltiplicata a `y`, mi restituisce `n`
	- allora `y` è un divisore di `n`

4) Dobbiamo descrivere ora la risposta del problema
	Per farlo, definiamo una funziona $\rho$ che associa, all'insieme delle soluzioni effettive per l'istanza `n`, una risposta scelta nell'insieme `R` delle risposte
	
	Nel nostro caso abbiamo che $$R = 2^\mathbb{N}$$ ossia la risposta ad un'istanza del problema è un sottoinsieme di $\mathbb{N}$ 
	  
	E, per ogni istanza del problema, la funzione è definita come $$\rho(\eta(S(n))) = \eta(S(n))$$Ossia, in questo caso specifico, l'***insieme delle soluzioni effettive coincide con la risposta del quesito***.
### Esempio 2
>[!problema] PROBLEMA: dato un numero intero $n$, verificare se $n$ è primo


Qui i punti 1, 2 e 3 sono IDENTICI, a quelli di prima, perché
1) Lavoriamo ancora sui naturali, quindi $$𝕴 = \mathbb{N}$$
2) Dobbiamo comunque cercare se esistono dei divisori per `n`, quindi intanto prendiamo un insieme con TUTTI i numeri da `1` a `n` $$S(x) = \{y \in \mathbb{N} : y \le n\}$$
3) Per capire se un numero è primo, prendiamo il numero e cerchiamo i divisori di `n` $$\eta(S(n)) = \{y \in S(n) : \exists \ h \in N \ [n = y \cdot h]\}$$
Ora, l'unico punto che cambia, giustamente, è il 4 (perché si richiede una risposta diversa da prima)
4) Quello che andiamo a fare ora è utilizzare $\rho$ come "filtro" per $\eta(S(n))$ 
	Dato che noi cerchiamo un numero primo, sappiamo che tutti i possibili divisori di `n` sono solo 
	- `1`
	- `n`
	
	Quindi andiamo a specificare questa cosa nella funzione $$\rho(\eta(S(n))) = [\eta(S(n)) = \{1, n\}]$$
	E, in questo caso, la nostra `R` sarà $$R = \{\text{vero, falso}\}$$perché dobbiamo solo dire 
	- Sì, è primo
	- No, non è primo (down)

### Esempio 3
>[!problema] PROBLEMA: dato un numero intero $n$, calcolare UN divisore `d` non banale di $n$
Per DIVISORI NON BANALI si intende tutti tranne `1` e `n`

Anche in questo caso 1, 2 e 3 sono IDENTICI a prima

Ora, il 4.
4) Abbiamo che $$R = \mathbb{N}$$ perché dobbiamo scegliere UN SOLO NUMERO
	E, la nostra funzione sarà $$\rho(\eta(S(n))) = \eta(S(n)) \ \ \backslash \ \  \{1, n\}$$da cui poi dobbiamo estrarre l'elemento `d`

>[!warning] ATTENZIONE: `d` potrebbe anche non esistere!

### Esempio 4
>[!problema] PROBLEMA: dato un numero intero $n$, calcolare I<u>L PIÙ GRANDE</u> divisore `d` non banale di $n$
È identico a quello sopra, cambia solo che alla fine tiro fuori il più grande da $\rho$ 

---

## Tipi di problemi
#### Problemi di ottimizzazione
L'esempio 4
>[!problema] PROBLEMA: dato un numero intero $n$, calcolare I<u>L PIÙ GRANDE</u> divisore `d` non banale di $n$

È un ***problema di ottimizzazione*** in quanto alle soluzioni effettive è associata una misura e viene richiesto di trovare <u>la soluzione effettiva di misura massima</u> (come in questo caso), oppure <u>minima</u>.


#### Problemi di ricerca
L'esempio 3
>[!problema] PROBLEMA: dato un numero intero $n$, calcolare UN divisore `d` non banale di $n$

È un ***problema di ricerca*** in quanto viene richiesto di trovare (e mostrare) <u>una qualunque soluzione effettiva</u> 
- sono i problemi con i quali abbiamo maggiore confidenza


#### Problemi di enumerazione
L'esempio 1
>[!problema] PROBLEMA: dato un numero intero $n$, trovare tutti i divisori di $n$

È un ***problema di enumerazione***, in quanto ci viene richiesto di elencare <u>tutte le soluzioni effettive</u>.


#### Problemi di decisione
L'esempio 2
>[!problema] PROBLEMA: dato un numero intero $n$, verificare se $n$ è primo

È un ***problema di decisione*** (o ***decisionale***), in quanto ci viene richiesto di decidere se l’<u>istanza possiede una certa proprietà</u>


## Problemi e macchine
I due diversi tipi di macchine di Turing risolvono questi problemi.
In particolare utilizziamo
- **Trasduttori** per i problemi di *ricerca*, di *enumerazione*, e di *ottimizzazione* 
- **Riconoscitori** per i problemi di *decisione*

NOI CI OCCUPEREMO SOLO DI PROBLEMI DECISIONALI.
## Problemi decisionali
>[!definizione] Definizione formale (e generale) di PROBLEMA
>Da quello che abbiamo visto prima possiamo dire che un problema, in generale, può essere descritto da una quintupla $$\langle \ ℑ, \ S, \ \eta, \ \rho, \ R \ \rangle$$dove
>- $\eta$ è il sottoinsieme di S che specifica quali, fra le soluzioni possibili, sono le soluzioni effettive per una data istanza $x ∈ ℑ$
>- $\rho$ è la funzione che associa all’insieme delle soluzioni effettive $𝜂(S(x))$ una risposta (elemento di R) all’istanza `x` del problema

Nel caso dei ***problemi decisionali***, abbiamo che $$R = \{\text{vero, falso}\}$$Questo significa che $\rho$ **è un predicato**
- ossia una **funzione booleana**
	- o, per dirla meglio <u>una proposizione logica il cui valore di verità dipende da qualche incognita</u>

Allora possiamo riassumere $\eta, \ \rho, \ R$ in un unico predicato $\pi$ $$\pi(x, S(x)) = \text{vero} \iff \text{ l’insieme delle soluzioni possibili per x soddisfa i vincoli del problema}$$
E quindi, un *problema decisionale* è descritto da una tripla $$\langle \ 𝕴, \ S, \ \pi \ \rangle$$
>[!lemma]- COSA FACILE CHE CHIEDE SEMPRE ALL'ESAME
>Dato un problema, formalizzarlo con la terna $$\langle \ 𝕴, \ S, \ \pi \ \rangle$$

### Problemi decisionali: esempi
#### Esempio 1
![[Pasted image 20250512212752.png]]
Descrizione
##### 1. Insieme delle **istanze** $𝕴$
```
𝒮 = { ⟨G, s, t, k⟩ : G è un grafo non orientato ∧ s,t ∈ G ∧ k ∈ ℕ }
```
📌 Qui stiamo dicendo che:
- Un’**istanza** del problema è una quatupla $\langle \ G, \ s, \ t, \ k \ \rangle$, dove:
    - G è un grafo valido (non orientato),
    - s e t sono due nodi del grafo,
    - k è un numero naturale (lunghezza cercata del percorso).
##### 2. Insieme delle **soluzioni possibili** 𝒮(G, s, t, k)
```
𝒮(G, s, t, k) = { ⟨u₀, u₁, ..., uₖ⟩ : ogni uᵢ è un nodo del grafo G }
```
📌 Qui stiamo elencando **tutte le sequenze di nodi** lunghe k+1, potenziali percorsi da s a t:
- Ogni sequenza rappresenta un cammino che _potrebbe_ essere lungo **k** archi.
- Non sappiamo ancora se è valido, solo che ha la **forma giusta**.
##### 3. Predicato di verifica **π(G, s, t, k, 𝒮(G, s, t, k))**
```
π(G, s, t, k, 𝒮(G, s, t, k)) =
    ∃ ⟨u₀, ..., uₖ⟩ ∈ 𝒮(G, s, t, k) :
      u₀ = s ∧ uₖ = t ∧ ∀i ∈ [0, k−1], (uᵢ, uᵢ₊₁) ∈ E
```
📌 Questo **controlla** che:
- La sequenza parte da **s** e arriva a **t**
- Ogni coppia consecutiva di nodi sia **connessa da un arco** (cioè esista nel grafo),
- Quindi: **verifica che sia un vero cammino** da s a t di lunghezza k.

##### ESEMPIO 2
![[Pasted image 20250509171613.png]]
Qui detta molto in breve
- ho un insieme di variabili booleane $x_{0}, x_{1}, ... , x_{n}$
- ho poi un predicato $f$ costituito da
	- queste variabili
	- e operatori ∧, ∨ e ¬
- devo trovare un'assegnazione $a$ che mi renda $f$ vera


>[!tip] NOTA BENE: ciascun problema decisionale può essere descritto da diverse triple $\langle \ 𝕴, \ S, \ 𝝅 \ \rangle$!


---

## Da problema a linguaggio
![[Pasted image 20250509172043.png]]


### Codifica
Riprendendo l'esempio 2 che abbiamo visto poco fa
![[Pasted image 20250509172439.png]]
Questo esempio, che è generale, viene definito ***SAT***

Prendiamo in considerazione un suo caso particolare: ***3SAT***
![[Pasted image 20250509172622.png]]
In pratica, abbiamo un SAT ma 
- ogni ***clausola*** (ossia le parentesi, che noi chiamiamo $c_{j}$) è l'or (`∨`) di tre ***letterali*** (variabili / variabili negate).

>[!question] Come codifichiamo gli elementi di $𝕴$?
>Abbiamo due possibilità
>1. codifichiamo la STRUTTURA di  `f`
>2. codifichiamo "il SIGNIFICATO" di `f`

### Codifica $\chi_{1}$: codifichiamo la STRUTTURA di `f`
##### 🧠 L'idea di fondo
Hai:
- Un insieme di variabili: `X = {x₁, x₂, ..., xₙ}`
- Una formula `f = c₁ ∧ c₂ ∧ ... ∧ cₘ`, dove ogni clausola `cᵢ` è tipo `x₁ ∨ ¬x₂ ∨ x₃`

Vogliamo codificare **questa formula** usando bit.

##### ✏️ Come funziona la codifica?
###### 1. Codifichiamo le variabili
Le variabili vengono rappresentate in binario, una alla volta. Esempio:
- Se `X = {x₁, x₂, x₃}`, allora:
    - `x₁` è `100`
    - `x₂` è `010`
    - `x₃` è `001`
###### 2. Letterali nelle clausole
Per ogni **letterale** (cioè variabile o negazione):
- Se **NON negato**, si mette `0` davanti alla variabile.
- Se **negato**, si mette `1` davanti.
	Esempio:
	- `x₁` → `0 100`
	- `¬x₂` → `1 010`
###### 3. OR (`∨`) è rappresentato con il simbolo `'2'`
###### 4. AND (`∧`) è rappresentato con il simbolo `'3'`
###### 5. Si mette all’inizio un `'4'` per ogni variabile di `X` (serve per dire quante ce ne sono)

##### 🧪 Esempio
```
X = {x₁, x₂, x₃}
f = c₁ ∧ c₂ 
con:
c₁ = x₁ ∨ x₂ ∨ x₃
c₂ = x₁ ∨ ¬x₂ ∨ x₃
```
Codifica:
```
444       ← tre 4 perché ci sono 3 variabili
0 100     ← x₁
2         ← OR
0 010     ← x₂
2
0 001     ← x₃
3         ← AND
0 100     ← x₁
2
1 010     ← ¬x₂
2
0 001     ← x₃
```
###### ✅ Risultato finale
![[Pasted image 20250509181522.png]]

### Codifica $\chi_{2}$: codifichiamo il SIGNIFICATO di `f`
Sappiamo che possiamo **rappresentare completamente f** dicendo che valore restituisce in **ogni possibile combinazione di input** → questa è la **tavola di verità**.

Dato che la `f` della nostra istanza $\langle \ X, \ f \ \rangle$ di 3SAT è definita su $$\text{\{vero, falso\}}^{|X|}$$e poiché `X` è un insieme finito -> allora possiamo codificare `f` in ***forma esplicita*** e la sua <u>tabella di verità sarà finita</u>.

Per esempio: ![[Pasted image 20250509181251.png]]
Codificando 
- vero con ‘`1`’ 
- falso con ‘`0`’
e scrivendo le righe della tavola una di seguito all’altra, separate da ‘`2`’
Otteniamo:
![[Pasted image 20250509181622.png]]


### Perfetto, ora ci manca solo fornire una risposta al problema
Data $\langle \ X, \ f \ \rangle$ istanza di 3SAT, per decidere se `f` è <font color="#548dd4">soddisfacibile</font>.
- ossia esiste una assegnazione `a` di valori in $\text{\{vero, falso\}}$ alle variabili in `X` tali che $$f(a(X))= \text{vero}$$
consideriamo il seguente algoritmo:
1)  calcola $n = |X|$; 
2) per ogni assegnazione di verità `a` all’insieme delle `n` variabili in `X` : verifica se $$f(a(X))= \text{vero}$$ e, in tal caso termina nello stato di accettazione $q_{A}$; 
3) se non ha mai terminato in $q_{A}$ al passo 2, termina nello stato di rigetto$q_{R}$. 

> [!tip]- Quindi
> Dobbiamo sfruttare questo algoritmo che 
>- prende in pasto una istanza codificata o secondo $\chi_{1}$ o secondo $\chi_{2}$ 
>- e restituisce un risultato.
>
>In particolare, abbiamo 
>- un solo algoritmo
>- a questo algoritmo passiamo, una alla volta, entrambe le codifiche
>- dobbiamo verificare quale codifica "costa" meno.

#### Utilizzando $\chi_{1}$
##### FASE 1
![[Pasted image 20250509184510.png]]![[Pasted image 20250509184519.png|center|500]]
![[Pasted image 20250509184526.png|center|500]]

###### FASE 2
![[Pasted image 20250509184731.png]]
Quindi in pratica, 
- legge tutte le assegnazioni (ogni singolo blocco prima di un `5`)
- applica ciascuna assegnazione dentro `f`
- se almeno una restituisce `1` -> accetta
- se NESSUNA restituisce `1` -> rigetta

##### Quanto è $dtime(T_{1}, \ \chi_{1}(X, f))$?
![[Pasted image 20250509185210.png]]
Sono solo calcoli, però l'importante è capire che con questa codifica, `dtime` è <u>POLINOMIALE</u> in `n` 


#### Utilizzando $\chi_{2}$
![[Pasted image 20250509185341.png]]
##### Quando è $dtime(T_{2}, \ \chi_{2}(X, f))?$
![[Pasted image 20250509185431.png]]
Quindi in questo caso `dtime` è <u>LINEARE</u> in `n`!


Ora, ricordando che un linguaggio è nella classe $P$ se *esiste una macchina di Turing deterministica che lo decide in tempo polinomiale*, possiamo concludere che il linguaggio associato a 3SAT appartiene a P? 
- Osserva che T1 e T2 implementano lo stesso algoritmo 
- ma operano su due codifiche differenti!

>[!question] Ma quindi scusa, la caratteristica *essere un algoritmo polinomiale* dipende dal modo in cui è codificato l’input?
>Si e no.

Se io prendo $\chi_{1}$ so che l'algoritmo, data una istanza `x`, impiega tempo <u>POLINOMIALE</u>.
Ora, se io prendo la stessa istanza ma la allungo IRRAGIONEVOLMENTE di lunghezza polinomiale e do tutto questo in pasto all'algoritmo, mi sembrerà di aver utilizzato tempo <u>LINEARE</u>!
	Ma in realtà non è così, perché ho incrementato in maniera insensata l'input![[Pasted image 20250509191736.png]]

Se invece prendo $\chi_{2}$, l'algoritmo, data una istanza `x`, impiega tempo <u>LINEARE</u>.
<font color="#ff0000">Però l'istanza cos'è?</font> Letteralmente la codifica della tabella di verità.
<font color="#ff0000">E quando ci vuole per costruire una tabella di verità?</font> $2^{n}$ passi.
Quanto è lungo l'input? $2^{n}$, quindi $\chi_{2}$ è <u>esponenzialmente più lunga</u> di $\chi_{1}$
Quindi, da qualche parte, anche in questo caso, impiego tempo <u>POLINOMIALE</u>.

> Possiamo nascondere una complessità, ma non possiamo eliminarla davvero


---

### Codifiche (<font color="#00b0f0">ir</font>)ragionevoli
Prendiamo in considerazione le due codifiche di prima
- **χ₁**: codifica **strutturale** della formula. 
	È compatta: dice solo quali sono le clausole, i letterali, ecc.
- **χ₂**: codifica **esplicita** della formula. 
	Dice già per ogni assegnazione se la formula è vera o falsa → è **la tabella di verità**.

##### ⛔ 3. Perché χ₂ è "ingannevole"?
Perché **sembra** che con χ₂ tu abbia un algoritmo che funziona **in tempo lineare**:
- Leggi la tabella → rispondi subito: **"f è soddisfacibile? Sì/No"**

⚠️ Ma attenzione:  
**Quanto tempo hai impiegato per costruire χ₂?**
- Hai dovuto calcolare **2ⁿ righe di tabella**, per ogni combinazione delle variabili.
- Quindi hai impiegato **tempo esponenziale** prima, e solo poi hai un input lungo.

##### 🤯 4. Cosa vuol dire che è _irragionevole_?
Una codifica `χ` è **irragionevole** se:
> Esiste un’altra codifica `χ′` che rappresenta le stesse istanze,  
> ma `χ(x)` è **molto più lunga** di `χ′(x)`, diciamo che è **più che polinomialmente** (tipo $n^{n}$).

In altre parole:  $$|\chi(x)| \geq F(|\chi'(x)|)$$ con F **più che polinomiale** (es. esponenziale).

##### 💡 5. Perché è un problema?
Perché **la complessità di un algoritmo si misura in base alla lunghezza dell’input**.  
Quindi:
- Se codifichi in modo **lunghissimo**, anche un algoritmo lento **sembra veloce**.
- Ma **stai barando**: stai **nascondendo il lavoro** dentro all’input.

##### ✅ Conclusione:
- **χ₁ è una codifica ragionevole**: è compatta, riflette il vero lavoro da fare.
- **χ₂ è una codifica irragionevole**: è lunga, nasconde il lavoro fatto prima.


### Codifiche ragionevoli
![[Pasted image 20250509195217.png]]
Qui in poche parole ti dice
- date due codifiche $\chi$ e $\chi^{'}$
- $\chi$ può anche essere più grande di $\chi^{'}$
- però esiste un polinomio $p$ che, qualunque sia l'istanza che prendi, farà si che la lunghezza di $\chi$ non sia MAI PIÙ GRANDE della lunghezza di $\chi^{'}$ data in pasto al polinomio

>[!tip] $\Gamma$ lo ha usato la prof nella slide precedente a questa foto per indicare un generale problema.


#### Quindi, in breve
- Se $\chi$ è **esponenzialmente più lunga** di $\chi^{'}$ → $\chi$ è _irragionevole_
- Se $\chi$ è al più _polinomialmente_ più lunga di $\chi^{'}$ → $\chi$ è _ragionevole_


![[Pasted image 20250509195818.png]]
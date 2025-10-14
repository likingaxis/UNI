# 📘 Capitolo 2 – Variabili casuali discrete e aspettativa

## 🎯 Introduzione

Nel capitolo precedente abbiamo visto come la probabilità serva a stimare quanto spesso accadono certi eventi.  
Ora facciamo un passo oltre: vogliamo capire **quali valori numerici può assumere un evento casuale** e, soprattutto, **quanto ci aspettiamo in media da esso**.

Per farlo introduciamo uno strumento fondamentale: la **variabile casuale**, detta anche *variabile aleatoria*.

---

## 🔹 2.1 – Variabili casuali e aspettativa

Una **variabile casuale (o aleatoria)** è una funzione che associa a ciascun possibile esito di un esperimento casuale un numero reale:

$$
X : \Omega \to \mathbb{R}
$$

dove:

- $\Omega$ è lo **spazio campionario**, cioè l’insieme di tutti i possibili esiti;  
- $X(\omega)$ è il numero che la variabile assegna all’esito $\omega$.

👉 Quindi $X$ **non è un evento**, ma una quantità che dipende dal caso.

---

### 🔸 Esempio 1 – Il lancio di un dado

Lanci un dado a sei facce.

$$
\Omega = \{1, 2, 3, 4, 5, 6\}
$$

Definiamo la variabile casuale:

$$
X(\omega) = \omega
$$

In altre parole, $X$ è il numero uscito sul dado.  
Ogni valore $x$ ha probabilità:

$$
\Pr(X = x) = \frac{1}{6}, \quad x = 1, 2, \dots, 6
$$

---

## 🔹 2.1.1 – Il concetto di aspettativa

Il **valore atteso** o **aspettativa**, indicato con $E[X]$, è la **media ponderata** di tutti i valori che $X$ può assumere, usando come peso le loro probabilità:

$$
E[X] = \sum_x x \cdot \Pr(X = x)
$$

👉 In parole semplici:  
$E[X]$ rappresenta il **valore medio teorico** che otterremmo se ripetessimo l’esperimento infinite volte.

---

### 🔸 Esempio 2 – La media del dado

$$
E[X] = \frac{1 + 2 + 3 + 4 + 5 + 6}{6} = 3.5
$$

⚠️ **Nota:** 3.5 non è un valore che può uscire, ma è la media teorica dei risultati.  
Se lanci un dado molte volte, la media dei numeri ottenuti si avvicinerà a 3.5.

👉 È un concetto astratto ma **predittivo**: ci dice “in media” cosa aspettarci dal fenomeno.

---

## 🔹 2.1.2 – Differenza tra evento e variabile casuale

Un **evento** è una proposizione che può essere vera o falsa (es. “esce 6”).  
Una **variabile casuale** assegna un numero a ciascun evento possibile.

Esempio:

- Evento: “esce un numero pari”  
  → $\Pr(\text{pari}) = \frac{3}{6} = 0.5$

- Variabile casuale: “il numero uscito”  
  → $E[X] = 3.5$

📘 Quindi $E[X]$ **non è una probabilità**, ma la **media** dei valori numerici che la variabile può produrre.

---

## 🔹 2.1.3 – Famiglie di variabili casuali: indici sopra e sotto

Spesso dobbiamo descrivere più variabili casuali collegate, come in una sequenza di esperimenti.

$$
X_1, X_2, \dots, X_n
$$

rappresentano $n$ variabili distinte, ad esempio i risultati di più lanci di un dado.

- $X_1, X_2, X_3$: risultati del primo, secondo, terzo dado  
- $(X_1)^2$ o $X^2$: il quadrato del valore di $X$, utile per la varianza o per $E[X^2]$

---

### 🔸 Esempio pratico

Lanci due dadi tre volte.

- $X^1_1$: risultato del primo dado al primo lancio  
- $X^2_1$: risultato del secondo dado al primo lancio  
- $X^1_2$, $X^2_2$: risultati al secondo lancio  

Definiamo la somma:

$$
S_i = X^1_i + X^2_i
$$

$S_i$ è la somma dei due dadi nell’esperimento $i$-esimo.  
Tutte queste sono variabili casuali, ciascuna con la propria aspettativa.

---

## 🔹 2.1.4 – Linearità dell’aspettativa

Una delle proprietà più eleganti e potenti:

$$
E[X + Y] = E[X] + E[Y]
$$

ed è **sempre vera**, anche se $X$ e $Y$ **non sono indipendenti**.

---

### 💡 Esempio 3 – Due dadi

Lanci due dadi e definiamo:

$$
X_1 = \text{risultato del primo dado}, \quad X_2 = \text{risultato del secondo dado}
$$

Sia $X = X_1 + X_2$.  
Allora:

$$
E[X] = E[X_1 + X_2] = E[X_1] + E[X_2]
$$

Poiché $E[X_1] = E[X_2] = 3.5$, otteniamo:

$$
E[X] = 3.5 + 3.5 = 7
$$

👉 Il valore medio della somma dei due dadi è **7**.

---

## 🔹 2.1.5 – Quando l’aspettativa non esiste

Se i valori possibili di $X$ crescono troppo velocemente rispetto alle loro probabilità,  
la somma che definisce $E[X]$ **non converge**.

Esempio:

$$
X = 2^i \quad \text{con probabilità} \quad \frac{1}{2^i}
$$

Allora:

$$
\sum_i 2^i \cdot \frac{1}{2^i} = \infty \quad \Rightarrow \quad E[X] = \infty
$$

Questo succede con **distribuzioni a coda pesante**, tipiche di fenomeni economici o di rete.

---

## 🔹 2.1.6 – Inizio: la disuguaglianza di Jensen

Spesso ci interessa non solo $E[X]$, ma anche $E[f(X)]$, cioè la media di una funzione di $X$.  
Se $f$ è **convessa**, allora vale la **disuguaglianza di Jensen**:

$$
E[f(X)] \ge f(E[X])
$$

---

### 💡 Esempio 4 – L’area di un quadrato

Sia $X$ la lunghezza del lato di un quadrato casuale e $f(X) = X^2$ la sua area.  
Poiché $f$ è convessa:

$$
E[X^2] > (E[X])^2
$$

👉 La **media delle aree** è più grande dell’area calcolata sulla **media dei lati**.  
Questo spiega perché la varianza non è mai nulla anche quando la media è costante.

---

## 🧩 Sintesi finale

| **Concetto** | **Significato** | **Esempio / Formula** |
|:-------------|:----------------|:-----------------------|
| Variabile casuale | Funzione che assegna un numero a ogni esito possibile | $X : \Omega \to \mathbb{R}$ |
| Probabilità di un valore | Quanto spesso $X$ assume un certo valore | $\Pr(X = x)$ |
| Aspettativa $E[X]$ | Media pesata dei valori di $X$ | $E[X] = \sum x \Pr(X = x)$ |
| Linearità | La media della somma è la somma delle medie | $E[X + Y] = E[X] + E[Y]$ |
| Jensen | Per funzioni convesse: $E[f(X)] \ge f(E[X])$ | $E[X^2] > (E[X])^2$ |
| Indici $X_1, X_2$ | Sottoscritti = variabili diverse, soprascritti = esperimenti diversi | $S_i = X^1_i + X^2_i$ |
# 📘 Capitolo 2 – Variabili casuali discrete e aspettativa  
## 🔹 Pagine 27–32 – Variabili Bernoulli, Binomiali e Aspettativa Condizionata

---

## 🧩 Introduzione

Abbiamo imparato che una **variabile casuale** (o *aleatoria*) è una funzione che associa un numero a un evento casuale.  
Ora ci concentriamo su due tipi fondamentali di variabili discrete — **Bernoulli** e **Binomiale** — e su come calcolare **aspettative condizionate**, cioè medie “sapendo che qualcosa è successo”.

Queste idee sono la base della probabilità applicata, dagli algoritmi randomizzati alle simulazioni statistiche.

---

## 🔹 2.2 – Variabili casuali Bernoulli e binomiali

### 🎯 Variabile di Bernoulli

La **variabile di Bernoulli** è il modello più semplice: può valere solo 0 o 1.

$$
X =
\begin{cases}
1 & \text{con probabilità } p \\
0 & \text{con probabilità } 1 - p
\end{cases}
$$

📘 **Interpretazione pratica:**

- $1$ = successo (es. “esce testa”, “evento accaduto”)  
- $0$ = fallimento

---

### 💡 Esempio intuitivo

Lancio una moneta con probabilità $p = 0.7$ di testa.  
Definisco $X = 1$ se esce testa, $X = 0$ se esce croce.  
→ $X$ è una variabile di Bernoulli.

---

### 📊 Aspettativa e varianza

$$
E[X] = 1 \cdot p + 0 \cdot (1 - p) = p
$$

👉 In media, il valore di $X$ coincide con la **probabilità di successo**.

La **varianza**, cioè quanto $X$ varia rispetto alla sua media, è:

$$
\mathrm{Var}(X) = p(1 - p)
$$

📈 È massima quando $p = 0.5$, cioè quando il risultato è più incerto.

---

## 🔹 Variabile Binomiale

Ora immaginiamo di ripetere l’esperimento **n volte**, in modo indipendente.  
Ogni prova ha probabilità $p$ di successo.  
Definiamo:

$$
X_i =
\begin{cases}
1 & \text{se la i-esima prova è un successo} \\
0 & \text{altrimenti}
\end{cases}
$$

La **somma dei successi**:

$$
X = X_1 + X_2 + \dots + X_n
$$

è una **variabile binomiale**.  
Essa conta **quanti successi** otteniamo in $n$ prove.

---

### 🧮 Distribuzione binomiale

$$
\Pr(X = k) = \binom{n}{k} p^k (1 - p)^{n - k}
$$

📘 Dove:
- $n$ = numero di prove  
- $k$ = numero di successi  
- $p$ = probabilità di successo per prova  

$$
\binom{n}{k} = \frac{n!}{k! \, (n - k)!}
$$

rappresenta il numero di modi per scegliere **quali** prove risultano vincenti.

---

### 🔍 Come leggere la formula

- Il termine $p^k (1 - p)^{n - k}$ è la probabilità di **una singola sequenza** con $k$ successi e $n - k$ fallimenti.  
- Il coefficiente $\binom{n}{k}$ conta **tutte le sequenze** possibili che producono $k$ successi.  
- Moltiplicando otteniamo la probabilità complessiva di ottenere **esattamente k successi**.

---

### 💡 Esempio concreto

Lancio una moneta equa ($p = 0.5$) tre volte.  
Voglio la probabilità di ottenere 2 teste:

$$
\Pr(X = 2) = \binom{3}{2} (0.5)^2 (0.5)^1 = 3 \times 0.25 \times 0.5 = 0.375
$$

👉 Probabilità = **37,5%**

---

### 🎯 Esempio generale

Immagina un test con 10 domande a scelta multipla,  
e ogni risposta ha probabilità $p = 0.25$ di essere giusta “a caso”.

La probabilità di azzeccarne esattamente 4 è:

$$
\Pr(X = 4) = \binom{10}{4} (0.25)^4 (0.75)^6 \approx 0.146
$$

👉 Circa **14,6%**.

---

## ⚙️ Aspettativa e varianza della binomiale

Usiamo la **linearità dell’aspettativa**:

$$
E[X] = E[X_1 + X_2 + \dots + X_n] = E[X_1] + \dots + E[X_n]
$$

Poiché ogni $E[X_i] = p$, abbiamo:

$$
E[X] = n p
$$

👉 In media, ci aspettiamo **$n p$ successi** su $n$ prove.

---

### Varianza

Poiché le prove sono indipendenti:

$$
\mathrm{Var}(X) = \mathrm{Var}(X_1 + X_2 + \dots + X_n) = \mathrm{Var}(X_1) + \dots + \mathrm{Var}(X_n)
$$

e dato che $\mathrm{Var}(X_i) = p(1 - p)$:

$$
\mathrm{Var}(X) = n p (1 - p)
$$

La **deviazione standard** è:

$$
\sigma = \sqrt{n p (1 - p)}
$$

---

### 💬 Interpretazione intuitiva

Se lanci una moneta 100 volte ($n = 100$, $p = 0.5$):

$$
E[X] = 100 \times 0.5 = 50
$$
$$
\sigma = \sqrt{100 \times 0.5 \times 0.5} = 5
$$

👉 In media ottieni 50 teste, con oscillazioni tipiche di ±5.  
Risultati tra 45 e 55 sono i più probabili; 20 o 80 sono estremamente rari.

---

### 🧠 Osservazione importante

Il valore atteso $E[X]$ **non indica la probabilità** che accada qualcosa,  
ma la **media numerica** dei valori che $X$ assume.

$$
\Pr(X = E[X]) \text{ può essere basso, ma } E[X] \text{ rappresenta il “centro” della distribuzione.}
$$

---

## 🔹 2.3 – Aspettativa condizionata (introduzione)

Spesso vogliamo capire l’**aspettativa sapendo che è accaduto un certo evento**.

La **media condizionata** di $X$ dato un evento $A$ si scrive:

$$
E[X \mid A] = \sum_x x \cdot \Pr(X = x \mid A)
$$

Essa rappresenta la **media dei valori di X considerando solo i casi in cui A è vero.**

---

### 💡 Esempio

Sia $X$ il numero di teste in due lanci di moneta.  
Abbiamo $E[X] = 1$.

Se sappiamo che è uscita almeno una testa (evento $A$), i casi possibili sono:

$$
\{ TH, HT, HH \}
$$

Allora:

$$
E[X \mid A] = \frac{1 + 1 + 2}{3} = \frac{4}{3}
$$

👉 Sapendo che è uscita almeno una testa, ci aspettiamo **1,33 teste in media.**

---

## 🔹 Legge delle aspettative totali

Una proprietà fondamentale:

$$
E[X] = E[E[X \mid A]]
$$

Cioè:  
> la media complessiva è la media delle **medie condizionate**,  
> pesate con le probabilità degli eventi corrispondenti.

---

### 💡 Esempio pratico

Supponiamo che un algoritmo funzioni su due tipi di input:

| Tipo | Probabilità | Tempo medio |
|:-----|:-------------|:-------------|
| Facile | 0.8 | 5s |
| Difficile | 0.2 | 20s |

Allora:

$$
E[\text{tempo}] = 0.8 \times 5 + 0.2 \times 20 = 8 \text{ secondi}
$$

👉 L’aspettativa globale è la **media ponderata** delle aspettative condizionate.
## 🎯 Introduzione

Finora abbiamo visto **variabili casuali binomiali**, che contano **quanti successi** avvengono in un numero fisso di prove.  
Ora cambiamo prospettiva: vogliamo sapere **quante prove servono prima di ottenere il primo successo**.

👉 Questo è il punto di partenza per la **distribuzione geometrica**.

---

## 🔹 2.4 – La distribuzione geometrica

### 🔸 Definizione

La variabile geometrica $X$ rappresenta il **numero di prove necessarie fino al primo successo** in una sequenza di esperimenti indipendenti,  
ognuno con probabilità di successo $p$.

$$
\Pr(X = k) = (1 - p)^{k - 1} p, \quad k = 1, 2, 3, \dots
$$

📘 **Significato:**

- Le prime $(k - 1)$ prove **falliscono** (ognuna con probabilità $(1 - p)$)  
- La $k$-esima prova è un **successo** (con probabilità $p$)

---

### 💡 Esempio intuitivo

Lancio una moneta e voglio sapere **quanti lanci servono prima di ottenere testa**, con $p = 0.5$:

$$
\Pr(X = 1) = 0.5 \quad \text{→ testa al primo lancio}
$$

$$
\Pr(X = 2) = 0.5^2 = 0.25 \quad \text{→ croce, poi testa}
$$

$$
\Pr(X = 3) = 0.5^3 = 0.125 \quad \text{→ due croci, poi testa}
$$

...e così via.

---

## ⚙️ Aspettativa della distribuzione geometrica

Il numero medio di prove necessarie per il primo successo è:

$$
E[X] = \frac{1}{p}
$$

👉 Se la probabilità di successo è bassa, servono **più prove in media**.

| $p$ | $E[X]$ | Significato |
|:---:|:-------:|:------------|
| 0.5 | 2 | in media, due lanci per una testa |
| 0.1 | 10 | in media, dieci tentativi per un successo |
| 0.01 | 100 | eventi molto rari → attese lunghe |

---

## ⚖️ Varianza della geometrica

$$
\mathrm{Var}(X) = \frac{1 - p}{p^2}
$$

👉 La variabilità cresce molto quando il successo è raro ($p$ piccolo).

---

## 🧭 Interpretazione intuitiva

La **distribuzione geometrica** modella il tempo di attesa fino al primo evento “positivo”.  
È il modello naturale per situazioni del tipo:

- primo successo in una sequenza di esperimenti,  
- primo pacchetto corretto in una rete rumorosa,  
- prima collisione evitata in un sistema casuale.

📈 È la base per descrivere **tempi di attesa** e **conteggi di tentativi** nei processi casuali.

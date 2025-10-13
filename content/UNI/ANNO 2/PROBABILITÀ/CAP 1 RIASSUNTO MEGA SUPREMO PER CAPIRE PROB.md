## 🧩 1. Introduzione: perché usare la probabilità negli algoritmi

Il capitolo inizia con un’idea importante:
👉 **La probabilità serve per controllare l’incertezza e l’efficienza.**

Gli autori mostrano che in informatica possiamo usare la casualità non solo per modellare fenomeni incerti (come errori o dati rumorosi), ma anche per **progettare algoritmi più semplici e veloci**.  
Questi sono detti **algoritmi randomizzati**.

---

### 🔹 **Primo esempio: verificare un’identità polinomiale**

Supponiamo di voler verificare se due polinomi sono uguali:

$$
F(x) = G(x)
$$

In teoria, potresti espandere tutto e confrontare i coefficienti — ma questo è lento.  
Invece, si può fare così:

1. Scegli un numero casuale $r$ (per esempio tra $1$ e $100d$, dove $d$ è il grado massimo dei polinomi).  
2. Calcola $F(r)$ e $G(r)$.  
3. Se i risultati sono diversi → i polinomi **non sono uguali**.  
4. Se sono uguali → **probabilmente** lo sono davvero.

---

### 🤔 **Perché “probabilmente”?**

È possibile (anche se raro) che due polinomi diversi assumano lo stesso valore per un certo $r$.  
Ma questo può accadere **al massimo in $d$ punti diversi**, dove $d$ è il grado del polinomio.  

Quindi la probabilità di errore è al più:

$$
\frac{d}{100d} = \frac{1}{100}
$$

👉 Con una sola prova hai solo **l’1% di errore**.  
Ripetendo la prova più volte con numeri casuali diversi, la **probabilità di errore decresce esponenzialmente**.

📘 È un esempio classico di **algoritmo randomizzato con errore controllato**:
non garantisce sempre la correttezza, ma è **molto veloce** e **quasi sempre giusto**.

---

## 🎲 1.2 – Axiomi di probabilità

Dopo l’esempio pratico, gli autori formalizzano i concetti matematici su cui si basa la probabilità.

---

### 🔸 **Lo spazio di probabilità**

Un esperimento casuale (come “scegli un numero tra $1$ e $100d$”) è descritto da:

- **Spazio campionario** $\Omega$:  
  insieme di tutti i possibili risultati.  
  → Nell’esempio: $\Omega = \{1, 2, \dots, 100d\}$.

- **Eventi:** sottoinsiemi di $\Omega$.  
  → Esempio: “il numero scelto è pari”.

- **Funzione di probabilità** $\Pr$:  
  assegna a ogni evento un numero tra $0$ e $1$, con tre proprietà fondamentali (gli **assiomi di Kolmogorov**):

  1. $0 \leq \Pr(E) \leq 1$
  2. $\Pr(\Omega) = 1$
  3. Se due eventi non si sovrappongono,  
     $$
     \Pr(E_1 \cup E_2) = \Pr(E_1) + \Pr(E_2)
     $$

Per eventi qualsiasi (anche sovrapposti) vale:

$$
\Pr(E_1 \cup E_2) = \Pr(E_1) + \Pr(E_2) - \Pr(E_1 \cap E_2)
$$

Questo è utile per **combinare più probabilità**.

---

### ⚖️ **La “Union Bound”**

Una regola semplice ma potentissima:

$$
\Pr(E_1 \cup E_2 \cup \dots \cup E_n) \leq \Pr(E_1) + \Pr(E_2) + \dots + \Pr(E_n)
$$

In parole povere:
> La probabilità che accada almeno uno degli eventi è al massimo la **somma delle loro probabilità**.

È uno strumento fondamentale per ottenere **stime superiori (upper bounds)** in probabilità e analisi di algoritmi.

---

## 🧮 **Ritorno all’algoritmo dei polinomi**

Applichiamo ora le definizioni all’esempio iniziale:

- Lo spazio campionario è $\{1, 2, \dots, 100d\}$.  
- Ogni numero ha probabilità $\frac{1}{100d}$.

L’evento “l’algoritmo sbaglia” è che $r$ sia una radice del polinomio $F(x) - G(x)$.  
Poiché ci sono al massimo $d$ radici:

$$
\Pr(\text{errore}) \leq \frac{d}{100d} = \frac{1}{100}
$$

Se si ripete l’esperimento $k$ volte (scegliendo $r$ indipendenti):

$$
\Pr(\text{errore in tutte le prove}) \leq \left(\frac{1}{100}\right)^k
$$

👉 Quindi l’errore scende **esponenzialmente** con il numero di ripetizioni.

---

## 🧠 **Indipendenza e probabilità condizionata**

Per comprendere meglio i calcoli precedenti, servono due concetti base.

### 🔹 **Eventi indipendenti**

Due eventi $E$ e $F$ sono **indipendenti** se:

$$
\Pr(E \cap F) = \Pr(E) \Pr(F)
$$

cioè: sapere che uno accade **non cambia** la probabilità dell’altro.

---

### 🔹 **Probabilità condizionata**

Definita come:

$$
\Pr(E \mid F) = \frac{\Pr(E \cap F)}{\Pr(F)}
$$

cioè: la probabilità che accada $E$ **sapendo che** $F$ è accaduto.

---

### 🔁 **Applicazione all’algoritmo randomizzato**

- **Con sostituzione:** ogni scelta è indipendente ⇒ si può **moltiplicare le probabilità**.  
- **Senza sostituzione:** le prove sono collegate ⇒ si usa la **probabilità condizionata**.

---
## 🧩 1.3 – Verifying Matrix Multiplication  
**Verificare una moltiplicazione di matrici in modo probabilistico**

Questa sezione mostra un’idea potente: usare la **probabilità** per rendere **efficienti verifiche molto costose**.

---

### 🔹 **Il problema**

Abbiamo tre matrici quadrate $A$, $B$ e $C$, ciascuna di dimensione $n \times n$.  
Vogliamo verificare se:

$$
A \times B = C
$$

Il metodo diretto — calcolare $A \times B$ e confrontarlo con $C$ — richiede **$O(n^3)$** operazioni,  
cioè milioni di moltiplicazioni per matrici grandi.  
Troppo lento, soprattutto se vogliamo solo **controllare** che il risultato sia corretto.

---

### 🔹 **L’idea randomizzata**

Invece di rifare tutta la moltiplicazione, scegli un **vettore casuale** $r$ di dimensione $n \times 1$  
(ad esempio con valori 0 o 1 scelti a caso).

Poi calcola:

$$
A(Br) \quad \text{e} \quad Cr
$$

e confrontali:

- Se $A(Br) = Cr$, **probabilmente** $A \times B = C$.
- Se $A(Br) \neq Cr$, **sicuramente** $A \times B \neq C$.

---

### 🔹 **Cosa significano $A(Br)$ e $Cr$**

$Br$ significa “moltiplica la matrice $B$ per il vettore casuale $r$”:  
ottieni un nuovo vettore, combinazione delle colonne di $B$.

Poi moltiplichi $A$ per quel risultato: $A(Br)$.  
Questo equivale ad applicare prima $B$, poi $A$ al vettore $r$.

$Cr$ è invece la moltiplicazione della matrice $C$ per lo stesso vettore $r$.

➡️ In sintesi, il test confronta due vettori:
- il risultato di applicare $A$ e $B$ in cascata,
- con quello di applicare direttamente $C$.

---

### 🔹 **Perché funziona**

Se $A \times B = C$, allora per ogni vettore $r$ vale:

$$
A(Br) = (AB)r = Cr
$$

Quindi il test sarà sempre vero.

Se invece $A \times B \neq C$, definiamo:

$$
D = A \times B - C
$$

Poiché $D \neq 0$, vogliamo verificare se:

$$
Dr = 0
$$

cioè se la combinazione delle colonne di $D$ data da $r$ restituisce il vettore nullo.

Se $D \neq 0$, quasi sempre ci sarà almeno un vettore $r$ per cui $Dr \neq 0$.  
Solo in casi rari (con probabilità $\le \frac{1}{2}$) potremmo scegliere casualmente un vettore che “nasconde” l’errore.

Ripetendo il test più volte con vettori diversi, la probabilità di errore scende **esponenzialmente**:

$$
\Pr(\text{errore dopo $k$ prove}) \le \left(\frac{1}{2}\right)^k
$$

---

### 🔹 **Vantaggi**

| Metodo | Complessità | Accuratezza |
|--------|--------------|-------------|
| Classico | $O(n^3)$ | Esatta |
| Probabilistico | $O(n^2)$ | Quasi certa (errore ≤ $(1/2)^k$) |

👉 È un esempio di **algoritmo Monte Carlo**:  
usa la casualità per ottenere risultati più rapidi, accettando un piccolissimo margine d’incertezza.

---

## 🎲 1.4 – Conditional Probability and Independence  
**Probabilità condizionata e indipendenza**

Gli autori introducono ora formalmente i concetti di **probabilità condizionata** e **indipendenza**, già usati negli esempi precedenti.

---

### 🔹 **Probabilità condizionata**

$$
\Pr(E \mid F) = \frac{\Pr(E \cap F)}{\Pr(F)}
$$

Si legge:  
> “La probabilità che accada $E$, **dato che** è accaduto $F$.”

---

#### 📘 Esempio

In un mazzo di 52 carte:

- $E$: “è un re” → 4 carte  
- $F$: “è una figura” (re, donna o fante) → 12 carte  

Poiché $E \cap F = E$:

$$
\Pr(E \mid F) = \frac{\Pr(E)}{\Pr(F)} = \frac{4/52}{12/52} = \frac{1}{3}
$$

Quindi, sapendo che è uscita una figura, la probabilità che sia un re è **1/3**.

---

### 🔹 **Regola del prodotto**

Dalla definizione di probabilità condizionata:

$$
\Pr(E \cap F) = \Pr(F) \times \Pr(E \mid F)
$$

oppure anche:

$$
\Pr(E \cap F) = \Pr(E) \times \Pr(F \mid E)
$$

Questa è la base per molti calcoli, incluso il **Teorema di Bayes**.

---

### 🔹 **Indipendenza**

Due eventi $E$ e $F$ sono **indipendenti** se:

$$
\Pr(E \cap F) = \Pr(E) \Pr(F)
$$

cioè sapere che uno accade **non cambia** la probabilità dell’altro.

E quindi anche:

$$
\Pr(E \mid F) = \Pr(E)
$$

---

#### 🎲 Esempio

Lancio due monete:

- $E$: “la prima moneta è testa”  
- $F$: “la seconda moneta è testa”

→ Sono **indipendenti**, perché l’esito della prima non influisce sulla seconda.

---

## 🧠 1.5 – Naive Bayesian Classifier  
**Un’applicazione della probabilità condizionata alla classificazione**

Questa sezione fa da ponte tra **probabilità** e **intelligenza artificiale**, mostrando come usare il **Teorema di Bayes** per classificare oggetti o dati in categorie.

---

### 🔹 **Il modello probabilistico**

Vogliamo stimare:

$$
\Pr(C \mid x) = \frac{\Pr(C) \times \Pr(x \mid C)}{\Pr(x)}
$$

dove:

- $C$ = categoria (es. “spam” o “non spam”)  
- $x$ = insieme delle caratteristiche osservate (es. parole di un’email)

👉 L’obiettivo è scegliere la categoria $C$ che **massimizza** $\Pr(C \mid x)$.

---

### 🔹 **Cosa significa categoria**

Una categoria è una **classe o etichetta** che identifica il tipo di oggetto:

| Oggetto | Categorie possibili |
|----------|---------------------|
| Email | Spam / Non spam |
| Immagine | Gatto / Cane |
| Recensione | Positiva / Negativa |

Il sistema osserva un insieme di caratteristiche $x$ (es. le parole di un testo)  
e cerca la categoria più probabile.

---

### 🔹 **Cosa significa $\Pr(x \mid C)$**

> “La probabilità di osservare le caratteristiche $x$, sapendo che l’oggetto appartiene alla categoria $C$.”

Esempio:

- $\Pr(x \mid \text{spam})$ = probabilità che un’email di spam contenga “lotteria” e “premio”  
- $\Pr(x \mid \text{non spam})$ = probabilità che un’email normale contenga le stesse parole

---

### 🔹 **L’assunzione “naive”**

Nella realtà le caratteristiche non sono indipendenti (“lotteria” e “premio” compaiono spesso insieme).  
Ma per semplificare i calcoli si assume che, dato $C$, **siano indipendenti**.

$$
\Pr(x \mid C) = \Pr(x_1, x_2, \dots, x_n \mid C) = \prod_i \Pr(x_i \mid C)
$$

Il simbolo $\prod_i$ indica il prodotto di tutte le probabilità individuali $\Pr(x_i \mid C)$.

Esempio:

$$
\Pr(x \mid \text{spam}) = 0.8 \times 0.7 \times 0.4 = 0.224
$$

---

### 🔹 **Il simbolo “∝” (proporzionale a)**

Il teorema di Bayes completo è:

$$
\Pr(C \mid x) = \frac{\Pr(C) \Pr(x \mid C)}{\Pr(x)}
$$

Poiché $\Pr(x)$ è uguale per tutte le categorie (è lo stesso messaggio), possiamo ignorarlo e scrivere:

$$
\Pr(C \mid x) \propto \Pr(C) \times \Pr(x \mid C)
$$

Il simbolo “∝” significa “proporzionale a”,  
cioè differisce solo per un **fattore costante** $\frac{1}{\Pr(x)}$.

---

### 🔹 **Esempio numerico completo**

| Parola | $\Pr(\text{parola} \mid \text{spam})$ | $\Pr(\text{parola} \mid \text{non spam})$ |
|:-------|:-------------------------------------:|:------------------------------------------:|
| “lotteria” | 0.8 | 0.1 |
| “premio” | 0.7 | 0.05 |

E sappiamo che:

$$
\Pr(\text{spam}) = 0.4, \quad \Pr(\text{non spam}) = 0.6
$$

Allora:

$$
\Pr(\text{spam} \mid x) \propto 0.4 \times (0.8 \times 0.7) = 0.224
$$

$$
\Pr(\text{non spam} \mid x) \propto 0.6 \times (0.1 \times 0.05) = 0.003
$$

Poiché $0.224 \gg 0.003$, il messaggio è classificato come **spam**.

---

### 🔹 **Intuizione finale**

- $\Pr(C)$ → quanto è comune quella categoria (“quanto spesso ricevo spam”).  
- $\Pr(x \mid C)$ → quanto il contenuto è tipico di quella categoria.  
- $\Pr(C \mid x)$ → quanto è probabile che il messaggio appartenga a quella categoria, **dato il contenuto**.

Poiché $\Pr(x)$ è costante, possiamo semplicemente scegliere la categoria con:

$$
\Pr(C) \Pr(x \mid C) \text{ massimo.}
$$

✅ In pratica, è così che funzionano i classificatori **Naive Bayes** negli algoritmi di machine learning.

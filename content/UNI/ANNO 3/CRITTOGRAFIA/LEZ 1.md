2.1.1 
2.1.2 
2.2.1
2.2.2

## 🔹 **Obiettivo della crittografia**

Lo scopo principale della **crittografia** è permettere a due persone (tradizionalmente **Alice** e **Bob**) di **comunicare in modo sicuro** su un canale insicuro (come Internet o una linea telefonica).

- Alice vuole inviare un messaggio (**plaintext**) a Bob.  
- Usa una **chiave segreta** e un algoritmo di **cifratura** per trasformarlo in **ciphertext** (testo cifrato).  
- Bob riceve il ciphertext e, usando la **stessa chiave** (o una chiave corrispondente), lo **decifra** per recuperare il messaggio originale.  
- Un avversario (**Oscar**), anche se intercetta il ciphertext, **non è in grado di capire il contenuto**.

---

## 🔹 **Definizione formale di un crittosistema**

Un **crittosistema** è definito matematicamente come una **cinquina**:

$$
(P, C, K, E, D)
$$

dove:

1. **P** è l’insieme dei **plaintexts** (tutti i possibili messaggi originali);
2. **C** è l’insieme dei **ciphertexts** (tutti i possibili messaggi cifrati);
3. **K** è lo **spazio delle chiavi**, cioè l’insieme di tutte le chiavi possibili;
4. Per ogni chiave $K \in K$:
   - esiste una **funzione di cifratura** $e_K : P \to C$
   - ed una **funzione di decifratura** $d_K : C \to P$  
     tali che:

$$
d_K(e_K(x)) = x \quad \text{per ogni } x \in P
$$

(cioè, se cifri e poi decifri, ottieni di nuovo il messaggio originale).

➡️ In altre parole, **la cifratura e la decifratura sono funzioni inverse** l’una dell’altra per una data chiave.

---

## 🔹 **Il processo di comunicazione**

1. Alice e Bob **concordano una chiave $K$** in modo sicuro (di persona o tramite un canale protetto).  
2. Alice vuole inviare un messaggio $x = x_1x_2 \dots x_n$, composto da $n$ simboli.  
3. Ogni simbolo $x_i$ viene cifrato con la funzione $e_K$:
   $$
   y_i = e_K(x_i)
   $$
   ottenendo il **ciphertext** $y = y_1y_2 \dots y_n$.  
4. Alice invia $y$ a Bob tramite il canale insicuro.  
5. Bob applica la funzione di decifratura $d_K$ su ogni simbolo:
   $$
   x_i = d_K(y_i)
   $$
   e ricostruisce così il messaggio originale $x$.

Oscar, anche se intercetta $y$, non può risalire a $x$ senza conoscere la chiave $K$.

---
### 📊 **Figura 2.1 – Il canale di comunicazione**

L’immagine descrive graficamente questo processo:
![[Pasted image 20251007185235.png]]


---
## 🔹 **Proprietà fondamentali**

1. **Cifratura iniettiva (one-to-one):**  
   Ogni plaintext deve corrispondere a **uno e un solo ciphertext**.  
   Se due plaintext diversi dessero lo stesso ciphertext:

   $$
   e_K(x_1) = e_K(x_2), \quad x_1 \neq x_2
   $$

   allora Bob non potrebbe sapere quale messaggio decifrare → il sistema non funzionerebbe.

2. **Se $P = C$** (cioè se l’insieme dei plaintext e quello dei ciphertext coincidono):  
   ogni funzione di cifratura $e_K$ è una **permutazione** degli elementi dell’insieme.  
   → In questo caso, cifrare significa semplicemente **riordinare** (permutare) gli elementi del messaggio in modo controllato dalla chiave.

---

## 🔹 **Esempio intuitivo: il Cifrario di Cesare**

Un esempio pratico di questo modello è il **Shift Cipher (Cifrario di Cesare)**:

- $P = C = \{ A, B, C, \dots, Z \}$
- $K = \{ 0, 1, 2, \dots, 25 \}$
- $e_K(x) = (x + K) \bmod 26$
- $d_K(y) = (y - K) \bmod 26$

Qui:

- Cifratura e decifratura sono **inversi**.  
- Ogni $e_K$ è una **permutazione dell’alfabeto**.  
- Oscar può vedere il ciphertext, ma senza la chiave $K$ non può sapere di quanto è stato “spostato” ogni simbolo.
## 🔹 2.1.1 – Il Cifrario a Scorrimento (Shift Cipher)

Il **Shift Cipher** è uno dei più semplici esempi di crittosistema.  
Funziona applicando **uno spostamento numerico costante** a ogni lettera del messaggio, utilizzando le regole dell’**aritmetica modulare**.

---

### ⚙️ **Ripasso di aritmetica modulare**

Prima di descrivere il cifrario, il testo ricorda alcuni concetti fondamentali.

#### **Definizione di congruenza modulo m**

Per interi $a, b$ e un intero positivo $m$, diciamo che:

$$
a \equiv b \pmod{m}
$$

se e solo se $m$ divide $(b - a)$.  
In altre parole, **$a$ e $b$ lasciano lo stesso resto** quando divisi per $m$.

Esempio:

$$
101 \bmod 7 = 3, \quad (-101) \bmod 7 = 4
$$

(perché $-101 = 7 \times (-15) + 4$)

> 🔸 Nota: in matematica il resto $a \bmod m$ è sempre **non negativo**, compreso tra $0$ e $m - 1$.  
> In molti linguaggi di programmazione, invece, può avere il segno di $a$.

---

### 🧮 **L’insieme $\mathbb{Z}_m$**

Si definisce:

$$
\mathbb{Z}_m = \{ 0, 1, 2, \dots, m-1 \}
$$

con due operazioni:

- **Addizione modulo m:** $(a + b) \bmod m$
- **Moltiplicazione modulo m:** $(a \times b) \bmod m$

Esempio:

$$
11 \times 13 = 143, \quad 143 \bmod 16 = 15 \Rightarrow 11 \times 13 \equiv 15 \pmod{16}
$$

---

### 🧩 **Proprietà di $\mathbb{Z}_m$**

- È **chiuso** per addizione e moltiplicazione.  
- Le operazioni sono **commutative** e **associative**.  
- Esiste l’elemento neutro:
  - per l’addizione: $0$
  - per la moltiplicazione: $1$
- Ogni elemento ha un **inverso additivo**:  
  $$
  a + (m - a) \equiv 0 \pmod{m}
  $$
- Le operazioni soddisfano la **distributività**.

In termini algebrici:

- $(\mathbb{Z}_m, +)$ è un **gruppo abeliano**
- $(\mathbb{Z}_m, +, \times)$ è un **anello finito** (finite ring)

Esempio:  
In $\mathbb{Z}_{31}$,

$$
11 - 18 = -7 \Rightarrow (-7) \bmod 31 = 24
$$

---

## 🔐 **Definizione del Shift Cipher**

Il **Cifrario a Scorrimento** è definito come segue:

$$
P = C = K = \mathbb{Z}_{26}
$$

perché ci sono 26 lettere nell’alfabeto inglese.

Le funzioni di cifratura e decifratura sono:

$$
e_K(x) = (x + K) \bmod 26
$$

$$
d_K(y) = (y - K) \bmod 26
$$

dove:

- $x$ è il plaintext (una lettera convertita in numero)  
- $y$ è il ciphertext (la lettera cifrata)  
- $K$ è la chiave (lo “spostamento”)

È facile verificare che:

$$
d_K(e_K(x)) = (x + K - K) \bmod 26 = x
$$

→ quindi il sistema soddisfa la definizione formale di **crittosistema**.

---

### 🏛️ **Il Cifrario di Cesare**

Per la chiave $K = 3$, il sistema prende il nome di **Cifrario di Cesare**, perché secondo la tradizione fu usato da Giulio Cesare per le comunicazioni militari.

---

### 🔠 **Corrispondenza lettere–numeri**

![[Pasted image 20251007185620.png]]

---

## ✉️ **Esempio 2.1**
![[Pasted image 20251007185822.png]]
## 🔍 **Sicurezza e crittoanalisi**

Perché un sistema sia pratico, deve avere:

1. **Cifratura e decifratura efficienti**  
2. **Difficoltà di determinare la chiave $K$** osservando solo il ciphertext  

Ma il **Shift Cipher non è sicuro**, perché:

- il **numero di chiavi possibili** è solo 26;  
- un avversario può provare tutte le chiavi (metodo *exhaustive key search*).

---

### 🧩 **Esempio 2.2 – Attacco per forza bruta**

**Ciphertext:**

`JBCRCLQRWCRVNBJENBWRWN`

Si prova ogni chiave $K = 0, 1, 2, \dots, 25$.  
Dopo alcuni tentativi, si ottiene:

`astitchintimesavesnine`

Quindi il **plaintext** è *“a stitch in time saves nine”*  
e la chiave è $K = 9$.

In media, basta provare $\frac{26}{2} = 13$ chiavi per trovare quella giusta.

---

## ⚠️ **Conclusione sulla sicurezza**

Il Cifrario a Scorrimento mostra che:

- un crittosistema è **insicuro** se il suo **spazio delle chiavi è troppo piccolo**;  
- ma un **grande keyspace**, da solo, **non garantisce sicurezza** (servono anche buone proprietà matematiche).
## 🔹 2.1.2 – Il Cifrario a Sostituzione

Il **Substitution Cipher** è un sistema in cui ogni lettera dell’alfabeto viene sostituita da un’altra lettera, secondo una **permutazione casuale**.  
In altre parole, la chiave è una **riorganizzazione dell’alfabeto**.

Questo sistema è molto più flessibile del Cifrario di Cesare, perché non si limita a “spostare” tutte le lettere di una quantità fissa, ma consente qualunque corrispondenza.

---

### 🔐 **Definizione formale (Cryptosystem 2.2)**

$$
P = C = \mathbb{Z}_{26}
$$

(cioè le 26 lettere dell’alfabeto inglese rappresentate dai numeri da $0$ a $25$).

La chiave $K$ è costituita da **tutte le possibili permutazioni** dell’insieme:

$$
\{ 0, 1, 2, \dots, 25 \}
$$

Per ogni permutazione $\pi \in K$:

**Cifratura:**

$$
e_\pi(x) = \pi(x)
$$

**Decifratura:**

$$
d_\pi(y) = \pi^{-1}(y)
$$

dove $\pi^{-1}$ è la **permutazione inversa**, cioè quella che “annulla” la cifratura.

---

### 🧠 **Significato intuitivo**

Ogni lettera del plaintext viene **sostituita da una lettera diversa** secondo la chiave (cioè la permutazione).  
Per decifrare, si applica la **permutazione inversa**, che riporta ogni lettera al suo valore originale.

---

### 🔤 **Esempio di permutazione**

La tabella seguente mostra una possibile chiave casuale (cioè una permutazione dell’alfabeto):
![[Pasted image 20251007191055.png]]

Esempi:

$$
e_\pi(a) = X, \quad e_\pi(b) = N, \quad e_\pi(c) = Y, \quad e_\pi(z) = I
$$

---

### 🔁 **Permutazione inversa (decifratura)**

Per decifrare, bisogna **invertire la mappa**.  
La seconda tabella mostra la **permutazione inversa**:
![[Pasted image 20251007191113.png]]

Esempi:

$$
d_\pi(A) = d, \quad d_\pi(B) = l, \quad d_\pi(X) = a, \quad d_\pi(Z) = i
$$

---

### 🔓 **Esercizio di decrittazione (dal testo)**

**Ciphertext:**

`MGZVYZLGHCMHJMYXSSFMNHAHYCDLMHA`

Usando la **permutazione inversa** qui sopra, si può risalire al plaintext sostituendo ogni lettera cifrata con la corrispondente lettera in chiaro.

👉 (Posso mostrarti la decrittazione completa, se vuoi che la risolviamo passo per passo.)

---

### 📏 **Spazio delle chiavi**

La chiave del **Substitution Cipher** è una permutazione dell’alfabeto di 26 lettere.  
Quindi il numero di chiavi possibili è:

$$
26! = 26 \times 25 \times 24 \times \dots \times 1 \approx 4.03 \times 10^{26}
$$

Si tratta di un numero enorme, quindi una ricerca esaustiva (*brute-force*) è impraticabile, anche per un computer moderno.

---

### ⚠️ **Ma… non è sicuro**

Nonostante l’enorme spazio delle chiavi, il **Substitution Cipher** è **facile da rompere** con tecniche di **crittanalisi statistica**, perché:

- Ogni lettera del plaintext viene **sempre cifrata nello stesso modo**  
  (es. se “E” diventa “Q”, sarà sempre “Q”).  
- Quindi, la **frequenza delle lettere nel testo cifrato** rispecchia quella del linguaggio originale.  
  (es. in inglese la “E” è la lettera più comune → la lettera più frequente nel ciphertext sarà probabilmente la “E” cifrata.)

Le tecniche di **frequency analysis** furono sviluppate già nel Medioevo e bastano per decifrare messaggi cifrati con questo metodo.

## 🔹 2.2.1 – Cryptanalysis of the Affine Cipher

### 🧩 **Contesto**

Oscar (l’avversario) intercetta un messaggio cifrato con un **Affine Cipher**:

$$
e_K(x) = (a x + b) \bmod 26
$$

dove:

- $x$ è la lettera del **plaintext** (convertita in numero tra $0$ e $25$);
- $a, b$ sono i **parametri della chiave segreta**;
- $a$ deve essere **invertibile modulo 26**, cioè $\gcd(a, 26) = 1$.

La **decifratura** corrispondente è:

$$
d_K(y) = a^{-1} (y - b) \bmod 26
$$

---

### 📜 **Esempio 2.10 – Ciphertext intercettato**

FMXVEDKAPHFERBNDKRXRSREFMORUDSDKDVSHVUFEDKAPRKDLYEVLRHHRH

Totale: **57 lettere**


### 📊 **Analisi delle frequenze**

Il testo fornisce la frequenza di ciascuna lettera nel messaggio:

| Lettera | Freq | Lettera | Freq | Lettera | Freq | Lettera | Freq |
|----------|------|----------|------|----------|------|----------|------|
| A | 2 | B | 1 | C | 0 | D | 7 |
| E | 5 | F | 4 | G | 0 | H | 5 |
| I | 0 | J | 0 | K | 5 | L | 2 |
| M | 2 | N | 1 | O | 1 | P | 2 |
| Q | 0 | R | 8 | S | 3 | T | 0 |
| U | 2 | V | 4 | W | 0 | X | 2 |
| Y | 1 | Z | 0 |  |  |  |  |

Le lettere più frequenti nel ciphertext sono:

- **R (8)**
- **D (7)**
- **E, H, K (5)**
- **F, S, V (4)**

---

### 🎯 **Ipotesi iniziale basata sulle frequenze**

Oscar sa che, in inglese, le lettere più comuni sono:

- **e** (più frequente)
- **t** (seconda più frequente)

Quindi ipotizza:

$$
R \rightarrow e, \quad D \rightarrow t
$$

---

### 🧮 **Costruzione del sistema di equazioni**

In forma numerica:

$$
e = 4, \quad t = 19, \quad R = 17, \quad D = 3
$$

Dalla definizione del cifrario affine:

$$
e_K(x) = a x + b \pmod{26}
$$

otteniamo due equazioni:

$$
4a + b \equiv 17 \pmod{26}
$$
$$
19a + b \equiv 3 \pmod{26}
$$

✏️ **Risoluzione**

Sottraiamo le due equazioni:

$$
(19a - 4a) \equiv (3 - 17) \Rightarrow 15a \equiv -14 \Rightarrow 15a \equiv 12 \pmod{26}
$$

Risolvendo in $\mathbb{Z}_{26}$, otteniamo $a = 6, \ b = 19$.

Ma:

$$
\gcd(6, 26) = 2 \neq 1
$$
- gcd è MCD

→ quindi $a = 6$ **non è invertibile** modulo 26 → **chiave illegale.**  
L’ipotesi è sbagliata.

---

### 🔁 **Secondi tentativi**

Oscar prova nuove ipotesi:

| Ipotesi              | Risultato                                      |
| -------------------- | ---------------------------------------------- |
| $R \to e$, $E \to t$ | $a = 13$ ❌ (illegale, $\gcd(13, 26) = 13$)     |
| $R \to e$, $H \to t$ | $a = 8$ ❌ (illegale)                           |
| $R \to e$, $K \to t$ | $a = 3$, $b = 5$ ✅ (legale, $\gcd(3, 26) = 1$) |

---

### 🔓 **Determinazione della chiave**

Abbiamo quindi:

$$
a = 3, \quad b = 5
$$

→ Chiave $K = (3, 5)$

---

### 🔁 **Funzione di decifratura**

Serve ora l’inverso moltiplicativo di $a = 3$ modulo 26.  
Poiché:

$$
3 \times 9 = 27 \equiv 1 \pmod{26}
$$

l’inverso è:

$$
a^{-1} = 9
$$

La funzione di decifratura diventa:

$$
d_K(y) = 9 (y - 5) \bmod 26
$$

che si può riscrivere come:

$$
d_K(y) = 9y - 45 \equiv 9y - 19 \pmod{26}
$$

---

### 🧩 **Risultato finale (plaintext)**

Applicando:

$$
d_K(y) = 9y - 19 \bmod 26
$$

al ciphertext, si ottiene:

`algorithmsarequitegeneraldefinitionsofarithmeticprocesses`

➡️ **Plaintext:**  
“**Algorithms are quite general definitions of arithmetic processes.**”

✅ Il testo è coerente e leggibile in inglese → la chiave trovata è corretta.

---

### 🔍 **Cosa abbiamo imparato**

Questo esempio mostra che:

- Anche senza conoscere la chiave, un avversario può **dedurla analizzando le frequenze** delle lettere.  
- Anche cifrari apparentemente complessi come l’**Affine Cipher** possono essere **rotti facilmente** se il testo è abbastanza lungo e se si conoscono le **statistiche del linguaggio**.

## 🔹 2.2.2 – Cryptanalysis of the Substitution Cipher

### 🧩 **Contesto**

Abbiamo un messaggio cifrato con un **Substitution Cipher**, cioè ogni lettera del plaintext è stata sostituita da una diversa lettera dell’alfabeto secondo una **permutazione sconosciuta** (la chiave).  
Lo scopo è determinare la chiave (cioè la mappatura lettere → lettere) e ricostruire il testo originale.

---

### 📜 **Ciphertext intercettato (Esempio 2.11)**

YIFQFMZRWQFYVECFMDZPCVMRZWNMDZVEJBTXCDDUMJ
NDIFEFMDZCDMQZKCEYFCJMYRNCWJCSZREXCHZUNMXZ
NZUCDRJXYYSMRTMEYIFZWDYVZVYFZUMRZCRWNZDZJJ
XZWGCHSMRNMDHNCMFQCHZJMXJZWIEJYUCFWDJNZDIR

yaml
Copy code

---

### 📊 **Analisi delle frequenze**

| Lettera | Frequenza | Osservazione |
|----------|------------|--------------|
| Z | molto frequente | più comune |
| C, D, F, J, M, R, Y | frequenti | |
| altre | meno frequenti | |

Quindi, come prima ipotesi:

$$
d_K(Z) = e
$$

poiché “e” è la lettera più comune in inglese.

---

### 🧩 **Analisi dei digrammi (coppie di lettere)**

Per confermare o smentire l’ipotesi, si studiano i **digrammi** che contengono la lettera Z.  
Se $Z \to e$, allora coppie come DZ, ZW, NZ, ZU potrebbero corrispondere a digrammi comuni in inglese (“re”, “ed”, “he”, “er”, ecc.).

- **DZ** e **ZW** compaiono 4 volte ciascuno  
- **NZ** e **ZU** compaiono 3 volte  
- altri (HZ, XZ, RZ, ecc.) solo 1–2 volte

---

### 🧠 **Prima ipotesi ragionata**

Poiché **ZW** è frequente ma **WZ** no → probabilmente $W \to d$  
(il digramma “ZW” corrisponde a “ed”, comune in inglese).

Poiché **DZ** compare spesso → $D \to r$, $s$ o $t$ (ma non ancora certo).

---

### 🔍 **Nuove deduzioni osservando il testo**

Nel ciphertext compaiono sequenze come:

ZRW

yaml
Copy code

Poiché $Z \to e$ e $W \to d$, abbiamo “ed”.  
C’è una R prima: “RZ” → “ne” è un digramma molto comune.  
Quindi $R \to n$.

---

### 💬 **Situazione parziale**

| Cipher | Plain |
|--------|-------|
| Z | e |
| W | d |
| R | n |

Applicando queste sostituzioni, nel testo compaiono frammenti come:

------end---------e----ned---e------------

yaml
Copy code

→ già si intravede la parola **“end”**, segno che le ipotesi sono buone.

---

### 🧠 **Nuove osservazioni**

Il digramma “NZ” (cioè “he”) è molto comune, mentre “ZN” no → $N \to h$.  
La sequenza “ne–ndhe” suggerisce che $C \to a$.

Aggiornamento:

| Cipher | Plain |
|--------|-------|
| Z | e |
| W | d |
| R | n |
| N | h |
| C | a |

Applicando queste sostituzioni:

---end---a---e-a--nedh--e---

yaml
Copy code

---

### 🧮 **Analisi successiva**

La lettera **M** è frequente → probabilmente rappresenta una **vocale**.  
Abbiamo già $a$ ed $e$, quindi $M$ può essere $i$ oppure $o$.

Poiché il digramma “CM” (cioè “ai”) è comune, si prova $M \to i$.

Aggiornamento:

| Cipher | Plain |
|--------|-------|
| Z | e |
| W | d |
| R | n |
| N | h |
| C | a |
| M | i |

Ora nel testo emergono parole parziali come:

...inedhi...

yaml
Copy code

→ potrebbe essere “finished” o “end hi...” — plausibile.

---

### 🔠 **Ipotesi sulla lettera Y**

Restano le vocali mancanti: $o, u$.  
Si nota che Y è frequente e, se $Y \to o$, si evitano sequenze di vocali innaturali come “aoi”.  
→ quindi $Y \to o$.

---

### 🔁 **D, F, J come possibili consonanti**

Le lettere più frequenti rimaste sono **D, F, J** → probabilmente corrispondono a $r, s, t$ (in qualche ordine).

Osservazioni:

- Il trigramma “NMD” → con $N = h$, $M = i$ → “hi\_$\_$” → suggerisce $D \to s$  
- Il gruppo “HNCMF” → con $N = h$, $C = a$, $M = i$ → “ha\_i\_$\_$”  
  Se fosse “chair”, allora $F \to r$ e $H \to c$  
  → Rimane $J \to t$ per esclusione.

---

### ✅ **Chiave parziale trovata**

| Cipher | Plain | | Cipher | Plain |
|:-------|:------|--|:-------|:------|
| Z | e | | D | s |
| W | d | | F | r |
| R | n | | H | c |
| N | h | | J | t |
| C | a | | M | i |
| Y | o | |   |   |

---

### 🧩 **Risultato del testo parziale**

Dopo tutte le sostituzioni, il messaggio diventa chiaramente leggibile:

> “Our friend from Paris examined his empty glass with surprise, as  
> if evaporation had taken place while he wasn’t looking.  
> I poured some more wine and he settled back in his chair,  
> face tilted up towards the sun.”

✅ **Plaintext finale:**

> “**Our friend from Paris examined his empty glass with surprise, as if evaporation had taken place while he wasn’t looking. I poured some more wine and he settled back in his chair, face tilted up towards the sun.**”

---

### 🧠 **Cosa abbiamo imparato**

Anche senza formule matematiche, il **Substitution Cipher** può essere rotto analizzando:

- le **frequenze delle lettere**  
- i **digrammi** (coppie)  
- i **trigrammi** (triplette)  
- il **contesto linguistico**

Si parte da ipotesi plausibili (es. “$Z \to e$”) e si confermano con la coerenza del testo.  
Man mano che si identificano parole, le altre lettere vengono dedotte per **esclusione**.

---

### 💡 **In sintesi**

| Concetto | Descrizione |
|-----------|-------------|
| **Cifrario** | Substitution Cipher (sostituzione monoalfabetica) |
| **Metodo di attacco** | Analisi statistica: frequenze, digrammi, contesto linguistico |
| **Chiave trovata** | Permutazione parziale (es. $Z \to e$, $W \to d$, $R \to n$, …) |
| **Risultato** | Plaintext completamente recuperato |
| **Conclusione** | Anche con un enorme spazio di chiavi ($26!$), il Substitution Cipher è debole perché mantiene la struttura linguistica del testo. |

---

🔓 **Conclusione:**  
Il **Substitution Cipher non è sicuro**, perché la **frequenza delle lettere nel ciphertext riflette quella del linguaggio naturale**.  
Un attaccante può, con abbastanza testo, **ricostruire la chiave a mano** usando logica e statistica

### ESERCIZIO 1.A

L'esercizio 1.A chiede di determinare se alcune relazioni asintotiche tra funzioni sono vere o meno. Per risolvere correttamente questo tipo di esercizio, è necessario conoscere i principali strumenti della notazione asintotica: **O (Big-O), Θ (Theta), o (small-o), Ω (Omega) e ω (small-omega)**.

---

## **1. Concetti Fondamentali**

Prima di procedere con gli esercizi, è importante ricordare cosa significano queste notazioni:

- **Big-O** $O(f(n))$: Stima superiore asintotica. Indica che una funzione non cresce più velocemente di un'altra, al più con una costante moltiplicativa.
    
- **Theta** $\Theta(f(n))$: Stima stretta. Indica che due funzioni crescono con lo stesso ordine di grandezza.
    
- **Small-o** $o(f(n))$: Stima superiore stretta. Indica che una funzione cresce in modo strettamente più lento rispetto a un'altra.
    
- **Big-Omega** $\Omega(f(n))$: Stima inferiore asintotica. Indica che una funzione cresce almeno velocemente quanto un'altra.
    
- **Small-omega** $\omega(f(n))$: Stima inferiore stretta. Indica che una funzione cresce strettamente più velocemente rispetto a un'altra.

---

## **2. Strategia di Risoluzione**

Per determinare la correttezza delle relazioni date, seguiamo questi passi:

1. **Identificare il termine dominante** nelle funzioni, ossia quello che cresce più velocemente asintoticamente.
2. **Utilizzare le proprietà della notazione asintotica** per confrontare le funzioni.
3. **Applicare approssimazioni matematiche** (per es., trascurare i termini meno significativi quando $n \to \infty$).
4. **Confrontare i risultati con la definizione di** $O, \Theta, o, \Omega, \omega$.

---

## **3. Esempio di Applicazione**

Vediamo come affrontare una delle relazioni tipiche degli esami.

### **Esempio 1**

**Verificare se:**

$$
n^{1/5} \log n + \sqrt{\log n} = o(n^{1/4})
$$

✅ **Passaggio 1: Individuare i termini dominanti**

- $n^{1/5} \log n$ cresce meno di $n^{1/4}$ perché $1/5 < 1/4$.
- $\sqrt{\log n}$ cresce molto più lentamente di $n^{1/4}$.

✅ **Passaggio 2: Stimare il rapporto tra le due funzioni**

$$
\frac{n^{1/5} \log n + \sqrt{\log n}}{n^{1/4}}
$$

Dividiamo tutto per $n^{1/4}$:

$$
n^{-1/20} \log n + n^{-1/4} \sqrt{\log n}
$$

Quando $n \to \infty$, entrambi i termini tendono a 0, quindi possiamo concludere che:

$$
n^{1/5} \log n + \sqrt{\log n} = o(n^{1/4})
$$

✅ **Risultato:** La relazione è **vera**.

---

### **Esempio 2**

**Verificare se:**

$$
2^n = \Theta(2^{n+ \log n})
$$

✅ **Passaggio 1: Semplificare il termine a destra**

$$
2^{n+ \log n} = 2^n \cdot 2^{\log n}
$$

Sappiamo che $2^{\log n} = n$, quindi possiamo riscrivere:

$$
2^{n+ \log n} = 2^n \cdot n
$$

✅ **Passaggio 2: Confrontare le funzioni**

$$
\frac{2^n}{2^n \cdot n} = \frac{1}{n}
$$

Quando $n \to \infty$, il rapporto tende a 0, il che significa che:

$$
2^n = o(2^{n+ \log n})
$$

✅ **Risultato:** La relazione **non è vera**, perché non esiste una costante $ c $ tale che 

$$
2^n \cdot c = 2^{n+ \log n}
$$

per ogni $n$ sufficientemente grande.

---

## **4. Tecniche di Calcolo Utili**

Ecco alcuni strumenti che possono semplificarti i calcoli:

- **Regola del quoziente:** Per verificare se $f(n) = O(g(n))$, calcola il limite:

$$
\lim_{n \to \infty} \frac{f(n)}{g(n)}
$$

    - Se il limite è **0**, allora $f(n) = o(g(n))$.
    - Se il limite è una **costante positiva**, allora $f(n) = \Theta(g(n))$.
    - Se il limite è **infinito**, allora $f(n) = \omega(g(n))$.

- **Confronto tra funzioni comuni:**
    
    - **Logaritmi crescono più lentamente di potenze.**  
        
        $$
        \log^k n = o(n^\epsilon) \quad \text{per ogni } k, \epsilon > 0.
        $$
        
    - **Le potenze crescono più lentamente delle esponenziali.**  
        
        $$
        n^k = o(2^n) \quad \text{per ogni } k > 0.
        $$

    - **Le esponenziali crescono più lentamente dei fattoriali.**  
        
        $$
        2^n = o(n!).
        $$

---

## **5. Consigli per l'Esame**

- **Fai pratica**: Risolvi più esercizi possibili per familiarizzare con le proprietà della notazione asintotica.
- **Sii metodico**: Segui sempre i passi di analisi indicati sopra per evitare errori.
- **Concentrati sui termini dominanti**: Spesso è sufficiente identificare il termine che cresce più velocemente per rispondere alla domanda.

---

## **Conclusione**

Seguendo questa guida, sarai in grado di risolvere con sicurezza l'esercizio 1.A di ogni esame di Algoritmi e Strutture Dati. Buono studio! 🚀

### ESERCIZIO 1.B
# 📖 Guida alla Risoluzione dell'Esercizio 1.B (Equazioni di Ricorrenza)

## **1️⃣ Cosa sono le Equazioni di Ricorrenza?**
Le **equazioni di ricorrenza** descrivono il costo di un algoritmo **ricorsivo** in termini del costo del problema ridotto a dimensioni minori. L'obiettivo è trovare una **stima asintotica** della soluzione, espressa in notazione $O, \Theta, \Omega$.

Ad esempio:
$$ T(n) = 2T(n/2) + n $$
significa che il problema di dimensione $n$ viene diviso in **2 sottoproblemi** di dimensione $n/2$ e che l'operazione aggiuntiva costa $O(n)$.

---

## **2️⃣ Approcci per Risolvere le Equazioni di Ricorrenza**
Esistono **3 principali metodi** per risolvere queste equazioni:

1. **Metodo del Teorema di Master** *(il più veloce per molti casi)*
2. **Metodo dell'Iterazione (Espansione Ricorsiva)**
3. **Metodo del Cambio di Variabile (Caso Speciale)**

Vediamo come usarli. 👇

---

## **3️⃣ Metodo del Teorema di Master**
Il **Teorema di Master** è il metodo più rapido per molte equazioni della forma:
$$ T(n) = aT(n/b) + f(n) $$
dove:
- $a$ è il numero di sottoproblemi,
- $b$ è il fattore di riduzione della dimensione del problema,
- $f(n)$ è il costo del lavoro extra.

### **Regole del Teorema di Master**
A seconda della crescita di $f(n)$, confrontiamo con $n^{\log_b a}$:

4. **Caso 1: Dominano le chiamate ricorsive**  
   Se $f(n) = O(n^c)$ con $c < \log_b a$, allora:
   $$ T(n) = \Theta(n^{\log_b a}) $$

5. **Caso 2: Equilibrio tra ricorsione e lavoro extra**  
   Se $f(n) = \Theta(n^{\log_b a})$, allora:
   $$ T(n) = \Theta(n^{\log_b a} \log n) $$

6. **Caso 3: Dominano le operazioni extra**  
   Se $f(n) = \Omega(n^c)$ con $c > \log_b a$ e la condizione di regolarità è soddisfatta ($a f(n/b) \leq c f(n)$ per una costante $c < 1$), allora:
   $$ T(n) = \Theta(f(n)) $$

---

### **📌 Esempi di Applicazione del Teorema di Master**
#### **Esempio 1:**  
$$ T(n) = 4T(n/2) + n^2 $$
- Qui $a = 4$, $b = 2$ e $f(n) = n^2$.
- Calcoliamo $\log_2 4 = 2$.
- Confrontiamo con $f(n) = n^2$.
- $n^2 = n^{\log_2 4}$, quindi è il **Caso 2**.

✅ **Soluzione:** $T(n) = \Theta(n^2 \log n)$.

---

#### **Esempio 2:**  
$$ T(n) = 2T(n/4) + \sqrt{n} $$
- $a = 2$, $b = 4$, $f(n) = \sqrt{n}$.
- $\log_4 2 = 1/2$.
- Confrontiamo con $f(n) = n^{1/2}$.
- Poiché $f(n)$ domina ($n^{1/2} > n^{1/2 - \epsilon}$), è il **Caso 3**.

✅ **Soluzione:** $T(n) = \Theta(\sqrt{n})$.

---

## **4️⃣ Metodo dell'Iterazione (Espansione Ricorsiva)**
Se il **Teorema di Master** non è applicabile, possiamo **espandere la ricorrenza** fino a trovare un pattern.

### **📌 Esempio**
$$ T(n) = T(n-1) + n $$
Espandiamo:

$$
T(n) = T(n-2) + (n-1) + n
$$

Continuando:

$$
T(n) = T(n-k) + (n-k+1) + \dots + n
$$

Fermiamoci a $T(1)$:

$$
T(n) = 1 + \sum_{i=1}^{n} i = 1 + \frac{n(n+1)}{2}
$$

✅ **Soluzione:** $T(n) = \Theta(n^2)$.

---

## **5️⃣ Metodo del Cambio di Variabile**
Usato quando la ricorrenza è espressa in termini di $T(\sqrt{n})$.

### **📌 Esempio**
$$ T(n) = T(\sqrt{n}) + 1 $$

Definiamo $m = \log n$, quindi $n = 2^m$ e la ricorrenza diventa:

$$ T(2^m) = T(2^{m/2}) + 1 $$

Questa è una ricorrenza lineare sulla variabile $m$, che si risolve in $O(\log \log n)$.

✅ **Soluzione:** $T(n) = \Theta(\log \log n)$.

---

# **6️⃣ Strategie Veloci per l'Esame**
✅ **Passo 1:** Identifica la forma della ricorrenza:  
   - Se è del tipo $T(n) = aT(n/b) + f(n)$, usa **il Teorema di Master**.
   - Se è tipo $T(n) = T(n-1) + g(n)$, usa **l'iterazione**.
   - Se è $T(n) = T(\sqrt{n}) + f(n)$, prova **il cambio di variabile**.

✅ **Passo 2:** Applica il metodo scelto e semplifica la soluzione.  
✅ **Passo 3:** Controlla la crescita asintotica per evitare errori.

---

# **📌 Conclusione**
Seguendo questa guida, sarai in grado di risolvere **qualsiasi esercizio di ricorrenza** presente negli esami caricati. 

💡 **Suggerimento finale:**  
- Fai pratica con **le ricorrenze più comuni**.
- **Memorizza i casi del Teorema di Master** per riconoscere velocemente il risultato.
- Usa l'**iterazione o il cambio di variabile** quando necessario.

Buono studio! 🚀🔥

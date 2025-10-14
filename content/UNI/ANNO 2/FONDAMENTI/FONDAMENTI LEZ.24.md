Fino ad ora abbiamo visto quasi tutte relazioni tra classi di complessità improprie
- ovvero senza sapere se hanno una inclusione propria oppure se hanno una coincidenza
le uniche certezze che abbiamo sono su
- $P \subset EXPTIME$ 
- $PSPACE=NPSPACE$ 

sappiamo che 
- tutti i linguaggi in PSPACE sono anche in EXPTIME 
	- $PSPACE \subseteq EXPTIME$
-  tutti i linguaggi che sono in P sono anche in NP
	- $P \subseteq NP$ 
Ma sorgono altre domande come
>[!question] 
>- $PSPACE=EXPTIME$?
>	- tutti i linguaggi di PSPACE sono in EXPTIME
>- $P \subset NP$?
>- $P=NP$?

>[!bug] Le relazioni che conosciamo sono, in massima parte, relazioni deboli

La domanda della prof che poi ci porta a creare delle cose concrete nella lezione è:
>[!question] Siano C1 e C2 classi di complessità e sia dato un linguaggio L∈C2, come facciamo a sapere se è anche incluso in C1​, oppure se è davvero un linguaggio separatore (cioè in C2∖C1​)?
>questo ci serve per capire se abbiamo $C1\subset C2$ oppure continuiamo ad avere $C1 \subseteq C2$
>

>[!tip] ![[Pasted image 20250507174234.png]]

## Potremmo forse realizzare questo sogno con le riduzioni?
Le riduzioni sono un argomento vecchio ma che ci può tornare utile
Ricapitolando cosa erano:
Dati due linguaggi $L_1 \subseteq \Sigma_1^*$ e $L_2 \subseteq \Sigma_2^*$, diciamo che  
**$L_1$ è riducibile a $L_2$**, e scriviamo: $L1 ≼ L2$ 
se **esiste una funzione** $f : \Sigma_1^* \to \Sigma_2^*$ tale che:  ^c0c563
1. **$f$ è totale e calcolabile**
	- $f(x)$ è definita per ogni $x \in \Sigma_1^*$.
	- Esiste una macchina di Turing $T_f$ tale che, per ogni $x$, $T_f$ termina con $f(x)$ scritto sul nastro di output.

2. **$f$ preserva l’appartenenza al linguaggio**
- Per ogni $x \in \Sigma_1^*$:
$$x∈L1  ⟺  f(x)∈L2$$

Quindi **decidere se $x \in L_1$ equivale a decidere se $f(x) \in L_2$**.
- in poche parole se un linguaggio ha l'input l'altro deve avere il suo rispettivo output

A queste riduzioni per il nostro scopo si aggiunge una piccola cosa
#### Rivisitazione delle riduzioni
aggiungiamo il concetto del $\pi$ 
- è un predicato ovvero una proprietà che serve per definire le funzioni totali e calcolabili prese in causa
ad esempio $\pi$ mette come proprietà che:
- $\forall x \in \Sigma_1^*, \ |f(x)| = |x|$ (la lunghezza dell'output è uguale a quella dell’input).
- inoltre come condizione di $\pi$ viene anche detto che
- $f$ è calcolabile in tempo polinomiale in funzione di $|x|$ ovvero che:
	- $f(x)$ termina in **al più $p(|x|)$ passi**, dove $|x|$ è la lunghezza della stringa $x$.

Quindi definite queste due condizioni possiamo ad esempio avere che:
Dati due linguaggi $L_1 \subseteq \Sigma_1^*$ e $L_2 \subseteq \Sigma_2^*$, diciamo che:
$$L1 ≼_\pi L2$$

se **esiste una funzione** $f : \Sigma_1^* \to \Sigma_2^*$ tale che:
- Le cose sopra delle [[#^c0c563|riduzioni]]
- f soddisfa anche $\pi$
Quindi queste $riduzioni+aggiunta$ ci possono permettere di individuare i linguaggi separatori tra due classi di complessità
- usando concetti legati alle $\pi- riduzioni$ :
	- chiusura di una classe rispetto a una $\pi- riduzione$ 
	- completezza di un linguaggio per una classe rispetto a una $\pi- riduzione$ 
questi due concetti li spiegheremo adesso con due teoremi

##### Definizione 6.4
>[!tip] Definizione 6.4
> Una **classe di complessità $\mathcal{C}$** è **chiusa rispetto a una $\pi$-riduzione** se:
> 
> Per ogni coppia di linguaggi $L_1$, $L_2$ tali che:
> 
> $$L_1 ≼_\pi L_2 \quad \text{e} \quad L_2 \in \mathcal{C}​$$
> 
> allora:
> $$L_1 \in \mathcal{C}$$

IN POCHE PAROLE
Se posso ridurre un linguaggio $L_1$ a un linguaggio $L_2$ <- che **so già appartenere** alla classe $\mathcal{C}$ e $\mathcal{C}$ è **chiusa** rispetto a quel tipo di riduzione, allora anche $L_1$ appartiene a $\mathcal{C}$
##### Definizione 6.3
>[!tip] Definizione 6.3
> Sia $\mathcal{C}$ una **classe di complessità** di linguaggi, e sia $≼_\pi$ una **$\pi$-riduzione**.
> 
> Un linguaggio $L \subseteq \Sigma^*$ è **$\mathcal{C}$-completo** rispetto alla $\pi$-riducibilità se:
> ### a) $L \in \mathcal{C}$
> Il linguaggio **fa parte della classe**.
> ### b) $\forall L_0 \in \mathcal{C} \quad L_0 ≼_\pi L$
> **Ogni altro linguaggio** nella classe $\mathcal{C}$ **si riduce a $L$ tramite $\pi$**.


La **completezza** e la **chiusura** sono strumenti centrali per:
- Studiare la **struttura interna** delle classi di complessità
- Identificare i problemi **più rappresentativi e difficili**
- Ragionare su **separazioni** tra classi (come P $\neq$ NP)
### Strategia per dire che due classi sono uguali
✅ Ipotesi iniziali:
- Hai **due classi** di complessità:
    C1⊆C2
- C1 è contenuto in C2
- Sai che $\mathcal{C}_1$ è **chiusa rispetto a una $\pi$-riduzione**  
    (cioè: se $L_2 \in \mathcal{C}_1$ e $L_1 ≼_\pi L_2$, allora anche $L_1 \in \mathcal{C}_1$)

🎯 Strategia:
1. Trova un linguaggio $L$ che sia **$\mathcal{C}_2$-completo** rispetto a $\pi$:
    - cioè:
        $L \in \mathcal{C}_2 \quad \text{e} \quad \forall L_0 \in \mathcal{C}_2, \quad L_0 ≼_\pi L$ 
    - Tutti i problemi in C2 si possono trasformare in un linguaggio L
	    - ogni problema L0 è in C2 e posso trasformare ogni problema L0 in L
- Se C1 è **chiusa** rispetto a questa riduzione (cioè: se L è in C1, anche L0 ci entra)
	- Allora **anche L0 è in C1**
2. **Dimostra che $L \in \mathcal{C}_1$**

📌 Conclusione:
Poiché:
- $L_0 ≼_\pi L$ per ogni $L_0 \in \mathcal{C}_2$
- $L \in \mathcal{C}_1$
- E $\mathcal{C}_1$ è **chiusa** rispetto a $\pi$
Allora: $\forall L_0 \in \mathcal{C}_2, \quad L_0 \in \mathcal{C}_1 \quad \Rightarrow \quad \mathcal{C}_2 \subseteq \mathcal{C}_1$

Tutti i problemi in C2 sono anche in C1
Ma già sapevamo che:
$\mathcal{C}_1 \subseteq \mathcal{C}_2$ Quindi: $\mathcal{C}_1 = \mathcal{C}_2$

Trovare un problema completo (come L) è utile perché:
- Se **appartiene a C1**, allora **tutta C2** è in C1 ⇒ **C1 = C2**
- Se **non appartiene a C1**, allora **C1 ≠ C2**

>[!tip]- precisazioni su problemi completi, ovvero i più difficili
>![[Pasted image 20250507192021.png]]

#### Teorema 6.20
Hai due classi di problemi:
- **C1** è contenuta in **C2**
- **C1 è chiusa** rispetto a una certa riduzione $\pi$
Se per caso trovassimo un linguaggio L C2–completo rispetto a una qualche riduzione$\pi$ e 
- se qualcuno riuscisse a dimostrare che C1 ≠ C2 allora sapremmo automaticamente che L ∉ C2
>[!tip] Teorema 6.20
> Date:
> - Due classi di complessità: **C₀** e **C**
> - Sappiamo che **C₀ è contenuta in C** (cioè tutti i problemi di C₀ sono anche in C)
> - Sappiamo anche che **C₀ è chiusa** rispetto a una riduzione π
> ### Il teorema dice:
> Se prendi **un linguaggio L che è C-completo** (cioè il più difficile in C),  
> allora:
> 
> **L è in C₀ se e solo se C = C₀**

![[Pasted image 20250507192212.png]]
### una particolare $\pi-riduzione$ la **riduzione polinomiale**
una $\pi$ greco riduzione in un esempio fatto prima prevedeva una funzione che doveva essere calcolata in $|x|$
- ora facciamo un esempio di $\pi -riduzione$ che lo fa in tempo polinomiale

Dati due linguaggi L₁ e L₂​, diciamo che:
> **“L₁ è polinomialmente riducibile a L₂”**


Esiste una funzione$f: \Sigma_1^* \to \Sigma_2^*$ tale che:
1. **f è totale e calcolabile in tempo polinomiale**
	- f è **definita per ogni input** $x \in \Sigma_1^*$
	- esiste una macchina di Turing $T_f$ che calcola f(x)
	- il tempo di calcolo $dtime(T_f, x)$ è **al massimo un polinomio** nella lunghezza di x inteso come:  $O(|x|^c)$
> In altre parole: si può calcolare f(x) in “tempo ragionevole” (cioè non esplosivo)

2. **f conserva la verità del problema**
Per ogni parola $x \in \Sigma_1^*$​:

>$x \in L₁ \iff f(x) \in L₂$

Cioè: **posso decidere se x sta in L₁ controllando se f(x) sta in L₂**

in poche parole se esiste una **funzione f** che trasforma ogni istanza di L₁​ in un’istanza di L₂​, e questa trasformazione:
- è **corretta**
- è **calcolabile in tempo polinomiale**

>[!warning] d'ora in poi scriveremo $≼$ per intendere però: $≼_p$ ovvero una riduzione polinomiale

### **come usare una riduzione polinomiale per costruire una macchina che decide un linguaggio**, sfruttando un altro linguaggio che sappiamo già decidere.

## 🎯 Obiettivo
Hai due linguaggi, **L1** e **L2**, e vuoi **decidere se una parola x sta in L1**.

**Il nuovo strumento**
- Abbiamo due linguaggi, $L_1 \subseteq \Sigma_1^*$ e $L_2 \subseteq \Sigma_2^*$
    
    > Sono due insiemi di stringhe su alfabeti diversi. $L_1$ è quello che vogliamo decidere.
- Riusciamo a dimostrare che $L_1 \preceq L_2$ (cioè: **$L_1$ è riducibile a $L_2$** in tempo polinomiale)
    > Possiamo trasformare ogni input $x$ per $L_1$ in un input $f(x)$ per $L_2$, in modo "veloce" (tempo polinomiale)

- Esistono un trasduttore $T_f$ e una costante $c$ tali che:
    - per ogni $x \in \Sigma_1^*$:  
        $x \in L_1 \iff f(x) \in L_2$,  
        e inoltre $\text{dtime}(T_f, x) \in O(|x|^c)$
    > Il trasduttore calcola $f(x)$ in tempo polinomiale e conserva la verità tra $L_1$ e $L_2$

- Supponiamo di sapere che $L_2 \in \text{DTIME}[f(n)]$

    > Significa che esiste un algoritmo deterministico (una macchina $T_2$) che decide $L_2$ entro tempo $f(n)$
    
- Quindi: esiste un riconoscitore $T_2$ tale che, per ogni $y \in \Sigma_2^*$:
    - $T_2(y)$ accetta se e solo se $y \in L_2$
    - $\text{dtime}(T_2, y) \in O(f(|y|))$
    > $T_2$ è una macchina affidabile che decide $L_2$ in tempo noto
    
 Allora possiamo costruire una macchina $T_1$ che decide $L_1$:

$T_1$ lavora in due **fasi** e usa **due nastri**:

**FASE 1**

- $T_1$ simula $T_f(x)$ e scrive l’output $y = f(x)$ sul secondo nastro
    > Sta traducendo il problema da $L_1$ in un’istanza equivalente di $L_2$ che aveva $f(x)$
**FASE 2**
- $T_1$ simula $T_2(y)$ sul secondo nastro
    - Se $T_2$ accetta, allora $T_1$ accetta
    - Se $T_2$ rifiuta, anche $T_1$ rifiuta
    > Usa $T_2$ per decidere se $x \in L_1$, passando per $f(x)$
**Conclusione:**
- $T_1$ **decide $L_1$**, perché:
    - $T_2(y)$ accetta $\iff y \in L_2$
    - $y = f(x)$ e $x \in L_1 \iff f(x) \in L_2$
    > Se funziona per $L_2$, allora funziona anche per $L_1$

**Quanto tempo impiega $T_1$ a decidere $L_1$?**
> (Serve per sapere in che classe di complessità finisce $L_1$)
- Abbiamo due linguaggi, $L_1 \subseteq \Sigma_1^*$ e $L_2 \subseteq \Sigma_2^*$
- Abbiamo dimostrato che $L_1 \preceq L_2$
- E sappiamo che $L_2 \in \text{DTIME}[f(n)]$
    > Quindi possiamo usare una macchina $T_2$ per decidere $L_2$ in tempo deterministico $f(n)$

per quanto riguarda invece il tempo che impiega $T_1$ a decidere $L_1$

Con input $x$:
- **FASE 1** (calcolo della riduzione):  
    $\text{dtime}(T_f, x) \in O(|x|^c)$
    > Serve per trasformare $x$ in $y = f(x)$
- **FASE 2** (verifica con $T_2$):  
    $\text{dtime}(T_2, y) \in O(f(|y|))$
    > Serve per verificare se $f(x) \in L_2$

il risultato sarà la somma delle due fasi!

nella fase 2 abbiamo detto che impiega $f(|y|)$
- Poiché $T_f(x)$ impiega $O(|x|^c)$ per calcolare $y$
- e scrivere la simulazione sul secondo nastro di $T_1$ richiede almeno tanti passi quanto al lunghezza di $y$ 
Quindi la lunghezza $|y|$ è **al massimo** $O(|x|^c)$

Si fa la somma dei due e quindi
il tempo che impiega $T_1$ a decidere $L_1$ è
$$O(∣x∣^c+f(∣x∣^c))$$
e si scrive anche come:
$$L1​∈DTIME[n^c+f(n^c)]$$
### Conclusione su questa parte

RICAPITOLIAMO: abbiamo due linguaggi, $L_{1} ⊆ Σ_{1}^{*}$ e $L{2} ⊆ Σ{2}^{*}$, e sappiamo che $L_{1} ≼ L_{2}$
### Conclusione su questa parte
RICAPITOLIAMO: abbiamo due linguaggi, $L_{1} ⊆ Σ_{1}^{*}$  e $L_{2} ⊆ Σ_{2}^{*}$,  e sappiamo che $L_{1} ≼ L_{2}$

>[!tip] Grazie a quello che abbiamo visto prima, siamo riusciti a dimostrare che se $L_{2} \in P$ allora $L_{1}\in P$
>Infatti, in questo caso esiste una costante `k` tale che $$L_{2} \in \text{DTIME}[n^{k}]$$
>-> allora da quanto visto nella dimostrazione precedente $$L_{1} \in \text{DTIME}[n^{c} + (n^{c})^{k}] \subseteq P$$

Ossia abbiamo dimostrato il seguente teorema
#### Teorema 6.21
>[!lemma] TEOREMA 6.21
>Se 
>- $L_{1} ≼ L_{2}$  
>- e  $L_{2} \in P$  
>- $\ \Rightarrow \ L_{1} \in P$ 
>
>Ossia, il teorema dice che la classe P è chiusa rispetto alla riducibilità polinomiale.

Se hai:
- Due linguaggi $L_1$ e $L_2$
- E $L_1 \preceq L_2$ (cioè $L_1$ si riduce a $L_2$ in tempo polinomiale)
- E $L_2$ si risolve in **tempo polinomiale**
Allora anche **$L_1$ si risolve in tempo polinomiale**, quindi:
> **$L_1 \in P$**

In sintesi:

> Se trasformi un problema in un altro in tempo polinomiale, e l’altro è in P, allora anche il primo è in P..

Anche per altre classi non deterministiche
![[Pasted image 20250507212513.png]]

### I linguaggi NP-completi_

- A questo punto, **abbandoniamo le generiche $\pi$-riduzioni**  
    e **torniamo definitivamente alle nostre riduzioni polinomiali**
    
    > Da ora in poi, si usa il simbolo $\preceq$ per indicarle
    
- Un linguaggio $L \subseteq \Sigma^*$ è **NP-completo** (rispetto alla riducibilità polinomiale) se:
    
    a) L∈NP
    b) $∀L0​∈NP, \  L0​⪯L$
- I linguaggi NP-completi sono importanti per il loro ruolo di **linguaggi separatori** tra le classi **P** e **NP**

---

### 🧩 Corollario 6.4:

> **Se $P \ne NP$, allora per ogni linguaggio NP-completo $L$, si ha $L \notin P$**

- Supponiamo invece che $L$ sia **NP-completo** e anche **$L \in P$**
    
- Poiché $L$ è NP-completo, allora:
    
    $\forall L_0 \in \text{NP}, \quad L_0 \preceq L$
- Ma $P$ è chiusa rispetto a $\preceq$ ⇒ quindi anche:
    
    $\forall L_0 \in \text{NP}, \quad L_0 \in P$
- Dunque: $\text{NP} \subseteq \text{P}$ ⇒ $\text{P} = \text{NP}$, **contraddicendo l’ipotesi**

### 📘 _I problemi NP-completi_

- Ma qual è il senso del Corollario 6.4?

> È **molto improbabile** che **un linguaggio NP-completo appartenga a P**

- Perché? Perché **si sospetta che $P \ne NP$**, ma nessuno è mai riuscito a dimostrarlo  
    → È **la congettura fondamentale della complessità computazionale**
    
- È così importante che c’è una **taglia da 1 milione di dollari** per chi risolve la congettura (o la sua negazione)

### ❗ Quindi:

Se vogliamo **dimostrare** (probabilmente) che **non esiste un algoritmo deterministico polinomiale** per un certo problema in NP...

> ... dobbiamo **dimostrare che quel problema è NP-completo**

---

### 💰 E se invece troviamo un algoritmo polinomiale per un NP-completo?

> Abbiamo vinto **un milione di dollari**  
> ... oppure, ehm, **abbiamo sbagliato qualcosa** 😅

---

### 📘 _Uso delle riduzioni_

- Le **riduzioni** sono uno strumento fondamentale anche **nella calcolabilità**:
    
    - Se dimostro che:
        
        $L_1 \preceq L_2 \quad \text{e} \quad L_2 \text{ è decidibile}$
        allora anche $L_1$ è **decidibile**
        
    - Se invece:
        
        $L_0 \preceq L_1 \quad \text{e} \quad L_0 \text{ non è decidibile}$
        
        allora anche $L_1$ **non è decidibile**
        

---

- Allo stesso modo, **le riduzioni polinomiali** sono utili per la **complessità**:
    
    - Se dimostro che:
        $L_1 \preceq L_2 \quad \text{e} \quad L_2 \in P$
        allora:
        $L_1 \in P$
    - Se invece:
        $L_0 \preceq L_1 \quad \text{e} \quad L_0 \notin P \text{ (probabilmente)}$
        allora:
        $L_1 \notin P \text{ (probabilmente)}$

> Perché un linguaggio **non può essere più facile** di uno a cui **tutti si riducono**
---

- Ma di questo parleremo **(e abbondantemente!) nella dispensa 9**

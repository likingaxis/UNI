# Compendio ASD — Esercizi 1 & 2 (versione compatta in Markdown)

> Obiettivo: lista **autosufficiente** di argomenti per rispondere correttamente ai V/F, mini‐prove e domande a tranello degli **Esercizi 1 e 2**. Include le **AGGIUNTE FONDAMENTALI** emerse dagli scritti.

---

## ESERCIZIO 1

### MST (Minimum Spanning Tree)
- Cycle property / Cut property
- Differenze MST vs SPT (Shortest Path Tree)
- Complessità di Prim / Kruskal, e impatto delle strutture dati Union-Find
- Casi particolari (pesi tutti uguali, grafi completi, archi {1,2}, ecc.)
- **AGGIUNTE FONDAMENTALI**
  - **Forme forti delle proprietà**
    - **Cycle**: l’**arco più pesante di un ciclo** **non** appartiene ad **alcun** MST.
    - **Cut**: **ogni** arco **strettamente minimo** su un taglio appartiene a **tutti** gli MST; in caso di pari peso, ciascuno sta in **almeno un** MST.
  - **Unicità / non‐unicità**
    - MST **unico** con **pesi tutti distinti**.
    - Con pesi uguali: **non unico** (se pesi=1 **ogni ST è un MST**).
  - **SPT ≠ MST (anche con pesi positivi)**
    - SPT minimizza distanze da una sorgente, MST minimizza **somma pesi** degli archi: in generale diversi.
    - Caso pesi=1: uno **SPT fissato** può **non** coincidere con un **MST fissato** (insiemi di archi diversi).
  - **Correttezza**
    - **Prim** via **Cut property** (arco minimo che attraversa il taglio \=(S, V\\S) è “sicuro”).
    - **Kruskal** via **Cycle/Cut** + **exchange argument** (inserire archi in ordine crescente senza creare cicli).
  - **Bound e casi {1,2}**
    - Massimizzare archi da 1; saper derivare **limiti** sul costo MST in funzione di |V| e #archi di peso 1.
    - Grafi completi: complessità \(O(E\log V)\) con \(E=\Theta(V^2)\).

**Complessità (promemoria)**
- **Prim**: \(O(E\log V)\) (heap binario); \(O(E+V\log V)\) (Fibonacci heap).
- **Kruskal**: \(O(E\log V)\) + UF ammortizzato \(O(\alpha(V))\).

---

### Max Flow / Min Cut
- Teorema max-flow min-cut
- Complessità Ford-Fulkerson (esponenziale o polinomiale con capacità intere)
- **AGGIUNTE FONDAMENTALI**
  - **Grafo residuo \(G_f\)**: archi **forward** con capacità \(c-f\) e **backward** con capacità \(f\). **Bottleneck** su un cammino aumentante.
  - **Condizione di ottimalità**: **nessun cammino** \(s\leadsto t\) in \(G_f\) **⇔** flusso **massimo** (**⇔** esiste un **min-cut** con capacità = valore del flusso).
  - **Edmonds–Karp (EK)**: sceglie cammini a **minimo #archi** (BFS); #augmentazioni \(O(VE)\) ⇒ **tempo \(O(VE^2)\)** (polinomiale).
  - **Estrazione del min-cut da un max-flow**: prendi l’insieme **R** dei vertici raggiungibili da \(s\) in \(G_f\) finale ⇒ il taglio \((R, V\\R)\) è **minimo** e \(|f| = c(R,V\\R)\).
  - **Terminazione di FF**: con **capacità intere** termina (tempo **pseudo‐polinomiale**, dipende da \(|f^*|\)); con **irrazionali** può **non** terminare.

**Frasi T/F tipiche**
- “C’è un arco con capacità residua vicino a \(t\) ⇒ esiste un cammino aumentante” → **Falso** (serve un **percorso completo** da \(s\) a \(t\)).  
- “Assenza di cammini aumentanti ⇒ flusso massimo” → **Vero**.  
- “FF è sempre polinomiale” → **Falso**; **EK** sì, \(O(VE^2)\).  
- “Il flusso netto attraverso **qualunque** taglio vale \(|f|\)” → **Vero** (definizione di valore del flusso).

---

### Union-Find (Disjoint Set Union, DSU)
- QuickFind, QuickUnion, con/ senza euristiche, e complessità ammortizzate
- Uso in Kruskal.
- **AGGIUNTE FONDAMENTALI**
  - **Union-by-rank/size + path compression**: costo **ammortizzato** \(O(\alpha(n))\) per operazione; differenza da worst‐case.
  - **Altezza delle foreste**: \(\Theta(\log n)\) senza compression (con rank/size); come **costruire sequenze testimoni**.
  - **Lower bound**: per \(m\) operazioni su \(n\) elementi, tempo totale \(\Omega(m+n)\) è inevitabile.
  - **Impatto in Kruskal**: sorting \(O(E\log V)\) domina; UF è “quasi \(O(1)\)” ammortizzato.

**T/F rapidi**
- “`find` è \(O(1)\) worst‐case con compression+rank” → **Falso** (è \(O(\alpha(n))\) ammortizzato).  
- “QuickFind ha `union` \(O(n)\)” → **Vero**.  
- “Union-by-size garantisce altezza \(\Theta(\log n)\) (senza compression)” → **Vero**.

---

### Problemi Greedy/PD classici (più rari in E1, ma compaiono)
- **Interval Scheduling** (ordinare per **earliest finish time**, exchange argument).
- **Load Balancing** (due **lower bound**: media e job più lungo) — utile per 2-approx.
- **AGGIUNTE UTILI**
  - **Interval Partitioning**: **depth** = #macchine ottimo; greedy con priority queue.

---

## ESERCIZIO 2 (promemoria integrato)

- **Flussi (max-flow, min-cut, Ford–Fulkerson)**
  - **EK \(O(VE^2)\)** vs FF (pseudo‐polinomiale);  
  - **Min-cut** da \(G_f\) finale (raggiungibili da \(s\)) con sketch di correttezza;  
  - **Definizioni brevi**: flusso, valore, residua, cammino aumentante, capacità di un taglio.
- **MST (cut property, Prim)**
  - Proof sketch di Prim via cut property; unicità con pesi distinti; controesempi MST≠SPT.
- **Scheduling (Interval Scheduling, Interval Partitioning, Load Balancing)**
  - IS: EFT + exchange argument; IP: depth + heap; LB per 2-approx del LB.
- **Load Balancing 2-approx**
  - Due LB (media e job max) ⇒ fattore 2.
- **Classi di complessità (NP, riduzioni polinomiali, Vertex Cover)**
  - Definizioni **NP / NP-hard / NP-complete** (certificato verificabile in tempo polinomiale).
  - **Riduzione polinomiale**: funzione calcolabile in polinomiale che preserva sì/no.
  - Esempi: **3-SAT → Independent Set / Vertex Cover** (idea di gadget).  
  - Decisione vs Ottimizzazione: perché si usa la versione **decisione** per NP-completezza.

---

### Micro-schemi “pronti” (1–2 righe)
- **Cut property (proof sketch)**: arco strettamente minimo su un taglio è sicuro; se manca dall’MST, aggiungilo → ciclo; sostituisci un arco sul taglio non più leggero ⇒ costo non aumenta ⇒ contraddizione.
- **Cycle property (proof sketch)**: arco più pesante di un ciclo può essere rimosso e sostituito con altro del ciclo senza aumentare il costo ⇒ non appartiene ad alcun MST.
- **Min-cut da max-flow**: \(R\)=raggiungibili da \(s\) in \(G_f\) finale ⇒ tutti gli archi da \(R\) a \(V\\R\) sono saturi ⇒ \(c(R,V\\R)=|f|\) ⇒ taglio minimo.

---

### Tabella flash complessità
- **Prim**: \(O(E\log V)\) (binario); \(O(E+V\log V)\) (Fibonacci).
- **Kruskal**: \(O(E\log V)\) + UF \(O(\alpha(V))\) ammortizzato/operazione.
- **UF (rank+compression)**: \(O(m\,\alpha(n))\) su \(m\) operazioni.
- **Ford–Fulkerson** (capacità intere): termina; tempo pseudo‐polinomiale (dipende da \(|f^*|\)).
- **Edmonds–Karp**: \(O(VE^2)\).

---

*(Suggerimento: stampa questa pagina e ripassa le **frasi T/F** e i **micro‐schemi**: coprono la maggioranza dei tranelli.)*

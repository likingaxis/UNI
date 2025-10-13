### ESERCIZIO 1
- **MST (Minimum Spanning Tree)**
    - Cycle property / Cut property
    - Differenze MST vs SPT (Shortest Path Tree)
    - Complessità di Prim / Kruskal, e impatto delle strutture dati Union-Find
    - Casi particolari (pesi tutti uguali, grafi completi, archi {1,2}, ecc.)
    - **AGGIUNTE FONDAMENTALI**
        - **Forme “forti” delle proprietà:**  
            _Cycle (heaviest-in-cycle non sta in alcun MST); Cut (ogni arco strettamente minimo sul taglio sta in tutti gli MST)._
        - **Unicità/non-unicità:** MST unico con pesi **tutti distinti**; con pesi uguali **non** unico (con pesi=1 ogni ST è un MST).
        - **SPT ≠ MST con esempi:** saper costruire **controesempi** anche quando i pesi sono tutti positivi; caso “pesi=1”: SPT fissato può **non** coincidere con un MST fissato.
        - **Correttezza di Prim via Cut property** (schema di scambio) e di Kruskal via Cycle/Cut (exchange argument).
        - **Bound e casi {1,2}:** saper derivare/giustificare limiti sul costo dell’MST e quando si massimizzano gli archi di peso 1.
            
- **Max Flow / Min Cut**
    - Teorema max-flow min-cut
    - Complessità Ford-Fulkerson (esponenziale o polinomiale con capacità intere)
    - **AGGIUNTE FONDAMENTALI**
        - **Grafo residuo operativo:** archi forward c−fc-fc−f e backward fff; **bottleneck**; perché “capacità libera vicino a ttt” **non** implica per forza un cammino aumentante.
        - **Condizione di ottimalità:** “nessun cammino aumentante in GfG_fGf​” ⇔ flusso massimo (equivalenza col min-cut).
        - **Edmonds–Karp (BFS):** scelta del cammino a **minimo #archi**, **complessità O(VE2)O(VE^2)O(VE2)**, monotonia delle distanze residue.
        - **Estrazione del min-cut da un max-flow:** insieme dei **raggiungibili** da sss in GfG_fGf​ finale ⇒\Rightarrow⇒ taglio minimo (R,V ⁣∖ ⁣R)(R,V\!\setminus\!R)(R,V∖R) con sketch di correttezza.
            
        - **Terminazione FF:** con capacità **intere** termina (pseudo-polinomiale, dipende da $∣|f^*|$; con capacità **irrazionali** può non terminare.
            
- **Union-Find**
    
    - QuickFind, QuickUnion, con/ senza euristiche, e complessità ammortizzate
        
    - Uso in Kruskal.
        
    - **AGGIUNTE FONDAMENTALI**
        
        - **Union-by-rank/size + path compression:** costo **ammortizzato** $O(\alpha(n))$ per operazione; differenza da worst-case.
            
        - **Altezza delle foreste:** $\Theta(\log n)$) senza compression (con rank/size); come **costruire sequenze testimoni**.
            
        - **Lower bound generale:** qualunque struttura simile richiede Ω(m+n)\Omega(m+n)Ω(m+n) tempo totale su mmm operazioni.
            
        - **Impatto pratico in Kruskal:** sorting $O(E\log V) + UF$ “quasi $O(1)$” ammortizzato.
            
- **Problemi Greedy o PD classici** (più rari in Esercizio 1, ma compaiono in qualche sessione)
    
    - Interval Scheduling
        
    - Load Balancing
        
    - **AGGIUNTE UTILI (se compaiono)**
        
        - **Interval Partitioning:** concetto di **depth** = #macchine ottimo; greedy con priority queue.
            
        - **Prove lampo:** _exchange argument_ per IS; due **lower bound** (media e job più lungo) per il **2-approx** del Load Balancing.
            

---

### ESERCIZIO 2

Sì, anche l’Esercizio 2 ha pattern forti:

- **Flussi (max-flow, min-cut, Ford-Fulkerson)**
    
    - **AGGIUNTE FONDAMENTALI**
        
        - **Edmonds–Karp $O(VE^2)$** e confronto con FF (pseudo-polinomiale).
            
        - **Algoritmo per il min-cut da $G_f$** e relativa giustificazione.
            
        - **Definizioni “brevi” pronte:** flusso, capacità di un taglio, residua, cammino aumentante, valore del flusso.
            
- **MST (cut property, Prim)**
    
    - **AGGIUNTE FONDAMENTALI**
        
        - **Proof sketch di Prim tramite cut property**;
            
        - **Unicità con pesi distinti e non-unicità con pari peso**;
            
        - **Controesempi rapidi** per falsificare affermazioni tipiche (MST=SPT, ecc.).
            
- **Scheduling (Interval Scheduling, Interval Partitioning, Load Balancing)**
    
    - **AGGIUNTE FONDAMENTALI**
        
        - **IS:** ordinare per **earliest finish time** + exchange argument.
            
        - **IP:** **depth** come lower bound e greedy ottimo con heap.
            
        - **Load Balancing 2-approx:** due LB (media, job max) e prova del fattore 2.
            
- **Load Balancing 2-approx**
    
- **Classi di complessità (NP, riduzioni polinomiali, Vertex Cover)**
    
    - **AGGIUNTE FONDAMENTALI**
        
        - **Definizioni nette:** NP, NP-hard, NP-complete; **certificato** verificabile in tempo polinomiale.
            
        - **Riduzione polinomiale (formale):** funzione calcolabile in polinomiale che preserva sì/no.
            
        - **Esempi canonici:** 3-SAT →\rightarrow→ **Independent Set** / **Vertex Cover** (idea dei gadget).
            
        - **Decisione vs ottimizzazione**: perché si riduce su versioni **decisione** per la NP-completezza.

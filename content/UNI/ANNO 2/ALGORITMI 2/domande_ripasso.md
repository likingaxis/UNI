# Domande di ripasso ASD

## Greedy – Interval Scheduling / Partitioning
1. Perché l’ordinamento per tempo di fine è l’unico greedy corretto per Interval Scheduling?
2. Cos’è la **depth** di un’istanza di Interval Partitioning e perché fornisce un lower bound al numero di aule?
3. Spiega in 3 righe la differenza tra IS e IP e quali sono i rispettivi criteri greedy.

## Union-Find
4. Differenze di complessità tra **QuickFind**, **QuickUnion**, e **QuickUnion + UBS/Path compression**.
5. Spiega perché in QuickFind con union-by-size ogni elemento può cambiare id al massimo log n volte.
6. Mostra una sequenza di union che porta a un albero di altezza log n in QuickUnion con union-by-size.
7. In che modo Union-Find viene usato nell’algoritmo di Kruskal?

## MST (Kruskal, Prim, proprietà)
8. Enuncia la **cut property** e spiega in 2 righe come giustifica Kruskal.
9. Enuncia la **cycle property** e spiega in 2 righe come giustifica Kruskal.
10. Perché se i pesi sono distinti l’MST è unico?
11. MST e SPT coincidono? In quali casi sì?
12. È possibile che l’arco più pesante del grafo appartenga a un MST? Motivare.
13. Cosa fa l’algoritmo **reverse-delete** e su quale proprietà si basa?

## Clustering (da MST)
14. Cos’è lo **spacing** di un clustering?
15. Perché togliere i k−1 archi più pesanti dall’MST produce il clustering a spacing massimo?

## Programmazione dinamica classica
16. Scrivi la ricorrenza per il **Weighted Interval Scheduling** e spiega il ruolo di p(j).
17. Scrivi la ricorrenza per **Independent Set su cammino**.
18. Spiega come funziona il **traceback** nel knapsack problem.
19. Cos’è il vantaggio dell’algoritmo di Hirschberg rispetto alla DP classica per sequence alignment?
20. Scrivi la ricorrenza del **Bellman–Ford** in termini di numero massimo di archi usati.

## Max Flow / Min Cut
21. Enuncia il **teorema max-flow min-cut**.
22. Definisci la rete **residua** e il concetto di **cammino aumentante**.
23. Perché Ford–Fulkerson può essere esponenziale? In quali casi è polinomiale?
24. Come si calcola un min-cut a partire da un flusso massimo?
25. Perché Edmonds–Karp è polinomiale? Qual è la sua complessità?

## Algoritmi di approssimazione
26. Definisci cos’è un algoritmo di α-approssimazione per un problema di minimizzazione.
27. Quali sono i due lower bound usati per analizzare il problema del load balancing?
28. Perché l’algoritmo LPT (Longest Processing Time) funziona meglio di list scheduling semplice?
29. Enuncia la strategia greedy 2-approssimata per il problema del **k-center**.

## Riduzioni polinomiali / Complessità
30. Definisci formalmente una riduzione polinomiale X ≤P Y.
31. Mostra come si riduce **Independent Set ↔ Vertex Cover**.
32. Mostra come si riduce **Vertex Cover ≤p Set Cover**.
33. Descrivi la costruzione della riduzione **3-SAT ≤p Independent Set**.
34. Cosa significa X ≡P Y?
35. Qual è la differenza tra P, NP ed EXP?

## 📌 **1. Algoritmi numerici e ricorsivi**

- `fibonacci1` – formula chiusa (approssimazione)
    
- `fibonacci2` – ricorsivo semplice
    
- `fibonacci3` – iterativo con array
    
- `fibonacci4` – iterativo con due variabili
    
- `fibonacci5` – potenze di matrici
    
- `fibonacci6` – esponenziazione binaria di matrici
    
- **Torre di Hanoi**
    
- **Problema della celebrità**
    
- **Algoritmo Alg1** – pesatura lineare
    
- **Algoritmo Alg4** – pesatura logaritmica (divide et impera)
    

---

## 📌 **2. Ricerca**

- **Ricerca sequenziale**
    
- **<font color="#9bbb59">Ricerca binaria ricorsiva</font>**
    

---

## 📌 **3. Ordinamento – Quadratici**

- **Selection Sort**
    
- **Insertion Sort**
    
- **Bubble Sort**
    

---

## 📌 **4. Ordinamento – Divide et Impera**

- **Merge Sort** (con `Merge`)
    
- **Quick Sort** (con `Partition`)
    
- **Quick Sort randomizzato**
    

---

## 📌 **5. Ordinamento – Heap e strutture**

- **<font color="#9bbb59">Heap Sort</font>**
	- si divide in minheap o maxheap
		- il padre era o più grande o più piccolo dei figli
	- `Heapify`, `FixHeap`, `EstraiMax`
    

---

## 📌 **6. Ordinamento – Lineari (non per confronto)**

- **Integer Sort** / **Counting Sort**
	- array ausiliario che mettevi quante volte appare quel numero da quell'indice
    
- **Bucket Sort**
	- uguale al integer sort ma usa una struttura con puntatori per salvare eventuali informazioni satellite
    
- **Radix Sort**
	- era quello delle colonne dei numeri, fa prima le unità poi le decine ecc...
	- ogni posizione ordinata dal bucket
    

---

## 📌 **7. Visite su grafi**

- **DFS (Depth First Search)**
	- PROFONDITÀ
    
- **BFS (Breadth First Search)**
	- AMPIEZZA
    
- Visite multiple su componenti non connesse
    

---

## 📌 **8. Usi avanzati della DFS**

- **Individuazione cicli** in grafi orientati
    
- **Ordinamento topologico**
    
- **Classificazione degli archi** (in avanti, indietro, trasversali)
    
- **Calcolo delle Componenti Fortemente Connesse (CFC)**
    
    - DFS su grafo trasposto
        
    - DFS ordinata su post(v)
        

---

## 📌 **9. Cammini minimi**

- **<font color="#9bbb59">Algoritmo di Dijkstra</font>**
    
    - Con heap binario, binomiale, Fibonacci heap
        
- **Albero dei cammini minimi (SPT)**
    

---

## 📌 **10. Strutture dati fondamentali**

- **Pila** (array e liste)
    
- **Coda** (array e liste)
    
- **Liste** (collegate, doppiamente collegate)
    
- **Array**
    
- **Foresta di visita (da DFS)**
    

---

## 📌 **11. Alberi e dizionari**

- **Albero Binario di Ricerca (BST)**
    
    - `search(k)`, `insert(e,k)`, `delete(e)`
        
    - `min`, `max`, `predecessore`, `successore`
        
- **Albero AVL**
    
    - `insert`, `delete` con bilanciamento
        
    - Rotazioni: SS, SD, DS, DD
        

---

## 📌 **12. Code con priorità**

- Implementazioni:
    
    - **Array ordinato / non ordinato**
        
    - **Lista ordinata / non ordinata**
        
- **Heap binario**
    
- **d-Heap**
    
- **Heap binomiale**
    
- **Heap di Fibonacci**
    

---

## 📌 **13. Algoritmi su oracoli e range query**

- `CostruisciOracolo`
    
- `InterrogaOracolo`
    
- Versione logaritmica con intervalli
    

---

## 📌 **14. Teoria e tecniche di analisi**

- **Risoluzione di ricorrenze**:
    
    - Iterazione
        
    - Albero di ricorsione
        
    - Metodo di sostituzione
        
    - Teorema Master
        
    - Cambio di variabile
        
- **Analisi della complessità asintotica**:
    
    - Notazioni: OOO, Θ\ThetaΘ, Ω\OmegaΩ, ooo, ω\omegaω
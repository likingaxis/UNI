## Classifiche delle grammatiche di Chomsky
Chomsky definì 3 tipi di grammatiche:
- $G_0$
- $G_1$
- $G_2$
- $G_3$
![[Pasted image 20250402174545.png|300]]

Ogni grammatica interna è sottoinsieme di quella esterna
$$G3 ⊆ G2 ⊆ G1⊆ G0$$

Ogni grammatica genera un linguaggio $L_{i}$ 
con $$L3 ⊆ L2 ⊆ L1⊆ L0$$
### Definiamo le varie grammatiche
- Di tipo 0 sono illimitate senza vincoli come quelle viste finora
- Di tipo 1 se 
	- per ogni proiezione tipo $\alpha \rightarrow \beta$ abbiamo che $\alpha \leq \beta$ 
	- tipo $aBA → c$ non è ammessa in una grammatica di tipo 1
- Di tipo 2 se
	- la parte sinistra della produzione è un solo carattere non terminale
	- quindi abbiamo una forma $A \rightarrow \alpha$ con $A \in V_N \ e \ \alpha \in (V_T \cup V_N)*$
	- $aB → cd$ non è ammesso
	- questa grammatica si dice context-free
- Di tipo 3 se
	- la parte sinistra è un solo simbolo non terminale e quella destra un solo simbolo terminale
	- ossia, le produzioni di una grammatica di tipo 3 hanno tutte la forma A → a oppure $A \rightarrow aB$ con $A,B \in V_N \ e \  a\in V_T$  
	- viene detta grammatica regolare
		- in poche parole:
			- o un **solo simbolo terminale**
			- oppure un **simbolo terminale seguito da un non terminale**
>[!bug] La parola vuota $\epsilon$ è solo nella grammatica di tipo 0


Tuttavia possiamo comunque prendere le grammatiche >0 e estenderle per generare lo stesso linguaggio della grammatica di partenza con in più la parola vuota
aggiungiamo quindi un nuovo non terminale $S’$ che assumerà il ruolo di assioma (e, dunque il vecchio assioma $S$ non sarà più assioma perché $S'$ lo subentra ) 
inseriamo poi la produzione S’ → $\epsilon$ inseriamo la produzione$S’ \rightarrow S$
procediamo a dimostrare 
### Teorema per G1
![[Pasted image 20250402194448.png]]
Una epsilon produzione è quando abbiamo una produzione nella forma $\alpha \rightarrow \epsilon$ 
quindi praticamente dice che non posso avere $\alpha \rightarrow S$ perché non rispetterebbe le regole
ciò però non ci vieta di togliere questa limitazione per ogni t>1
## Teorema per G2
![[Pasted image 20250402195403.png]]
praticamente quello che dice è che se rimuoviamo le epsilon produzioni dalla grammatica otteniamo una grammatica normalissima con il tipo t>1 allora significa che possiamo estendere con epsilon quindi rispondiamo alla cosa detta prima
Questo teorema non si applica a G1 perché non si rispetterebbe la regola del <=

## Teorema G3
![[Pasted image 20250402201529.png]]


# ESEMPIO 4

![[Pasted image 20250402201656.png]]
Quindi praticamente dobbiamo generare tutte parole uguali una a fianco dell'altra
con tali produzioni
![[Pasted image 20250402201712.png]]
![[Pasted image 20250402201732.png]]

# ESERCIZIO
![[Pasted image 20250402201610.png]]
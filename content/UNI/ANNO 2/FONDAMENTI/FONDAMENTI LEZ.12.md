# Grammatica
fino ad ora abbiamo avuto a che fare con macchine che dato un linguaggio lo riconoscono e svolgono dei compiti
Iniziamo ora ad approcciarci alla grammatica che ha come scopo quello di generare tutte le parole di un linguaggio 
- grammatica è il nome del modello generativo 
nelle lezioni a venire compresa questa chiariremo le seguenti cose:
- come sono definite le grammatiche
- come fanno a generare linguaggi e in che senso
- quali proprietà hanno
- che relazione c'è tra grammatiche e macchine di Turing
##### Come sono definite
Le Grammatiche sono una quadrupla $G=<V_t,V_n,P,S>$ che sono rispettivamente:
- $V_t$  è l’insieme dei simboli terminali (che corrisponde all’alfabeto Σ) .
	- Esempio: se voglio descrivere parole fatte solo da $a \ e \ b$, allora avrò $V_T=\{a,b\}$ 

- $V_n$ è l’insieme dei simboli non terminali 
	- vengono usate come lettere temporanee per facilitare le trasformazioni
	- alla fine dell'output non appaiono
	- non fanno parte dell'insieme $\Sigma$ 

- S ∈ $V_n$ è un particolare simbolo non terminale detto assioma 
	- l'assioma è l'inizio del processo di produzione
	- Tutte le derivazioni iniziano da $S$, quindi è il punto di partenza.

- $P$ è l’insieme delle produzioni
	- Le **produzioni** sono le regole che **permettono di sostituire** simboli non terminali con altri simboli (terminali o non).
	- Ogni produzione è una coppia:$(\alpha, \beta) \in (V_T \cup V_N)^* \times (V_T \cup V_N)^*$ 
    dove:
    - α e β sono **stringhe (parole)** di simboli terminali e/o non terminali.
    - L’asterisco `*` indica che possono essere **stringhe di lunghezza arbitraria**, anche vuote.
    - **Condizione importante**: α deve contenere **almeno un simbolo non terminale**, altrimenti non avrebbe senso trasformarla.
- almeno una produzione è nella forma $S \rightarrow \beta$ 

 ### Obiettivo della grammatica
 generare parole di $V_T^*$ 
 - a partire dall'assioma
 - applicando una dopo l'altra le varie produzioni in $P$ 
### Alcune notazioni che ci servono per fare gli esercizi
Partiamo da un piccolo esempio 
se abbiamo $\alpha$ e $\beta$ che sono due parole ad esempio $\alpha=001$ e $\beta=abba$ la concatenazione $\alpha\beta$ sarà $001abba$ 
##### Notazione di derivazione e produzione
definisce una grammatica come prima ovvero
$G=<V_t,V_n,P,S>$
se abbiamo poi $x,y$ che sono $\in(V_T \cup \ V_N)^*$:  scriviamo $X \xRightarrow[G]{} Y$ , questo si dice che x se derivato porta a y nella grammatica G ad esempio se avviene ciò:
- $X = \alpha_1 a \alpha_2, \quad Y = \alpha_1 \beta \alpha_2 \text{ con } \alpha_1, \alpha, \alpha_2, \beta \in (V_T \cup V_N)^*$
- e ovviamente per avere in output y dobbiamo avere una produzione così
	- $\alpha\rightarrow \beta$
invece prendendo ciò che è stato detto prima in modo identico possiamo definire che con più proiezioni e quindi derivazioni possiamo raggiungere un risultato y
- se abbiamo  $x,y$  $\in(V_T \cup \ V_N)^*$:  scriviamo $X \xRightarrow[*]{G} Y$ , diciamo che y deriva da x se esiste una sequenza di parole $x_1,x_2,...x_n \in(V_T \cup V_N)$ tali che
$$X \xRightarrow[G]{} x_1 \xRightarrow[G]{} x_2 \xRightarrow[G]{} \cdots \xRightarrow[G]{} x_n \xRightarrow[G]{} Y$$
- una parola $y\in V_T^*$ si dice generata da G se  $S \xRightarrow[*]{G} Y$
piccole note: 
- per $(V_T \cup \ V_N)^*$ , si intende l'insieme di tutte le frasi di terminali e non
- una parola generata da G si dice <font color="#c0504d">forma di frase</font>
#### Definizione di linguaggio generato da G
Il linguaggio generato da G, che indichiamo con $L(G)$, è l’insieme delle parole generate da G, ossia
$$L(G) = \left\{ y \in V_T^* : S \xRightarrow[G]{*} Y \right\}$$
- notare che y è una parola che appartiene all'insieme di tutti i terminali quindi che sono nella grammatica
##### Ultime notazioni prima di fare 1000 esercizi
- Se due o più produzioni hanno la stessa parte sinistra esse si possono raggruppare mediante il simbolo | (da leggere come ‘‘oppure’’) 
	- ad esempio, le due produzioni $S → a$ e $S → b$ possono essere scritte nella forma S → a | b
- $\epsilon$ rappresenta la parola vuota (ossia, la parola che non contiene alcun carattere)
	- una produzione che porta a $\epsilon$ tipo $\alpha \rightarrow \epsilon$ si dice $\epsilon -produzione$
	- un linguaggio vuoto è segnato da questo simbolo : $\Lambda$ 
# Esercizi

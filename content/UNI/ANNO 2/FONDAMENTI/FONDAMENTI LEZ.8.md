## Concetto di Biezione
Dati due insiemi A e B, questi hanno $|A|$ = $|B|$ se $$\exists \ biezione \ \beta: A \rightarrow B$$ossia $$\forall a \in A, \ \exists! \ b \in B: b= \beta(a)$$$$\forall b \in B, \ \exists! \ a \in A: a = \beta(b)$$
## Infiniti
Cantor ha dimostrato che esistono infiniti più piccoli e infiniti più grandi.
Per esempio ha dimostrato che $|\mathbb{R}| > |\mathbb{N}|$.
![[Pasted image 20250321101628.png]]
Cantor ha dimostrato che non esiste una corrispondenza biunivoca di questo tipo nell'insieme ${0, 1}$.

![[Pasted image 20250321101647.png]]

>[!danger] I numeri NATURALI sono numerabili; i numeri REALI ***non*** sono numerabili.


## Problemi irrisolvibili
Turing ha dimostrato l'esistenza di un problema irrisolvibile, usando questo schema:
- si dimostra che le macchine di Turing sono tante quante i numeri naturali
- e, utilizzando questo conteggio, si dimostra che esiste almeno un linguaggio che NON è deciso da alcuna macchina e quindi esiste almeno un problema che NON può essere risolto con una macchina di Turing
	- quindi esistono più problemi dei numeri reali


#### Riprendiamo il concetto di parola codificata
![[Pasted image 20250321101726.png]]
![[Pasted image 20250321103355.png]]
Vogliamo trasformare tutto questo in un numero, dobbiamo quindi cambiare TUTTI i caratteri non codificati
![[Pasted image 20250321101736.png]]
Abbiamo quindi associato ad una macchina di Turing un numero naturale, e quindi ora ogni macchina di Turing sarà identificata con un numero differente dalle altre.

Quindi possiamo chiamare una macchina generica $$T_{h}$$e possiamo scrivere $$T_{h} < T_{k} \ \ se \ \ h<k$$In questo modo avremo una "prima" macchina, una "seconda" macchina e così via.

Allora
![[Pasted image 20250321101758.png]]

![[Pasted image 20250321101810.png]]
L'output sono le singole celle con 1 e 0.

$M$ rappresenta TUTTI i linguaggi ACCETTATI dalle Macchine di Turing 
	perché tutte le macchine di Turing sono rappresentate in M!

Ad esempio, gli 1 sulla riga uno rappresentano il linguaggio $L_{1}$ accettato da $T_{h_{1}}$, ossia $$L_{1} = \{x_{1}, x_{4}, ...\}$$
Prendiamo ora la diagonale (quella evidenziata in giallo).
Di per sè quella è un linguaggio $L$.
Ora scriviamo $\overline{L}$, ossia il complementare di $L$ e formalmente $$L = \{k : T_{h_{k}}(k) \ non \ accetta\}$$Questo vuol dire che il linguaggio $\overline{L}$ non è accettato da NESSUNA macchina di Turing che compare nella matrice e quindi non esiste nessuna $T$ che accetta $\overline{L}$.
	Qui l'idea è quella di prendere la diagonale, e scrivere in $\overline{L}$ tutte le celle hanno output 0 (quindi nella foto $\overline{L} = \{x_{2,}...\}$).
	Ora, do questo linguaggio a TUTTE le macchine (quindi tento di sovrascrivere $\overline{L}$ al posto delle singole righe). 
	Esiste una riga che è ESATTAMENTE IDENTICA a $\overline{L}$? NO, perché almeno un output (quello corrispondente alla diagonale in questo caso) sarà l'opposto rispetto alla matrice originale.
	Es. nella matrice originale $T_{h_2}(2)$ NON ACCETTA ma in $\overline{L}$ $T_{h_2}(2)$ è accettato: QUESTA COSA È IMPOSSIBILE.

QUINDI, $\overline{L}$ **è un linguaggio NON accettabile.**

>[!lemma] $|L| > |T|$ mentre $|L_{a}| = |T|$
>Questo perché se esiste un linguaggio accettabile, devo avere per forza una $T$ che lo accetta.

E quindi abbiamo dimostrato che esiste un problema che non può essere risolto con una macchina di Turing.

## Halting Problem
Turing considerò il seguente linguaggio:
![[Pasted image 20250321101838.png]]
chiamato **Halting Problem**.
Turing dimostrò che $L_{h}$ è accettabile MA non decidibile.
	il che vuol dire che $L_{h}^{c}$ NON È ACCETTABILE.


>[!lemma] TEOREMA: $L_{h}$ è accettabile

Costruisco una macchina $U'$ con input $(i,x)$ prendendo la macchina universale $U$ e facendo delle piccole modifiche.
	FASE 1) verifica se $i$ è la codifica di una macchina di Turing T
			se <u>NO</u>, rigetta
			altrimenti FASE 2
	FASE 2) simula $U(i,x)$
			se $o_{u}(i,x) \in \{q_{a}, q_{r}\} \Rightarrow$ ACCETTA
			altrimenti NON LO POSSIAMO SAPERE.

Quindi $U'(i,x)$ accetta TUTTE E SOLE le coppie $(i,x)$ che appartengono a $L_{h}$ - ossia $$L_{h} \ è \ accettabile$$

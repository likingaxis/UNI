
### ESERCIZIO 1
Si vuole inviare la seguente sequenza di bit proteggendola 
attraverso l'aggiunta di un bit di parità (pari), posto alla fine della 
sequenza.
``1101 1010 1001 0110``
Quali bit saranno effettivamente trasmessi?
- aggiungi bit parità alla fine
### ESERCIZIO 3
Si supponga di aver ricevuto il seguente frame protetto da singolo 
bit di parità (pari):
`1101 1010 1001 0110`
Rispondere alle seguenti domande:
1. Il ricevente rileva un errore?
2. In caso affermativo, il ricevente può correggere l'errore?
	- conta i bit 1 se sono dispari errore
	- non si può correggere perché il sistema di bit di parità non permette correzioni
### ESERCIZIO 4
Si considerino i dati forniti di seguito in formato binario
`1101 1010 1001 0110`
Si calcolino i bit di EDC (error detection and correction) secondo lo 
schema di controllo di parità (pari) bidimensionale.
Quali sono i bit EDC da aggiungere (fornire la soluzione minima)?
- dividi i bit 4 a 4 mettili in riga e colonna
- aggiungi bit di parità per ogni riga e colonna
	- aggiungi all'angolo il bit di parità globale che si trova vedendo il numero di 1 totali compresi i bit di parità
	- scrivi la soluzione prendendo bit di parità delle colonne e poi della riga e poi quello globale
### ESERCIZIO 5
Sono stati ricevuti i seguenti dati
`10110010 01101100 11001110`
I dati sono stati trasmessi in modo tale che:
• Il bit più significativo (il primo a sinistra) di ciascuno dei primi due byte è un 
bit di parità pari calcolato sui restanti 7 bit dello stesso byte.
• Il terzo byte contiene, in ciascuna posizione, la parità pari dei bit nella stessa 
posizione dei primi due byte
Rispondere alle seguenti domande:
1. Il ricevente rileva un errore?
2. In caso affermativo, può correggerlo?

- controlla gli 1 per vedere se ci sono errori
- per correggerlo prendi errori nelle righe e nella colonna e inverti il bit
- disponi prima i primi 8 bit su una riga e gli altri 8 bit in una seconda riga
- poi prendi i primi 2 bit come bit di parità della riga 
- usa il 3 byte come bit di parità della riga e quello globale a sx
![[Screenshot_2025-07-10-17-29-37-06_45415775811cea13943236d9369df411.jpg|400]]
### ESERCIZIO 6
Si considerino i dati forniti di seguito in formato binario
`1101 1010 1001 0110 1011 1100 0011 0101 1011 1100 0011 0101`
Si calcolino i bit di EDC (error detection and correction) secondo la 
checksum di Internet.
- prendi i primi 16 bit 
- prendi i secondi 16 bit
- sommali tra loro in colonna
- se alla fine hai un riporto di 1 sommalo a partire dai bit meno significativi e cancella il riporto
- poi somma al risultato i successivi 16 bit della fine
- compl a 1

![[Screenshot_2025-07-10-17-31-12-33_45415775811cea13943236d9369df411.jpg|400]]

### ESERCIZIO 6b
ricordati la conversione da esadecimale a decimale e poi da decimale a binario

| A   | 10  |
| --- | --- |
| B   | 11  |
| C   | 12  |
| D   | 13  |
| E   | 14  |
| F   | 15  |

### ESERCIZIO 7
Data la sequenza D di bit fornita di seguito in formato binario
`1101 1010 1001 0110`
Si calcolino i bit di EDC (error detection and correction) secondo lo 
schema di CRC usando il generatore CRC-8-CCITT (1 0000 0111).
Quali sono i bit EDC da aggiungere?
![[Pasted image 20250710180234.png]]
- aggiungo alla fine quanti zeri quanto il grado della CRC 
- inizio da sx a fare lo XOR con il generatore
	- ogni volta che ho uno o più 0 a sx procedo a portare giù le successive cifre da destra
	- se ho 2 0 a sx abbasso 2 a dx
- esercizio termina quando non ho più cifre da abbassare
- EDC=risultato dello XOR
- come verificare poi se il messaggio è arrivato correttamente
	- Prendi il messaggio ricevuto (dati + CRC)
	- Fai la divisione binaria con lo **stesso generatore**
	- Guarda il **resto finale**
    - Se è `00000000`, OK!
    - Altrimenti, errore
### ESERCIZIO 9
Un frame di $N$ bit viene trasmesso attraverso un collegamento 
soggetto a errori su bit indipendenti con probabilità $N$.
Qual è la probabilità che:
1. Il frame sia ricevuto senza errori
2. Il frame sia ricevuto con un errore
3. Il frame sia ricevuto con errori multipli (2 o più)
Applicare queste probabilità alla discussione dell'efficacia del bit di 
parità.
### 1. **Probabilità che il frame sia ricevuto senza errori**

$P(S = 0) = (1 - p)^N$
👉 Dipende fortemente da $N$ e $p$. Per $p \ll 1$ e $N$ piccolo, questa probabilità è **vicina a 1**.
### 2. **Probabilità che il frame sia ricevuto con esattamente un errore**

$P(S = 1) = \binom{N}{1} \cdot p \cdot (1 - p)^{N - 1} = Np(1 - p)^{N - 1}$
👉 Cresce linearmente con $N$, ma solo se $p$ è sufficientemente piccolo.
### 3. **Probabilità che il frame sia ricevuto con errori multipli (2 o più)**

$P(S \geq 2) = 1 - P(S = 0) - P(S = 1)$
👉 Questa è la parte più pericolosa per il bit di parità, come vediamo sotto.


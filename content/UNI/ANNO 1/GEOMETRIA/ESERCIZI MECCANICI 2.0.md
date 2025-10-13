## DETERMINATE 
- Assegna ad ogni elemento un + o un - partendo da + (segni della matrice degli sviluppi di Laplace)
- scegli la colonna o riga che più ti aggrada e escludi le rispettive righe e colonne associate a quella determinata posizione, per ognuna si calcola il $segno*numero*det(matrice formata)$
	- il $det$ si calcola facendo $ad-bc$ 
- sommi tutti i risultati assieme 
## VERIFICA SE INVERTIBILE
Due modi
1. fai il determinante e vedi se esce != 0
oppure
2. controlli se rango=max è invertibile
## Rango
- Gauss
- Controlli il numero di pivot != 0

## Matrice inversa
-  calcola il determinante della matrice 
- prendi i successivi cofattori della matrice (ogni singolo valore) e calcola il determinante SENZA CONTARE IL NUMERO STESSO
- scrivi la matrice risultante con tutti i $det$ e moltiplicala per $\frac 1 9$ 
- scrivi la matrice finale

## Gauss con sistemi lineari
- componi la matrice aumentata dei coefficienti 
	- si scrive mettendo $A|B$ dove 
		- $A$ sono i coefficienti delle varie incognite (prima dell'uguale)
		- $B$ sono i risultati
- applica Gauss 
- dopo Gauss puoi avere diversi casi
	- tutte le righe sono != 0 ->  sistema determinato dove puoi ricavarti i valori delle incognite (svolgi il sistema)
	- una o più righe sono interamente = 0 -> sistema indeterminato
	- una o più righe hanno $A = 0$ MA $B$ != $0$ -> sistema impossibile

## Rango nei sistemi lineari
- prendi la matrice applicata ai coefficienti e prendi anche quella aumentata con A|B
- applica Gauss e vedi le righe per definire il rango 
Diversi casi (Rouché-Capelli)
- Rango matrice = Rango matrice aumentata => sistema compatibile e hai almeno 1 soluzione
	- rango matrice = numero di incognite -> un'unica soluzione
	- rango matrice < numero di incognite ->  $\infty$ soluzioni
		- per incognite si intende le varie $x, y, z$  
- Rango matrice != Rango matrice aumentata -> non ci sono soluzioni ed è incompatibile, impossibile

## Vettori linearmente indipendenti 
Ci portano a capire la dimensione del sottospazio e la base del sottospazio vettoriale
- prendi gli elementi dei vettori e li scrivi sulla matrice come **righe**
- applichi Gauss
- il numero di pivot esprime la sua dimensione
	- se ad un pivot hai una funzione allora devi verificare quando essa è diversa da 0 
		- solo in quel caso vale come pivot altrimenti è 0 e non conta
- la base si scrive come un insieme di vettori delle singole righe post Gauss


# LIVELLO 2
## Polinomio caratteristico
aggiungi ai pivot $-\lambda$ 
- calcola il determinante
- otterrai una formula con le varie lambda quello è il polinomio caratteristico

## Autovalori e Autovettori
- Polinomio Caratteristico -> risolvi l'equazione del polinomio risultante
	- i risultati sono gli autovalori 
- sostituisci ogni autovalore alla matrice con i -$\lambda$, la moltiplichi con un vettore $(x1,x2,x3)$ e scrivi un sistema ponendo tutto a 0
- risolvi il sistema con Gauss e poi lo rimetti su un sistema 
RISULTATO -> $v=(x1,x2,x3)$ con i valori sostituiti

## Diagonizzabile
- Trova gli autovalori e calcoli quante volte appaiono (*molteplicità algebrica*) 
- calcoli rango per ogni autovalore trovando la *molteplicità geometrica* data da $$numero \ colonne-rango$$
- se $\forall$ autovalore $ma=mg$ è diagonizzabile

## Base nucleo(ker) 
NON CONFONDERE CON LA DIMENSIONE
- prendi la matrice e fai GAUSS 
- metti a sistema le varie righe e eventualmente definisci dei parametri liberi per risolvere il sistema
- per ogni parametro definiamo i vettori (compreso il parametro dei termini noti)
RISULTATO => $ker(MATRICE) = span${METTI I VETTORI SENZA PARAMETRI}

## Base immagine
DA NON CONFONDERE CON LA DIMENSIONE
- fai GAUSS e prendi tutte le colonne **linearmente indipendenti** (con pivot diversi da zero) 
- scrivi i vettori prendendo le colonne della matrice ORIGINALE associate alle colonne linearmente indipendenti 

## Dimensione nucleo (Null)
- dopo aver calcolato la base, calcoli la cardinalità dell'insieme dello $span$

## Dimensione immagine
- letteralmente il rango

## Matrice associata
INGREDIENTI:
- Matrice
- Base, con i vari vettori
- Formula

RISOLUZIONE
- definiamo una N come a1b1+a2b2+a3b3...
- calcoliamo la formula con A e ogni base (*poi dipende dalla formula ovviamente*)
- prendiamo i risultati e li mettiamo come coefficienti di N per ogni base
RISULTATO => la matrice risultante avrà come COLONNE i vari vettori trovati

# LIVELLO 3
## Trovare equazione parametrica
Due casi da cui partire
#### CASO 1: equazione cartesiana
- prendi il sistema 
- effettui delle sostituzioni definendo un parametro libero
RISULTATO => finito il sistema avrai la tua equazione parametrica (ossia con il parametro libero)
#### CASO 2: partendo da punti
Possiamo o inventarli o li dà il prof
- una volta ottenuti facciamo $P1-P0$ per ottenere il vettore direttore
- una volta ottenuto scriviamo la formula generale della equazione mettendo la prima colonna con i valori di P0 la seconda con $t$ moltiplicato per il vettore direttore
	- SISTEMA:
$$ \begin{cases} x = x_0+t v_0 \\ y = y_0+t v_1 \\ z = z_0+t v_2 \end{cases} $$
### Per il piano
- Se i punti non li da lui dobbiamo trovarli noi sostituendo $x,y \ o \ z$ (ne sostituisci al massimo due) all'equazione cartesiana per trovare le varie P
- troviamo 2 vettori direttori facendo $P1-P0$ e $P2-P0$
- Li sostituiamo alla formula generale dell'equazione parametrica che è IDENTICA alla retta ma con un vettore e un parametro in più.

***N.B.:*** se un piano è **parallelo** a delle rette userà gli stessi vettori direttori delle rete

# Equazione cartesiana
Se hai la parametrica
- trovati le equazioni per i parametri
- sostituiscili in una riga e ponila $= 0$
RISULTATO => la riga senza parametri sarà l'equazione cartesiana

## Intersezione tra retta e piano
INGREDIENTI:
- equazione CARTESIANA del PIANO
- equazione PARAMETRICA della RETTA

SVOLGIMENTO:
- al posto di $x, y, z$ dell'equazione CARTESIANA del PIANO sostituiamo i valori dell'equazione PARAMETRICA della retta
- svolgiamo l'equazione per trovare $t$ 
- sostituiamo $t$ all'equazione PARAMETRICA della RETTA per trovare i valori effettivi di $x, y, z$
RIAULTATO => metti queste coordinate in un vettore

## Rette parallele coincidenti incidenti sghembe  
#### parallele 
- prendi i vettori direttori delle rette e controlli se hanno dei multipli in comune
#### coincidenti
PUOI CALCOLARLO **SE E SOLO SE** SONO PARALLELE
- prendi una delle due equazioni parametriche
- scegli una riga (*es. quella di x*) e mettila uguale al termine noto della stessa riga nell'altra equazione parametrica per trovare il $t$ 
- una volta trovato, sostituisco il $t$ alle altre righe dell'equazione parametrica 
RISULTATO => se i risultati delle altre due coordinate (*in questo caso* $y, z$) sono UGUALI al punto di partenza delle altre (*prima colonna nell'altra eq. parametrica*) -> SONO COINCIDENTI
#### incidenti
PUOI CALCOLARLO SE NON SONO PARALLELE
- prendi le due equazioni parametriche le metti uguali in un unico sistema
RISULTATO => se il sistema ha soluzioni -> SONO INCIDENTI
#### sghembe
SE NON SONO NULLA -> SONO SGHEMBE

# Funzioni Suriettive, Iniettive, Biunivoche
### SURIETTIVA
$$R(A) = R(A|b)$$
### INIETTIVA
$$R(A) = numero \ colonne$$
### BIUNIVOCA
$$\text{SURIETTIVA + BIUNIVOCA}$$
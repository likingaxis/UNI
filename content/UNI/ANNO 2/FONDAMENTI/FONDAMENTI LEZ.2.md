# Di cosa ha bisogno la nostra macchina
-  I caratteri da scrivere sui nastri è dato da $\Sigma$ che rappresenta un <font color="#f79646">insieme di caratteri</font>
- Necessita gli <font color="#f79646">stati interni</font> definiti da un insieme $Q$ 
- gli <font color="#f79646">stati iniziali e finiti</font> con $q_0$ e $q_f$
- $q_0 \in Q$ e $Q_f$  un insieme di stati finali che è $\subseteq Q$ 
- l'insieme delle quintuple $P$ (le istruzioni) P $\subseteq$  $Q$ x $\Sigma$ $\cup$ ${\square}$ x $\Sigma$ $\cup$ $\square$ x $Q$ x $\{S,F,D\}$
$\Sigma$ P e Q sono insiemi con cardinalità costante 
## una macchina di Turing è definita da
$⟨Σ,Q,q_0​,Q_F​,P⟩$  che sono tutti gli insiemi citati prima
#### Facciamo un esempio per definire una possibile incorrettezza
sia $Q=\{q_0,q_1,q_2\}$ e $\Sigma=\{0,1\}$
se abbiamo $<q_0,0,0,q_1,D>$ $<q_0,0,1,q_1,D>$
le due quintuple sono distinte quindi non possono essere $\subseteq$ in P
perché hanno stessa condizione ma azione diversa

Quindi è sufficiente scrivere tale che non esistono due coppie che hanno stessa condizione e diversa azione
## Definizione di funzione di Transizione
la definizione che indica come una funzione deve essere definita
$\sigma$ : $Q$ x $\Sigma$->$\Sigma$ x $Q$ x $\{S,F,D\}$
ciò indica che abbiamo
- uno <font color="#f79646">stato iniziale</font> insieme di $Q$
- un <font color="#f79646">dato di ricevuta</font> iniziale insieme di $\Sigma$
che ci porta ad avere una azione con
- un <font color="#f79646">dato in scrittura</font> insieme di $\Sigma$
- uno <font color="#f79646">stato aggiornato</font> che verrà eseguito al <font color="#f79646">prossimo step</font>
- uno <font color="#f79646">spostamento</font> della <font color="#f79646">testina</font> da qualche parte o un fermo

### quando può terminare?
La macchina può terminare se <font color="#f79646">non ha quintuple</font> da eseguire oppure se <font color="#f79646">deve terminare</font> a prescindere

# ESEMPIO
Data una parola binaria con una sola x progettare una macchina a un solo nastro che analizza e cancella via via i valori sul nastro
- termina nello stato $q_f$ se x contiene un numero pari di 1 e scrive P sul nastro
- termina in $q_f$ se x contiene un numero dispari di 1 e scrive D sul nastro
![[Screenshot_2025-03-06-19-29-04-36_45415775811cea13943236d9369df411.jpg|400]]
![[Pasted image 20250306193134.png|600]]
# ESERCIZIO
Progettare una macchina di Turing a due nastri che, avendo sul primo nastro due numeri interi della stessa lunghezza, calcola il valore della loro somma scrivendo il risultato sul secondo nastro – ossia, si richiede di progettare una macchina di Turing che esegua la somma “in riga” di due numeri
![[Pasted image 20251015120203.png]]

![[Screenshot_2025-03-06-20-23-20-26_45415775811cea13943236d9369df411.jpg|600]]

# Una serie di definizioni
$\Sigma ^*$ sono tutte le parole dell'alfabeto, tutte le sequenze di caratteri combinate tra loro
![[Pasted image 20251015121442.png]]

# Stato globale
È una "fotografia" della macchina a un certo istante
lo stato globale rappresenta lo stato interno della macchina:
- il contenuto del nastro
	- tutti i vari caratteri non blank $\square$
- la posizione della testina
![[Pasted image 20250306210339.png|300]]
Ecco come si scrive lo stato globale ad esempio di questo:
è sostanzialmente una parola dove rappresenta lo stato attuale di una macchina con il testo del nastro
ecco due esempi:
![[Pasted image 20250306210439.png]]
<font color="#c0504d">lo Stato è iniziale quando siamo su q0 a b c d</font>
<font color="#c0504d">si dice finale quando abbiamo qf</font>
# transizione
avviene tra due stati globali
SG1->SG2 
SG1 non deve essere uno stato globale finale
È il passaggio tra uno stato globale a un altro tramite l'esecuzione di una quintupla
![[Pasted image 20250306210934.png]]
# computazione
Esecuzione della macchina di Turing applicata a un input
SG0 ->Sg1->SG2->($SG_f$ oppure errore e termina in uno stato non definito)
anche un loop infinito dato da $<q,a,a,q,f>$ ad esempio
sono una serie di transizioni 
possiamo dire quindi che formalmente una computazione è una sequenza di transizioni di vari stati Globali partendo da un SG0 con stato interno $q_0$ 
se esiste una h tale che un SGh non ha transizioni allora significa che è uno stato di terminazione
mentre invece tutti gli altri che hanno transizioni sono definite tra 0 e h-1
![[Pasted image 20250306211435.png]]
# 2 tipi di macchine di Turing
# Trasduttori
Calcolano il valore di una funzione e la scrivono su nastro
- dispongono di un nastro di output(serve solo per il risultato)
- hanno un solo stato finale $Q_f$
# Riconoscitori
- calcolano solo funzioni booleane$(0,1)$ $(V,F)$ $(S,N)$...
- non hanno un nastro di output, il risultato lo danno nello stato finale $Q_f$ 
	- vero falso ecc...
un esempio è la macchina $T_{parità}$
Gli stati riconoscitori
$Q_a$ e $Q_r$ 
- accettazione
- rigetto


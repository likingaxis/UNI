# Cosa è una macchina di Turing
$T=<\Sigma,Q,q0,Qf,P>$
caratterizzata principalmente dagli ultimi 3
Al livello più teorico possiamo dire che è la descrizione di un procedimento per risolvere un problema descritto con le quintuple
#### Definiamo una macchina T
che ha come parola ovvero l'input dato i vari stati separati da un - e tutte le varie quintuple una di seguito all'altra
questa parola in input definisce completamente una macchina T
- con i vari stati e parole
![[Pasted image 20250315111106.png]]
L'insieme delle quintuple non è una funzione totale poiché manca il caso in cui la lunghezza è dispari e la parola è palindroma
si possono aggiungere queste quintuple 
〈qa1 , ◻, ◻, qR , F〉,〈 qb1 , ◻, ◻, qR , F〉
ma comunque manca il caso in cui una parola è dispari ma palindroma 
Ci torneremo poi
![[Pasted image 20250315111629.png]]
#### Macchina di Turing presa come parola
quindi possiamo definire una vera e propria macchina di Turing come se fosse una parola completa costituita da
$Q \cup \Sigma \cup \{-\} \cup \{ \langle \} \cup \{ \rangle \} \cup \{ \square \}$
facendo ciò possiamo ottenere una macchina che simula un'altra macchina che lavora data la macchina dall'input delle parole
# Cosa succede se progettassimo una macchina Universale
$U(T,x)$ 
possiamo fare in modo che $o_u(T,x)=o_t(x)$
U cosa deve fare per simulare ciò che fa T?
1) Al primo nastro metto tutti gli stati e le quintuple di T 
2) Al secondo l'input effettivo
3) Sul terzo nastro U copia lo stato iniziale di T (primo simbolo di $p_t$)
4) Sul quarto nastro U copia lo stato di accettazione di T dopo il primo simbolo dopo il -
![[Pasted image 20250315113137.png]]
$N_3$ non cambierà mai 
$N_4$ contiene lo stato attuale della macchina di T (non U)
#### U ripeterà i seguenti passaggi
- Fase 1) Cerca la quintupla da eseguire
- Fase 2) Se abbiamo trovato la quintupla la eseguiamo e torniamo a Fase 1
- Fase 3) Se non troviamo la quintupla(lo capiamo se abbiamo 
  ( $\rangle \ poi \square$) confronta così il terzo nastro con il 4 se sono uguali accetta altrimenti rigetta
### Prime due fasi nel dettaglio
##### FASE 1
![[Pasted image 20250315114838.png]]
##### FASE 2
![[Pasted image 20250315114847.png]]

### Definire correttamente l'alfabeto
>[!bug] Problema:
>  l'alfabeto deve essere finito e quindi lo codifichiamo in binario per renderlo finito

![[Pasted image 20250315115409.png]]
![[Pasted image 20250315115422.png]]
Ovviamente ciò cambia un po di cose ma solo in termini di lettura tutto qui
ovvero verranno lette sequenze di bit e non più lettere dell'alfabeto

>[!question]- e se, putacaso, la parola scritta sul primo nastro di U non corrisponde alla descrizione di una macchina di Turing?
>Abbiamo due possibilità:
>- prima di computare e scrivere il tutto la macchina U controlla se sono state rispettate le specifiche descritte che definiscono una macchina di Turing
>- sono cavoli di chi sbaglia

### La prof alla fine
alla fine del pdf la prof descrive un metodo con accesso diretto per i nastri con le varie posizioni

# Esercizio lezione di ieri

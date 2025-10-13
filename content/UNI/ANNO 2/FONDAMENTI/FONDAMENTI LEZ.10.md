## Un modello realistico
È definito da istruzioni input e output FINITI *definito* da Turing
possiamo definire che per ogni modello di calcolo realistico $M$ 
- $M$ è Turing equivalente
ossia L è decidibile\accettabile nel <font color="#00b0f0">modello M</font> <--> L è decidibile\accettabile nel <font color="#00b0f0">modello Macchina di Turing </font>

si può trovare una definizione simile con
un linguaggio L è accettabile oppure decidibile se e solo se è accettabile o decidibile per la macchina Macchina di Turing

### La tesi di Church-Turing
Sostiene che non esiste un modello di calcolo più potente della Macchina di Turing
dando la definizione precedente
inoltre $M$ deve essere un modello "ragionevole"
- ovvero basato sul concetto di operazione elementare
È una tesi e non un Teorema
#### In sostanza dice
<font color="#c0504d">è calcolabile tutto e solo ciò che può essere calcolato dalla Macchina di Turing</font>
## Modello di calcolo
ogni linguaggio di programmazione rappresenta un modello di calcolo
#### Esempio di Pascal minimo 
linguaggio inventato da lei con meno cose basato su Pascal

cosa abbiamo:
- variabile(semplice)
- variabili(strutturate)
	- array
	- insiemi(set)
		- sono tipo array
- costanti
che istruzioni abbiamo?
- assegnazione a<-b;
- istruzioni condizionali: 
``` pascal
if (condizione) then
	istruzione 1;
	............;
	istruzione h;
end; // lo uso per "skippare" l'if se non si verifica
else begin
	.....;
end;
```

- istruzioni di loop:
```pascal
while (condizione) do begin
	......;
end;
```

- `return`

### Vogliamo dimostrare che questo modello di calcolo è Turing equivalente
In particolare, viene mostriamo come “trasformare” un programma in PascalMinimo in una macchina di Turing di tipo trasduttore

abbiamo una macchina $P \ in \ PM \rightarrow T \in \tau$
andiamo a trasformare le istruzioni che non ci piacciono per far si che ci piacciano sulla Macchina di Turing quindi andiamo a:

1) Eliminare array dalle condizioni
Se abbiamo l'istruzione
```pascal
if (A[j] = 0) then
```
La facciamo diventare
```pascal
ausilA <- A[j];
if (ausilA = 0) then
```


### Codice effettivo
Scriviamo una sola istruzione in ciascuna riga del programma e numeriamo le righe
Questo codice
```pascal
input: array A di n elementi interi; intero k;

p ← 1; i ← 1;

while (i ≤ n) do
	if (A[i] > p) then 
		p ← A[i];
end;

if (p > k) then 
	ris ← k;
else
	ris ← p;

output ris;
```

Ora andiamo a precisare le righe di codice e a modificare tutte quelle istruzioni per far si che siano adatte alla macchina di Turing
```pascal
1) p ← 1; 
2) i ← 1;

3) while (i ≤ n) do
4)   ausilA ← A[i];
5)   if (ausilA > p) then
6)     p ← A[i];
7)   i ← i+1;
   end;   // qui possono non mettere numeri (sotto capirai perché)

8) if (p > k) then
9)    ris ← k;
10) else ris ← p;  // gli else credo di poterli scrivere su una sola riga
11) output ris;
```
OGNI RIGA È UNO STATO DIFFERENTE

### andiamo a creare un trasduttore che lo replichi
##### Definiamo i Nastri 
ovviamente potremmo usarne solo 1 ma ciò complicherebbe le cose in modo assurdo
##### Generalmente
Un trasduttore GENERALE per un problema in PascalMinimo usa:
- nastro di input
- nastro di output
- un nastro per ogni variabile di tipo array sul quale memorizzare, in unario, l'indice dell'array al quale voglio accedere (nella foto sotto quello con tutti "$1$")
	- per separare i vari elementi dell'array uso un carattere speciale `$`
### In questo caso
AVRÒ 8 NASTRI
- 5 nastri per le variabili semplici
	- $N_{p}$ per p
	- $N_{i}$ per i
	- $N_{ausilA}$ per $ausilA$
	- $N_{k}$ per k
	- $N_{ris}$ per $ris$
- 1 nastro $N_{A}$ per la variabile di tipo array
- 1 nastro per $N_{indA}$ per l'indice con il quale accedere all'array
- 1 nastro di lavoro

in questo esempio per l'array usa i dollari invece nei lucidi prende per scontato che sia tutto su una cella
### Descrizione quintuple ad alto livello
queste sono meta quintuple ovvero una serie di quintuple ma che si racchiudono in una sola quintupla intuitiva e semplice che ha al suo interno
- lo stato attuale
- l'azione da svolgere ad alto livello
- lo stato successivo
- le testine saranno su fermo perché prendiamo per scontato che si sia già mosso tutto nel mentre
praticamente non conto le quintuple intermedie

![[Pasted image 20250326203305.png]]

### Conversioni di Quintuple effettive
andiamo a creare delle quintuple che passano da stato in stato seguendo un classico esecutore di codici
quindi partiamo dallo stato $q1$ per poi andare nello stato successivo $q_{i+1}$ 

### Quintupla di assegnazione
![[Pasted image 20250326203641.png]]

#### Assegnazione con Array
Se la riga contiene un'***istruzione di assegnazione che coinvolte una variabile A di tipo array***
1) viene copiato su $N_{indA}$ in unario il valore dell'indice dell'elemento A cui si vuole accedere (la foto di prima con tutti "$1$")
2) ci si posiziona sull'elemento nel nastro contenente $A$ (cosa che ti ho spiegato prima)
3) si esegue l'assegnazione dopo la quale $T$ entra nello stato $q_{i+1}$
	
![[Pasted image 20250326203708.png]]


### Quintupla di condizione if then
Quando la riga contiene un'istruzione `If (condizione) then...`, viene calcolata la condizione
1) se è vera allora $T$ entra nello stato $q_{i+1}$, 
2) altrimenti entra nello stato dell'istruzione da eseguire quando è falsa
	
![[Pasted image 20250326203801.png]]

### Quintupla con ciclo loop while 
Quando la riga contiene un'istruzione `While (condizione) do...`, viene calcolata la condizione
1) se è vera $T$ entra nello stato $q_{i+1}$ e poi di seguito fino all'ultima istruzione del loop per poi rientrare in $q_i$ (in pratica una volta finito il loop ritorno nello stato iniziale del loop e quindi al punto `1)`)
2) altrimenti entra nello stato corrispondente allo stato dell'istruzione da eseguire dopo il loop
![[Pasted image 20250326203816.png]]

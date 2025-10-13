# problemi risolti automaticamente
>[!question]- Cos'è un problema?
>È la descrizione di un insieme di oggetti chiamati dati, ognuno di questi dati è collegato da un insieme di relazioni, derivati da essi abbiamo l'insieme di oggetti soluzioni 
>perciò avremmo:
>- Oggetti di partenza: dati
>-Oggetti a cui dobbiamo arrivare: soluzione

### Esempio di problema:
<font color="#f79646">Somma</font>: dati due interi $n$ e $k$ trovare un terzo intero $s$ tale che $s=n+k$
trovare la somma di $3+2$ è una <font color="#f79646">istanza del problema</font> 
Infatti possiamo dire che il problema <font color="#f79646">Somma</font> con i vari dati e oggetti la coppia $(3,2)$ è una istanza del problema Somma
## Risolvere un problema
Risolvere un problema si tratta di trovare un metodo che sia in grado di risolvere qualunque istanza del problema ma
Esistono istanze 
- facili
	- 2+2
- difficili
	- quando ad esempio non bastano le dita
- impossibili
	- tipo $\sqrt{-1}$ 
Risolvere autonomamente un problema attraverso un metodo che sia
- diviso in passi elementari e finiti
- che portano alla soluzione
chiunque può avere la sua soluzione elementare poiché dipende dal soggetto(se sei un matematico un passo elementare è anche fare un integrale triplo)
È <font color="#f79646">necessario</font> quindi definire un <font color="#f79646">procedimento</font> che data una qualunque istanza del problema sia in grado <font color="#f79646">mediante azioni </font>di <font color="#f79646">trovare</font> la <font color="#f79646">soluzione</font> di quell'istanza
>[!question]- cosa si intende per procedimento?
>È la descrizione di un insieme di azioni unita alla specifica dell'ordine di svolgimento di quest'ultime
>- ricorda che le azioni devono essere semplici definite e elementari
#### Standard di istruzioni per Turing
1) una istruzione è elementare se la scelgo in un insieme di esse di piccole dimensioni
2) l'istruzione deve scegliere poche soluzioni possibili
3) Ogni istruzione deve poter essere eseguita utilizzando quantità di memoria limitata
![[Pasted image 20250305164259.png]]
###### Cosa significa <font color="#f79646">poco</font>?
significa che deve essere <font color="#f79646">costante</font> <font color="#f79646">indipendentemente</font> dall'istanza e <font color="#f79646">dall'input</font>
Data una istruzione essa sarà composta da 
- una sola condizione
- una sola azione
L'insegnante fa un esempio sulla somma dei numeri e ci mostra come per farla abbiamo bisogno di passi elementari definiti e generici che ci portano a questo
![[Pasted image 20250305162142.png|600]]
![[Pasted image 20250305162208.png|600]]
![[Pasted image 20250305162435.png|500]]

In questo <font color="#f79646">esempio</font> è necessario <font color="#f79646">rispettare</font> caratteristiche come leggere scrivere e interpretare
indipendentemente da quanto siano grandi i numeri dobbiamo effettuare una somma dovuto al confronto in una tabella $10*10$ e eventualmente sommare un resto quindi avremo $10*10*2$ e per sommare abbiamo bisogno di ricordare 3 cose, numero1 numero2 e il resto
### il tutto si può ricondurre in
se sono vere <font color="#548dd4">certe condizioni</font> allora esegui queste<font color="#92d050"> azioni</font>
#### Risolvere un problema in modo autonomo
Quando abbiamo una soluzione per ogni istanza del problema attraverso un procedimento che può essere eseguito da un automa
- qualcuno in grado di risolvere il procedimento senza sapere tutto del problema
possiamo quindi eseguire queste istruzioni per ottenere un risultato in modo autonomo
per scrivere Meno posso dividere in stati una istruzione con $q0$ e $q1$ che indicano resto $0$ e $1$
quindi se ho
Se $r=0$ e leggo....
avrò $<q_0,(9,5),4,q_1,Sinistra>$
abbiamo 2 condizioni e 3 istruzioni quindi si definisce una <font color="#f79646">QUINTUPLA</font>
non è proprio una macchina di Turing perché non stiamo specificando cosa fare ad ogni passaggio per ogni rispettivo nastro
## Macchina di Turing 
ho $3$ nastri che scorrono all'infinito con delle celle alcune vuote alcune piene
Le frecce indicano testine di lettura e scrittura
![[Pasted image 20250305163912.png]]
avremo quindi definite le varie istruzioni per Turing con $<q_0,(9,5,[]),(9,5,4),q_1,(S,S,S)>$
Le varie q si chiamano <font color="#f79646">stati interni</font>
le prime $2$ sono di lettura le ultime 3 di scrittura 
$S,S,S$ sta per sinistra sinistra sinistra per ogni nastro
L'<font color="#f79646">esecuzione </font>di queste <font color="#f79646">quintuple</font> si chiama <font color="#f79646">computazione</font>
le macchine singole si chiamano con $T_{nomeoperazione}$
scritte in linguaggio <font color="#92d050">M</font><font color="#4bacc6">acchina</font> e vengono eseguite da <font color="#92d050">m</font><font color="#4bacc6">acchine </font>
ricapitolando:
<font color="#92d050">m</font><font color="#4bacc6">acchina: ESECUTORE</font>
<font color="#92d050">M</font><font color="#4bacc6">acchina: LINGUAGGIO DEI PROCEDIMENTI</font>
## Quali problemi possiamo risolvere con questo sistema?
lo vedremo al corso
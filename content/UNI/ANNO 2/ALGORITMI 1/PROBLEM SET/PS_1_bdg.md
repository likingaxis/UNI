# MEMBRI DEL GRUPPO

| Nome    | Cognome   | Matricola | Email universitaria                   |
| ------- | --------- | --------- | ------------------------------------- |
| Valerio | Bernardi  | 0349538   | valerio.bernardi@students.uniroma2.eu |
| Samuele | De Santis | 0348324   | samuele.desantis@students.uniroma2.eu |
| Luca    | Gugliotta | 0342634   | luca.gugliotta@students.uniroma2.eu   |

# Problema 1
#### PSEUDOCODICE
```python
BILANCIATO(Sequenza S)
    countAperto=0;
    countChiuso=0;
    n = lunghezza di S;
    
    if(n è dispari) then return +inf;
    
    
    for(i=1 to n) do
        if(S[i] == ")") then
            if(countAperto > 0) then countAperto--;
                
            else countChiuso++;
            
        else countAperto++;
    
    if(countAperto != countChiuso) then return +inf
        
    else return (countAperto + countChiuso)//2; 
       
```

#### LEGENDA VARIABILI

| nomeVariabile | descrizione                       |
| ------------- | --------------------------------- |
| countAperto   | Contatore per le parentesi aperte |
| countChiuso   | Contatore per le parentesi chiuse |
| n             | Lunghezza Sequenza S              |
| S             | Sequenza di parentesi             |

#### COSTO
$O(n)$ scorrendo tutta la sequenza $1$ volta con il ciclo for
#### CORRETTEZZA
- L'algoritmo rispetta i Costi di esecuzione richiesti
Prima di iniziare la spiegazione dell'algoritmo, introduciamo una ipotesi per la risoluzione del seguente problema: possiamo dire che se il numero di parentesi chiuse e aperte è diverso non è possibile effettuare un bilanciamento, dato che le parentesi vanno inserite a coppie.

Verificherà se la lunghezza della sequenza S è dispari, poiché se così fosse, il numero di parentesi aperte sarà sempre diverso dal numero di parentesi chiuse e rientrebbe nell'ipotesi.

Scorre la sequenza con un ciclo for, per tenere conto delle parentesi rimanenti da bilanciare e "scartare" quelle già bilanciate.
- Il numero di parentesi aperte viene decrementato ogni volta che si incontra una parentesi che la chiude
- Qualora questo caso non si verificasse, entrambi i contatori verrebbero incrementati ad ogni occorrenza di una o dell'altra
Terminato il ciclo, andrà a verificare una eventuale disparità tra parentesi aperte e chiuse, che non consentirebbe il corretto bilanciamento. 
In caso contrario andrà a effettuare un return con il numero di bilanciamenti necessari, dato dal numero di parentesi aperte o chiuse rimanenti.

---
# Problema 2: Il posto fisso
#### PSEUDOCODICE
``` python
TOPLAVORO(Lista S, n, M):
    DeltaP = M - S[n];
    k=0;
    count=1;
    
    if (M==n) then return -1;
    
    for(i=n-1 to 1):
        count++;
        if (DeltaP == 1) then
            return 1;
			
        k=DeltaP*count;
        if ((M-k-S[i])<0) then
            DeltaP--;
			
    return DeltaP;

```

#### LEGENDA VARIABILI

| nomeVariabile | descrizione                                                                         |
| ------------- | ----------------------------------------------------------------------------------- |
| DeltaP        | Rappresenta la variabile $\Delta'$                                                  |
| k             | Variabile che ci consente di verificare se quel determinato $\Delta'$ è sostenibile |
| count         | Numero di lavori soddisfatti                                                        |
| M             | Orario di fine giornata                                                             |
| n             | Numero di lavori                                                                    |
| S             | Lista dei lavori nei rispettivi istanti di tempo $t_i$                              |


#### COSTO
$O(n)$ scorrendo tutta la sequenza $n-1$ volte con il ciclo for. 
$O(n)=o(nM)$ poiché $T_n < M$

#### CORRETTEZZA
- L'algoritmo rispetta i Costi di esecuzione richiesti
Sappiamo a priori l'ordine di arrivo dei clienti, il quale viene espresso con istanti di tempo interi $T_i$
L'algoritmo inizialmente deve assumere come $\Delta'$ massimo la distanza tra il tempo di arrivo dell'ultimo cliente $T_n$ e il tempo di chiusura $M$
Successivamente controlliamo a ritroso il tempo di arrivo dei clienti precedenti, correggendo ogni volta il $\Delta'$ (Se necessario), andando a verificare se il $\Delta'$ precedente, applicato per tutti i clienti controllati fino ad ora ($k$), eccede l'orario lavorativo $M$: per capirlo effettuiamo una differenza tra $M-k-S[i]$
Se si incorre in tale condizione, decrementiamo il valore di $\Delta'$
- Sappiamo che il tempo $\Delta$ rappresenta $1$ e $\Delta'\geq \Delta$
È corretto perché tiene conto di tutti i clienti serviti prima dell' $i-esimo$ cliente ed effettua un ricalcolo del tempo lavorativo impiegato fino a quel momento rispetto ai limiti imposti dalla giornata lavorativa

---
# Problema 3 (Algo Run)

Per il seguente problema, non siamo riusciti a giungere ad una conclusione che rispetti i costi temporali richiesti.
Ci terremo comunque a presentare una nostra idea :
- La nostra soluzione doveva sfruttare un AVL
- Il problema c'è stato nella costruzione dello stesso
##### Tentativo AVL per valori
l'idea era di prendere l'AVL ordinato per valori
- Prendere ogni volta il valore massimo effettuando un max con il costo di $log(n)$
- Tenere conto delle monete raccolte per ogni valore massimo preso, fino al raggiungimento della fine corsa
	- Per contare le monete raccolte volevamo sfruttare il valore della singola tupla moltiplicato per il suo intervallo dato da $(fine-inizio+1)*valore \ moneta$
- Una volta preso l'intervallo max si andavano a decrementare il secondo campo satellite (di fine sequenza) di tutti i nodi che rientravano nel suo stesso intervallo
- Una volta raggiunta la somma finale di tutti gli intervalli, quindi giunti a fine corsa, si sarebbe effettuato un return della somma totale delle monete

![[Pasted image 20241213225922.png]]






[[Cap1.5.pdf|PDF rispettivo della lezione]]
## Introduzione
Ci sono vari tipi di modelli di calcolo come la macchina di Turing ma è troppo vecchia per usarla nel corso

Vedremo invece una RAM, macchina a registri come modello di calcolo che è una astrazione della macchina di Von Neumann

![[Pasted image 20241015192441.jpg|500]]
- Ognuna di queste risorse della RAM viene usata per svolgere le istruzioni del programma finito 
### ANALISI DI UN ALGORITMO
Si basa su un concetto di passo elementare ad esempio(nella RAM):
- accesso ai nastri I/O
- operazione aritmetico/logica
- accesso/modifica in memoria

##### Quanto costa un passo elementare
>[!info]- Criterio di costo Uniforme
>- In questo caso tutte le operazioni hanno lo stesso costo definito
>- La complessità temporale viene calcolata in base al numero di passi

>[!info]- Criterio di costo Logaritmico
>- Il costo di una singola operazione è in base alla dimensione degli operandi dell'istruzione
>- Un'operazione su un operando di valore $x$ avrà costo $logx$ 
>- Si usa principalmente in algoritmi numerici per calcolare meglio la loro complessità
 
Nel corso di algoritmi per quasi tutti i problemi il modo 1 dovrebbe essere più usato del modo 2 giusto con Fibonacci viene usato 2
**Quindi useremo principalmente modello RAM con costo uniforme**
## Caso peggiore e Caso medio
Il tempo di esecuzione di un algoritmo viene calcolato in base alla dimensione delle istanze dell'algoritmo Che però possono avere dimensione variabile e potrebbero richiedere tempo diverso quindi differenziato due modi per calcolare il tempo di esecuzione
#### Nel caso peggiore
Prendiamo Tempo(I) come tempo di esecuzione su una Istanza I allora il caso peggiore sarà:
Il massimo dell'insieme di tutti i tempi delle istanze I, ovviamente parlando di istanze con dimensione n non potremmo avere un numero definito.
$$T_{worst}(n)=max_{istanze \ I \ di \ dimensione \  n} \ \{Tempo(I)\}$$
$T_{worst}$ sarà una garanzia sul tempo di esecuzione e indicherà il massimo sforzo che dovrà fare la macchina per eseguire l'algoritmo
#### Nel caso medio
Nel caso medio si calcola la probabilità del tempo di esecuzione delle istanze
$T_{avg}n=\sum_{istanze \ I \ di \ dimensione \ n} \{P(I)tempo(I)\}$
Ovviamente parlando di caso medio si può dedurre come si tratti dei casi tipici degli input n 
Come capiamo la distribuzione di probabilità sulle istanze?
- Di solito non la conosciamo quindi facciamo delle assunzioni
### ==Esercizio per casa==
La somma di n frazioni 1/n+1/n...n
## Notazione asintotica
Complessità computazionale di un algoritmo espressa con T(n) in modo qualitativo quindi
Ignoro 
- costanti
- ordini inferiori

>[!info]
> Il prof intende $log$ come $log_2$

$T(n)$ è il numero di passi elementari eseguiti su una RAM nel caso peggiore su una Istanza di dimensioni n
### ESEMPIO DI NOTAZIONE ASINTOTICA
![[Pasted image 20241015204847.jpg|600]]
Visto che siamo nel caso peggiore prenderemo la n più grande 
Quindi T(n) è asintoticamente proporzionale e a $n^2$
>[!bug] Carrellata di esempi sulle slide a pagina 17-18

## DEFINIZIONI NOTAZIONI ASINTOTICHE(5)

1) $O$
>[!info]- Notazione asintotica  Serve per dare degli upper-bound
>![[Pasted image 20241015210315.jpg|400]]

2) $\Omega$
>[!info]-  lower-bound
>![[Pasted image 20241015211050.jpg|400]]

3) $\Theta$
>[!info]-  doppio confronto quindi uguali
>![[Pasted image 20241015211751.jpg|400]]

4) $o$ 
>[!info]- rapp tra infiniti con 0 notare che 
>$o \subset O$
>![[Pasted image 20241015212020.jpg|500]]

5)$\omega$ 
>[!info]-  infiniti con inf con 
>$\omega \subset \Omega$
>![[Screenshot 2024-10-15 220807.png|500]]

###### PROPRIETÀ NOTAZIONE ASINTOTICA (non devi saperle tutte )

![[Pasted image 20241015213617.jpg|500]]

![[Pasted image 20241015214625.jpg|500]]

## Usare la Notazione asintotica nelle analisi
![[Pasted image 20241015215836.jpg|500]]
![[Pasted image 20241015215907.jpg|500]]
## Notazione asintotica perchè è da fighi
- Ti da una misura indipendente da quelle della macchina utilizzata
- I dettagli sono poco rilevanti si semplifica tutto
- analizza il numero dei passi in modo abbastanza dettagliato
- descrive abbastanza bene gli algoritmi
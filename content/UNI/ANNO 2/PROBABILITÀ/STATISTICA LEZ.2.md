# FORMULE LEGATE ALLE PROBABILITÀ CONDIZIONATE
A partire dalla formula della PROBABILITA' condizionata
$P(A|B)=\frac{P(A\cap B)}{P(B)}$ 
Possiamo arrivare con la regola del prodotto alla seguente formula
$P(A\cap B)$=$P(A|B)*P(B)$
Anche con 3 eventi
$P(A\cap B \cap C)$=$P(A|B\cap C)*P(B|C)*P(C)$
## esempio 1
>[!example] Un'urna contiene 2 palline bianche, 3 rosse e 4 nere
>Si estraggono 3 palline a caso, una alla volta senza reinserimento
>1) calcolare la probabilità' di ottenere la sequenza (rosso,non rosso) sulle prime due
>estrazioni
>2) Calcolare la probabilità' di ottenere la sequenza (rosso,bianco, rosso)

1) 
![[Screenshot_2024-10-04-17-27-26-86_45415775811cea13943236d9369df411.jpg|400]]

2) 
![[Screenshot_2024-10-04-17-46-06-36_45415775811cea13943236d9369df411.jpg|450]]

## FORMULA PROBABILITÀ TOTALI
Rivedere meglio Disgiunti due a due non è diverso
$P(A) = \sum_{i \in I} P(A \mid E_i) P(E_i)$
###### Caso in cui abbiamo due eventi
$$
\begin{cases}
    E_1 = E \\
    E_2 = E^c
\end{cases}
$$
Allora $P(A)=P(A|E)*P(E)+P(A|E^c)*P(E^c)$
## esempio 3
>[!example] Un'urna ha 2 palline bianche e 1 nera.
>Si lancia un dado equo:
>- Se esce il numero 1 si mettono 2 palline bianche nell'urna
>- Se escono i numeri 2 e 3 si mettono nell'urna 1 pallina bianca e 1 nera
>- Se escono i numeri 4,5,6 si mettono 2 palline nere nell'urna.
Poi si estrae a caso  una pallina e si mette nell'urna
Calcolare la probabilità di estrarre una pallina bianca

![[Screenshot_2024-10-04-18-55-53-14_45415775811cea13943236d9369df411.jpg|500]]
Al livello numerico come si trova il complementare?
## FORMULA DI BAYES
$P(E_n|B)=\frac{P(B|E_n)*P(E_n)}{\sum_{i \in I} P(A \mid E_i) P(E_i)}$

SI USA SEMPRE INSIEME ALLA FORM DELLE PROB TOTALI
## esempio 4
Riprendiamo l'esempio 3 e poniamo questo quesito
>[!example] Calcolare la probabilità che sia uscito 2 o 3 nel lancio del dado sapendo di aver estratto una pallina bianca


Quindi possiamo dire che $P(E_2|B)$
Ora facciamo la formula di Bayes
![[Screenshot_2024-10-04-19-31-35-70_45415775811cea13943236d9369df411.jpg|600]]



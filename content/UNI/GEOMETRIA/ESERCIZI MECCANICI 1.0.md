# ESERCIZI SU MATRICI
Una matrice è composta da RxR con partenza colonna e arrivorighe
## <span style="color: white; background-color: #9E0404">RANGO</span>
numero di pivot dopo semplificazione di michael jordan
## <span style="color: white; background-color: #9E0404">DETERMINANTE</span>
distribuisci + - alternati facendo in modo che le colonne tra loro siano sempre diverse, prendi una serie di valori lineari in righe o colonne moltiplichi poi quei valori(con il laser) per il determinante della sotto matrice che ti si crea, quando arrivi a una matrice 2x2 applichi la place quindi fai $det(A)=ad-bc$
condizioni per barare: se avevi due righe o due colonne uguali allora il det=0
oppure se hai una riga o una colonna full di zeri allora il det=0
![[Pasted image 20240708183435.png|500]]
## <span style="color: white; background-color: #9E0404">base KER o NUCLEO</span>
prendi la matrice e te la semplifichi con il michael jordan poi moltiplichi con un vettore con le variabili che rappresentano ognuna una colonna e poni tutto uguale a 0, ti svolgi il tutto come se fosse un sistema, se hai delle variabili che non trovi devi metterle uguali a una lettera, successivamente scrivi il risultato così (0,0,1,1) se hai una lettera devi metterci il suo coefficiente
![[Pasted image 20240708184149.png|500]]
## <span style="color: white; background-color: #9E0404">base IMMAGINE</span>
michael jordan, vedi dove sono i pivot e ti scrivi le colonne che c'erano originariamente
![[Pasted image 20240708184425.png|500]]
## <span style="color: white; background-color: #9E0404">dimensione IMMAGINE</span>
è il rango
## <span style="color: white; background-color: #9E0404">dimensione NUCLEO</span>
n di colonne-dimensione(IMM)
una trasformazione lineare da $\mathbb{R}^3  a  \mathbb{R}^5$ avrà 3 colonne e 5 righe.
## <span style="color: white; background-color: #9E0404">POLINOMIO CARATTERISTICO</span>

$P(A)=det(A-\lambda *I_n )$
fai il determinante mettendo $A-\lambda$ ad ogni pivot, senza fare michael jordan
## <span style="color: white; background-color: #9E0404">AUTOVALORE</span>
lo trovi facendo il polinomio caratteristico, alla fine dello svolgimento del determinante potresti incorrere in code simili  a formule come ad esempio $(\lambda-4)(-\lambda^2-4\lambda-4)$ prendendo le $\lambda$ trovi gli autovalori ovvero 4 e -2(doppio)

## <span style="color: white; background-color: #9E0404">AUTOSPAZIO</span>

per trovare l'autospazio devi applicare gli autovalori alle $\lambda$ della matrice creata, successivamente fai il michael jordan e poi ti calcoli l'autovettore(come la base del nucleo) senza però cambiare le t in numeri e lasci le lettere e scrivi il tuo autospazio 
## <span style="color: white; background-color: #9E0404">AUTOVETTORE</span>
sostituisci le lambda e fai come il calcolo del sistema per trovare la base del nucleo
## <span style="color: white; background-color: #9E0404">MOLTEPLICITÀ o MEDIA GEOMETRICA E ALGEBRICA</span>

fai il polinomio caratteristico, quante volte appare $\lambda_n$ rappresenta la media algebrica\
se fai n-rango hai la media geometrica, dove n è la partenza della matrice ovvero colonne
ogni lambda ha una media geometrica e algebrica a sè
## <span style="color: white; background-color: #9E0404">DIAGONIZZABILE</span>
devi fare il polinomio caratteristico, poi trovi le $\lambda$ e le loro molteplicità, applichi le lambda ai pivot della matrice e fai il michael jordan, e scopri così il rango di quei singoli casi
la media geometrica deve essere uguale da quella algebrica
la media geometrica era n-rango dove n è la partenza(colonne)
la media algebrica è il numero di autovalori che trovi(molteplicità)
dopo aver fatto questi controlli devi fare la somma delle medie geometriche e deve essere uguale a n
## <span style="color: white; background-color: #9E0404">INVERTIBILE</span>

det diverso da 0 oppure rango=max oppure biunivoca
## <span style="color: white; background-color: #9E0404">INVERSA</span>
metti l'identita a destra e fai il michael jordan della matrice a sinistra modificando però anche quella a destra, devi avere l'identità a sx e a dx avrai l'inversa
oppure
fai $\frac{1}{det}*catania$
per fare catania ti devi fare il determinante di ogni singolo elemento della matrice, poi ogni singolo elemento della riga lo metti come se fosse una colonna quindi metti la matrice al contrario, poi moltiplichi per 1/det
## <span style="color: white; background-color: #9E0404">VETTORE APPARTIENE A IMMAGINE(A)</span>
metti la matrice= a quel vettore facendo un sistema e svolgendolo tipo un sistema omogeneo

## <span style="color: white; background-color: #9E0404">VEDERE SE ESISTE UN VETTORE</span>$x$ T.C. $A*x=w$

devi verificare se esiste l'inversa perchè ti porti a destra la A come frazione, successivamente fai la moltiplicazione del vettore $w$ con la $A^{-1}$ per farlo moltiplichi ogni elemento del vettore $w$ per il suo rispettivo elemento della riga per ogni riga, dopodichè otterrai un vettore che sarà il risultato della x
## <span style="color: white; background-color: #9E0404">VETTORI BASE DI R</span>
metti i vettori nella matrix fai il michael jordan e vedi il rango se rango=max allora è base di R

## <span style="color: white; background-color: #9E0404">BINET</span>
determinante di $(A*B)$ è uguale a $det(A)*det(B)$

## <span style="color: white; background-color: #9E0404">MOLTIPLICAZIONE TRA MATRICI</span>

ogni riga della prima matrice va moltiplicata con ogni colonna della seconda

## <span style="color: white; background-color: #9E0404">DIAGONALE</span>
trova i risultati degli autovalori e mettili in diagonale

## <span style="color: white; background-color: #9E0404">TEOREMA DEGLI ORLATI</span>

se hai una matrice puoi sfruttare il teorema degli orlati per definire il rango minimo, se prendi una matrice a caso dentro di una determinata dimensione $n*n$, se il suo determinante è diverso da 0 significa che la matrice più grande è almeno di quella n
# ESERCIZI SU APPLICAZIONI LINEARI
## <span style="color: white; background-color: #9E0404">LINEARITÀ</span>
per verificare linearità bisogna capire se c'è omogeneità e additività
l'omogeneità si verifica moltiplicando per c tutte le variabili della matrice e del sistema lineare e poi si porta fuori 
![[Pasted image 20240711102455.png]]
poer verificare l'additività invece bisogna verificare se T(U+V) è uguale a T(U)+T(V)
dove u è x1,y1 invece v è x2,y2

## <span style="color: white; background-color: #9E0404">LINEARMENTE INDIPENDENTE</span>
quando fai il giordano e i pivot che non sono 0 sono indipendenti se sono tutti 0 sono tutti dipendenti

## <span style="color: white; background-color: #9E0404">MATRICE ASSOCIATA</span>
prendi i coefficienti dei vettori e te li spalmi in una matrice in colonna
## <span style="color: white; background-color: #9E0404">MATRICE A BASE CANONICA</span>
prendi i risultati dei vettori e li spalmi in una matrice

## <span style="color: white; background-color: #9E0404">MATRICE</span>
la scrivi con le lettere così com'è

## <span style="color: white; background-color: #9E0404">SURRY</span>
il rango della matrice deve essere uguale alla n di arrivo

## <span style="color: white; background-color: #9E0404">INNY</span>
se il rango della matrice è uguale a quella di partenza

## <span style="color: white; background-color: #9E0404">BIUNY</span>
se è biunivoca è invertibile ed è sia inny che surry
## <span style="color: white; background-color: #9E0404">COMBINAZIONI LINEARI</span>
$v_{1,2,3}$=$v_4$ ?
mettiti la matrice e fai rouche capelli 

# GEOMETRIA SPAZIALE
## <span style="color: white; background-color: #9E0404">VETTORI FORMANO UNA BASE</span>
michael jordan mettendo i vettori sulle colonne e poi vedi se rango=max
## <span style="color: white; background-color: #9E0404">COME TROVARE UN PIANO</span>
bho

## <span style="color: white; background-color: #9E0404">RETTE INCIDENTI PARALLELE SGHEMBE COMPLANARI</span>
scrivi equazione parametrica applicando la formula A+t(B-A)
#### parallele
per vedere se sono parallele devi controllare se c'è un valore che molitplicato per il vettore di una delle due rette esce uguale alla sua amica retta
#### incidenti
i risultati delle equazioni parametriche delle due rette devono esserci soluzioni e non devono esserci cose strane tipo h=1 e h=3 o è 1 o 3
#### sghembe 
nè parallele nè incidenti
#### complanari
vedi se sono parallele

## <span style="color: white; background-color: #9E0404">EQUAZIONE PARAMETRICA E CARTESIANA</span>
prendi i vettori e applica la seguente formula r=A+t(B-A)
fai il sistema con le corrispondenze delle varie x y e z


## <span style="color: white; background-color: #9E0404">VEDERE SE UN SISTEMA È COMPATIBILE</span>

ti fai la matrice e il rg(A) deve essere uguale al rg(A|B)   (teorema rouche capelli)

## <span style="color: white; background-color: #9E0404">VEDERE QUANTE SOLUZIONI HA UN SISTEMA</span>
- rg max ha una sola soluzione
- rg non max infinite soluzioni/oppure non ne ha proprio
## <span style="color: white; background-color: #9E0404">VEDERE QUANDO UN SISTEMA SI COMPORTA COME UNA RETTA</span>
un sistema ha infinite soluzioni(ha almeno un parametro t s o roba così)
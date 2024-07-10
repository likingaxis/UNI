# ESERCIZI SU MATRICI
Una matrice è composta da RxR con partenza colonna e arrivorighe
## RANGO
numero di pivot dopo semplificazione di michael jordan
## DETERMINANTE
distribuisci + - alternati facendo in modo che le colonne tra loro siano sempre diverse, prendi una serie di valori lineari in righe o colonne moltiplichi poi quei valori(con il laser) per il determinante della sotto matrice che ti si crea, quando arrivi a una matrice 2x2 applichi la place quindi fai $det(A)=ad-bc$
condizioni per barare: se avevi due righe o due colonne uguali allora il det=0
oppure se hai una riga o una colonna full di zeri allora il det=0
![[Pasted image 20240708183435.png|500]]
##  base  NUCLEO
prendi la matrice e te la semplifichi con il michael jordan poi moltiplichi con un vettore con le variabili che rappresentano ognuna una colonna e poni tutto uguale a 0, ti svolgi il tutto come se fosse un sistema, se hai delle variabili che non trovi devi metterle uguali a una lettera, successivamente scrivi il risultato così (0,0,1,1) se hai una lettera devi metterci il suo coefficiente
![[Pasted image 20240708184149.png|500]]
## base IMMAGINE
michael jordan, vedi dove sono i pivot e ti scrivi le colonne che c'erano originariamente
![[Pasted image 20240708184425.png|500]]
## dimensione IMMAGINE
è il rango
## dimensione KER o NUCLEO
n di colonne-dimensione(IMM)
una trasformazione lineare da $\mathbb{R}^3  a  \mathbb{R}^5$ avrà 3 colonne e 5 righe.
## POLINOMIO CARATTERISTICO

$P(A)=det(A-\lambda *I_n )$
fai il determinante mettendo $A-\lambda$ ad ogni pivot, senza fare michael jordan
## AUTOVALORE
lo trovi facendo il polinomio caratteristico, alla fine dello svolgimento del determinante potresti incorrere in code simili  a formule come ad esempio $(\lambda-4)(-\lambda^2-4\lambda-4)$ prendendo le $\lambda$ trovi gli autovalori ovvero 4 e -2(doppio)


## AUTOSPAZIO

per trovare l'autospazio devi applicare gli autovalori alle $\lambda$ della matrice creata, successivamente fai il michael jordan e poi ti calcoli la base del nucleo senza però cambiare le t in numeri e lasci le lettere e scrivi il tuo autospazio 

## DIAGONIZZABILE
la media geometrica deve essere uguale da quella algebrica
la media geometrica era n-rango dove n è la partenza
la media algebrica è il numero massimo di autovalori uguali che trovi
dopo aver fatto questi controlli devi fare la somma delle medie geometriche e deve essere uguale a n
## AUTOVETTORE


## INVERTIBILE


## INVERSA


## VETTORE APPARTIENE A IMMAGINE(A)


## VEDERE SE ESISTE UN VETTORE $x$ T.C. $A*x=w$


## BINET


## MOLTIPLICAZIONE TRA MATRICI





## DIAGONALE


## EQUAZIONE CARTESIANA E PARAMETRICA


## MOLTEPLICITÀ GEOMETRICA E ALGEBRICA


# ESERCIZI SU APPLICAZIONI LINEARI
## LINEARITÀ


## MATRICE ASSOCIATA

## MATRICE

## SURRY

## INNY

## BIUNY



# GEOMETRIA SPAZIALE
## VETTORI FORMANO UNA BASE
rango=max
## COME TROVARE UN PIANO

## RETTE INCIDENTI PARALLELE SGHEMBE

## EQUAZIONE PARAMETRICA E CARTESIANA

## VEDERE SE UN SISTEMA È COMPATIBILE

## VEDERE QUANDO UN SISTEMA SI COMPORTA COME UNA RETTA

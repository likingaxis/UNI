lista di esercizi in arm
clicca qui per quelli del [[ESERCIZI ARM#n.3(libro)|simonetta]]

| Condizione | Descrizione                                       | Flag Coinvolti       |
|------------|---------------------------------------------------|----------------------|
| EQ         | Equal (Uguale)                                    | Z=1                  |
| NE         | Not Equal (Non uguale)                            | Z=0                  |
| CS/HS      | Carry Set/Unsigned Higher or Same                 | C=1                  |
| CC/LO      | Carry Clear/Unsigned Lower                        | C=0                  |
| MI         | Minus/Negative                                    | N=1                  |
| PL         | Plus/Positive or Zero                             | N=0                  |
| VS         | Overflow Set                                      | V=1                  |
| VC         | Overflow Clear                                    | V=0                  |
| HI         | Unsigned Higher                                   | C=1 & Z=0            |
| LS         | Unsigned Lower or Same                            | C=0 or Z=1           |
| GE         | Signed Greater Than or Equal                      | N=V                  |
| LT         | Signed Less Than                                  | N≠V                  |
| GT         | Signed Greater Than                               | Z=0 & N=V            |
| LE         | Signed Less Than or Equal                         | Z=1 or N≠V           |

# Esercizi nostri
## n.1(nostro)
> [!question]- Scrivi un programma che scambia i valori di due registri.
> ```arm-asm
> MOV R0,#10
> MOV R1,#5
> MOV R2,R0
> MOV R0,R1
> MOV R1,R2
> MOV R3,#0
> ```
## n.2(nostro)
Addizione di Numeri:
> [!question]- Scrivi un programma che somma due numeri e salva il risultato in un altro registro.
> ```arm-asm
>MOV R1,#10
>MOV R2,#5
>ADD R0,R1,R2
>```
## n.3(nostro)
>[!question]- Scrivi un programma che usa un'istruzione di salto per bypassare alcune operazioni.
>```arm-asm
>MOV R1,#1
>MOV R2,#1
>CMP R1,R2
>BNE skip  //Branch if Not Equal
>MOV R3,#9
>skip:
>MOV R3,#6
>```
## n.4(nostro)
>[!question]- Scrivi un programma che confronta due numeri e, se il primo numero è maggiore del secondo, somma un terzo numero al primo. Altrimenti, sottrai il terzo numero dal secondo.
>```arm-asm
>MOV R0,#1
>MOV R1,#2
>MOV R3,#10
>CMP R0,R1
>BGT somma //Branch if Greater than
>SUB R1,R3
>B skipsom
>somma:
>ADD R0,R3
>skipsom:
>MOV R4,#5
>```
## n.5(nostro)
>[!question]- Scrivi un programma che confronta due numeri e, se il primo numero è minore o uguale al secondo, moltiplica il primo numero per un fattore specificato. Altrimenti, somma una costante al secondo numero.
>```arm-asm
>MOV R0,#3
>MOV R1,#2
>MOV R3,#2
>CMP R0,R1
>BLE skip     // Branch if less or equal
>ADD R1,R1,R3
>B skimul
>skip:
>MUL R0,R0,R3
>skimul:
>// continuo condizione
>```

## n.6(nostro)
>[!question]- Scrivi un programma che sottrae il secondo numero dal primo e, se il risultato è negativo, moltiplica il secondo numero per un fattore specificato. Se il risultato è positivo o zero, incrementa il primo numero di una costante.
>```arm-asm
>MOV R0,#1
>MOV R1,#2
>MOV R3,#0
>MOV R5,#5
>SUB R4,R0,R1
>CMP R3,R4
>BGT skip   //maggiore Greater Than (se 0 è maggiore di R0-R1 skip)
>ADD R0,#1
>B nomult
>skip:
>MUL R1,R5
>nomult:
>```

## n.7(nostro)
>[!question]- Scrivi un loop che decrementa un registro finché non raggiunge zero.
>```arm-asm
>MOV R0,#3
>while:
 >CMP R0,#0
 >BLE skip   // branch if LESS or EQUAL R0<=0
 >SUB R0,R0,#1
 >B while
 >skip:
>```

## n.8(nostro)
>[!question]- Creare un programma che confronta due numeri memorizzati nei registri R0 e R1. A seconda del risultato del confronto, il programma eseguirà diverse operazioni aritmetiche: Se R0 è maggiore di R1, incrementare R2. Se R0 è uguale a R1, decrementare R2. Se R0 è non uguale a R1, moltiplicare R2 per 2. Se R0 è minore di R1, dividere R2 per 2 (per semplicità, assumiamo una divisione intera).

# Esercizi Simonetta
## n.1(libro)
>[!question]- creare un esercizio che faccia la divisione senza usare la divisione in ARM
>```arm-asm
>MOV R1, #10
>MOV R2, #5
>MOV R3, #0
>WHILE:
>CMP R1,R2
>BLT continua
>SUB R1,R2
>ADD R3,#1
>B WHILE
>continua:
>```

## n.2(libro)
>[!question]- creare un esercizio che faccia la moltiplicazione senza usare la MUL in ARM
>```arm-asm
>MOV R1, #10
>MOV R2, #5
>MOV R3,#0
>WHILE:
>CMP R2,#0
>BEQ continua
>ADD R3,R3, R1
>SUB R2,#1
>B WHILE
>continua:
>```

## n.3(libro)
>[!question]- creare un esercizio che faccia la potenza senza la potenza
>```arm-asm
>MOV R1, #0
>MOV R2, #0
>MOV R0,R1
>CMP R1,#0
>BEQ case0
>CMP R2,#0
>BEQ case1
>WHILE:
>CMP R2,#1
>BLT continua
>MUL R0,R0,R1
>SUB R2,#1
>B WHILE
>case0:
>CMP R2,#0
>BEQ case3
>MOV R0,#0
>case3:
>MVN R0,#0
>B continua
>case1:
>MOV R0,#1
>continua:
>```

## n.4(libro)
>[!question]- creare un esercizio che fa una somma degli elementi di un array
>```arm-asm
>.data  // entriamo nella sezione di data dove li creiamo
>array: .word 3,4,5,6   // ci creiamo un array con il nome che ci pare poi con .word per creare delle
>word
>.global _start //tipo il main  
>_start:      // tipo il main
>LDR R0,=array     // facciamo una load in R0 della nostra struttura dell'array
>LDR R2,[R0]       // facciamo una load del primo elemento di R0 in R2 per salvarcelo
>MOV R4,#0         // creiamo il nostro registro che salverà la somma
>CMP R2,#0         // compare per verificare se il primo elemento è minore a zero, pk lo prevede la
>pre cond
>BLT fine   		  // branch a etichetta fine
>//LSL R3,R2,#4     // per salvarci l'ultimo offset dell'array in R3 facciamo uno shift a sinistra di 4
>posizioni??
>MOV R1,#0        // R1 sarà il nostro offset
>while:
>LDR R2,[R0,R1]   // per scorrere stiamo dicendo che il nostro R2 è la somma di R0+R1
>ADD R4,R2        // salviamo in R4 R2
>ADD R1,#4        // per andare ai numeri successivi sommiamo R1 con 4 N.B indirizzo di base non
>cambia l'offset
>CMP R1,#12	     // confronta il massimo valore possibile con l'offset attuale per capire se deve
>fermarsi
>BLE while
>fine:
>```
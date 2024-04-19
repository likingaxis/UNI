lista di esercizi in arm
clicca qui per quelli del [[ESERCIZI ARM#^8f5769|simonetta]]
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

# Esercizi simonetta

^8f5769

non ci sono godo 
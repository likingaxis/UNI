
## Esercizio 1
1. Qual è la sua rappresentazione in formato binario?
	- conversione in binario di ogni punto
2. Considerando il sistema di indirizzamento a classi (ora non più in uso), dire:
	- a qual è la maschera di sottorete (in notazione decimale puntata)
		- per definirla prendi i primi bit dell'indirizzo
		- se 0 maschera /8
		- se 10 maschera /16
		- se 110 maschera /24
	-  b qual è il prefisso di rete in formato CIDR
		- byte del prefisso messi normali poi 0 0 +/x
	-  c quali sono la parte di sottorete e la parte di host nell'indirizzo
		- sottorete primi /x bit il resto la parte di host
	-  d quante interfacce potrebbe supportare la sottorete
		- $2^{32-x}-2$ 
		- x rappresenta i bit della sottorete -2 perché bisogna escludere broadcast e sottorete
	-  e indirizzo di broadcast diretto della sottorete
		- prendi l'indirizzo della sottorete e a tutti gli altri metti 255

## Esercizio 2
![[Pasted image 20250708174838.png]]
- ordina in base al numero di bit della sottorete più grande 
- confronta i byte della parte di host e vedi se sono simili
	- nel primo caso hai /24 quindi 8-16-24 3 byte, devi vedere corrispondenza tra primi 3 byte
	- nel secondo caso /18 sono 8-16 e poi 2 bit del 3 byte, ti converti 192 in binario e prendi i primi 2 bit e li confronti con il 3 byte dell'indirizzo
	- e così via...
	- se trovi corrispondenza con uno allora hai trovato la soluzione corretta perché prendi il numero di bit della sottorete più grande
## Esercizio 3
![[Pasted image 20250708175308.png]]
- per trovare il piano di partizionamento prendi tutte le sottoreti che sono collegate senza router
	- anche un router che è collegato a un altro router è una sottorete
	- per calcolare le interfacce devi fare numero host+ numero di router della singola sottorete
	- per definire quanti bit di host sono necessari e quindi quale prefisso corrisponde
		- devi fare $2^x-2\geq \ interfacce$ 
		- per capire il numero di bit della parte della sottorete fai 32-x
## ESERCIZIO 4
![[Pasted image 20250708175938.png]]
- data la subnet mask puoi dedurre il numero di bit della parte della sottorete
	- ad esempio alla prima sono 3 byte ovvero 8-16-24 allora avremo indirizzo/24
	- all'ultima abbiamo 8-16-23 perché abbiamo 255-1 quindi indirizzo/23
- convertiamo in binario gli unici byte che cambiano in tutti gli indirizzi
- raggruppiamo per next hop simili e anche per /x uguale
	- ogni destinazione con next hop uguale e /x può essere raggruppato modificando lo /x 
	- metteremo lo /x della subnet- quanti bit meno significativi cambiano
### ESERCIZIO 5
![[Pasted image 20250713160358.png]]
1. calcola numero di bit minimi per poi fare $2^x-2\geq interfacce$ 
	- poi $32-2^x$
2. parti da /25 fai 8-16-24 e poi prendi il primo bit di 128 
![[Screenshot_2025-07-13-16-08-14-65_45415775811cea13943236d9369df411.jpg]]
3. divide in 
- a) $2^{32-x}$
- b) calcoli intervallo di indirizzi prendendo dal prefisso di rete al prefisso di broadcast, senza contarli
- c) $2^{32-x}-2$  
	- -2 pk hai prefisso di rete e di broadcast


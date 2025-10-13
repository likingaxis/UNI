# PRINCIPI DELL'HARDWARE DI I/O
il mondo dell'I/O è un mondo vastissimo 
Per gestire al meglio hardware il sistema operativo deve avere delle funzionalità importantissime
- invio dei comandi
- intercettazione di interrupt
- gestione degli errori
usare una interfaccia che funzioni con + dispositivi e +sistemi
####  ci sono due punti di vista
- quello degli ingegneri elettronici
	- che vedono la scheda come una vera e propria scheda fisica
- quello dei programmatori
	- interessati alle interfacce che permettono di utilizzare gli hardware con comandi ecc...
### DISPOSITIVI I/O
### Ci sono due macro categorie di dispositivi di I/O:
#### 1. dispositivi a blocchi
Astraggono i dati in forma di blocchi di dati di dimensioni fisse e che prevedono l'esistenza di indirizzi
- HDD, SSD e  nastri
- ogni blocco viene scritto e letto indipendentemente
#### 2. dispositivi a caratteri
flusso di caratteri senza struttura a blocchi
- mi limito a inviare e ricevere dati senza gestirli in modo indirizzabile o effettuando ricerche
- stampanti interfacce di rete mouse
#### alcuni non fanno parte completamente di uno o dell'altro
schermi mappati in memoria 

alcuni dispositivi per semplificazione vengono messi nel file system dal sistema operativo
### Velocita dei dispositivi che hanno impatti importanti
![[Pasted image 20250107183643.png|600]]


## panoramica generale dei dispositivi e i vari controller
il s.o. comunica con i controller dei dispositivi
- controller integrato nella scheda madre

La scheda madre è divisa in northbridge e southbridge
northbridge è il piu veloce e interagisce con il pci-e
il southbridge è il piu lento e interagisce con le cose più lente
![[Pasted image 20250107184722.png]]
### Standard delle interfacce
tipo sata scsi thunderbolt ecc...
consentono di utilizzare dispositivi da diverse aziende
## interfacce di basso livello
sono le ultime interfacce possibili e si occupano della gestione dei veri e propri bit
effettuano verifiche e controlli per gli errori dei bit con ad esempio ECC(Error Correction Code)
## Una vecchia porta parallela
![[Pasted image 20250107185303.png|300]]
![[Pasted image 20250107185318.png|200]]
vecchia interfaccia per stampanti ecc
8 spinotti per scambiare i dati
8 per i comandi effettivi
altri per la gnd e alimentazione
## porta usb
![[Pasted image 20250107190238.png|300]]
la vecchia porta usb è una interfaccia standardizzata per effettuare una connessione con il computer e i dispositivi 
![[Pasted image 20250107190048.png|300]]
2 pin per alimentazione e 2 per i dati 
in base alle onde positive o negative si codifica e decodifica il segnale
![[Pasted image 20250107190035.png|700]]
diverse versioni di usb portano una forte retrocompatibilità e sono plug-play
### tabella di porte usb
![[Pasted image 20250107190501.png|500]]

### un disco hdd come è fatto
PCB è il circuito che ha
- al centro una MCU (micro controller unit)
- cache una ram usata per una cache
- VCM controlla la rotazione del motore del disco
![[Pasted image 20250107190540.png|500]]

## Come comunicano dispositivi e CPU
ogni dispositivo ha un controller che fa da intermediario tra cpu e dispositivo
questo controller ha dei registri dove scrivere e leggere le informazioni
molti hanno una area detta buffer dove vengono conservati i dati mentre vengono letti o scritti

## Come avviene? importante
uso due approcci per inviare i dati
- I/O port-mapped
- I/O memory-mapped
- versione ibrida
#### Port mapped I/O
 per rappresentare un dispositivo hardware uso ad esempio port mapped I/O
 ogni porta è un collegamento con quel dispositivo definito attraverso un indirizzo 
 ogni porta a 8 o 16 bit
uso istruzioni differenti dal solito assembly
- `IN REG, PORT ` per la lettura di port e salva in reg 
- `OUT PORT,REG` per scrivere
due spazi di indirizzi uno per la ram e uno per i dispositivi di I/O
![[Pasted image 20250108171938.png|300]]
#### Memory mapped I/O
![[Pasted image 20250108173252.png|200]]
ma perché non mettiamo tutto insieme?
ogni dispositivo viene mappato in memoria insieme alle altre cose con degli indirizzi univoci
i registri hardware sono accessibili solo dal kernel, garantisce maggiore sicurezza

Attraverso la gestione delle pagine di memoria, il sistema può controllare dispositivi in modo selettivo. 
potrebbe esserci un problema relativo all'utilizzo della cache
dove un registro viene salvato in cache e non subisce cambiamenti dal dispositivo e quindi il dato non si aggiorna
![[Pasted image 20250108181001.png|300]]
di questo sistema c'è una problematica che prevede 2 soluzioni
il sistema non sa se ha a che fare con un indirizzo in memoria o che appartiene a un dispositivo hardware
- prima soluzione a tentativi lenta ma facile da scrivere
- bus snooping come seconda soluzione che monitora quali sono i dispositivi di I/O e determina se un indirizzo è associato a un dispositivo hardware o alla memoria principale.
necessità di bilanciare prestazioni e efficienza

#### IBRIDO
![[Pasted image 20250108183047.png|200]]
si usano entrambi i metodi uno per operazioni più rapide l'altro per operazioni più lente
PMIO e MMIO, il primo per fare roba più lenta l'altro roba più veloce

### Direct memory access
##### DMA VS SENZA
Il controller DMA consente lo scambio di dati dei dispositivi senza uso della CPU
- senza DMA il controller del disco legge i dati e li memorizza nel suo buffer e li invia al SO
- con DMA la CPU dice al DMA attivati e dice al controller del disco attivati e li fa lavorare
![[Pasted image 20250108185829.png|500]]
Il controller DMA può essere
- semplice(1 trasferimento per volta)
- complesso(+ trasferimenti)
	- inoltre possono essere più personalizzabili 
	- gestiscono più controller di dispositivi

##### Come trasferisco i dati?
tutti i blocchi citati riguardano un conflitto di bus
- cycle stealing: invio un pacchetto alla volta rubando cicli alla cpu, perché ogni volta la interpello
- modalità burst: invia tutto con una botta rubando il bus per quel tempo
- fly by mode: trasferisce direttamente alla memoria principale senza cpu usando semafori mutex o roba cosi
### Come arriva l'interrupt
- trap, azione deliberata, expected
- fault, azione non deliberata, unexpected
- interrupt hardware segnali inviati da dispositivi come stampanti alla CPU
l'interrupt viene gestito da un controller
se ho piu interrupt li gestisco con delle code e algoritmi
![[Pasted image 20250108192445.png|500]]
#### STEP interrupt
1. un dispositivo richiede attenzione alla CPU inviando un interrupt alla CPU, il controller assegna un numero a quel dispositivo per identificarlo
2. la CPU interrompe ciò che fa e ha un vettore degli interrupt dove ad ogni numero corrisponde un indirizzo di quello che deve eseguire a seconda dell'interrupt. Quando un dispositivo corrisponde a un numero la CPU prende quel numero e lo confronta con l'array e esegue quella determinata riga di codice 
3. sfrutta il vettore degli interrupt, per eseguire una procedura puntando alla sua base
4. una volta eseguita tutta la routine quindi procedura ecc... la cpu scrive nel controller degli interrupt per dire che ha finito questo è utile per evitare race conditions ovvero conflitti 
5. il program counter deve essere salvato per far riprendere la CPU ciò che stava facendo
6. le informazioni dai dispositivi di I/O viene salvato nei registri interni o sullo stack
7. ci sono due tipi di stack, uno nel kernel uno invece che appartiene al processo utente, con quello utente si possono creare errori, quello del kernel richiede cambi di contesto che rallentano un po' le cose

### interrupt precisi vs imprecisi
![[Pasted image 20250109102914.png]]
la CPU grazie a pipeline può gestire più processi senza che debbano per forza finire
questo complica la gestione degli interrupt
abbiamo due tipi di interrupt:
1. interrupt precisi: il sistema quando avviene un interrupt può determinare con esattezza quali istruzioni sono state completate
2. interrupt imprecisi: salviamo gli stati di completamento degli interrupt non sapendo effettivamente lo stato del programma
con gli interrupt precisi: 
- forzo che le istruzioni terminino
- tutte le istruzioni prima del program counter sono state eseguite
- la CPU annulla tutti gli effetti transitori eseguiti dopo il PC, per evitare azioni non prevedibili
- quando avviene un interrupt vengono completate tutte le istruzioni prima di quella che stava per fare la CPU così si ha uno stato definito
con gli interrupt imprecisi:
- ogni istruzione viene lacciata con uno stato di completamento
- salvare tutti questi stati rallenta il computer
- non tutti gli effetti sono completamente annullati



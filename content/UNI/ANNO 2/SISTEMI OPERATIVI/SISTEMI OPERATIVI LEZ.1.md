### Def sistema operativo
Il sistema operativo è uno strato di software della macchina ha lo scopo di fornire una semplificazione delle risorse hardware ai programmi
- Il s.o. maschera gli elementi sottostanti della macchina
- Il s.o. consentono la gestione di esecuzioni in parallelo
- Il s.o. e' un gestore delle risorse e ne facilita l'utilizzo
![[Pasted image 20241010161716.jpg|400]]
In mezzo abbiamo un s.o. che traduce le operazioni dall'alto verso le componenti in basso
##### Librerie
Una persona che vuole creare un software non si deve reinventare le interazioni con i livelli sottostanti bensì utilizzerà Librerie ovvero estratti di codice da implementare per accedere alle componenti sottostanti
##### Differenza principale tra normale software e sistema operativo
Esistenza di un flag che differenzia del codice software o del codice software del s.o.
Il s.o. accede a cose in più 
Cambio di contesto da software a modalità kernel
Il s.o. deve saper gestire
- più utenti
- più programmi in esecuzione
La gestione delle risorse del sistema operativo include il discorso di Multiplexing(condivisione) fa dividere la gestione delle risorse in 2 modalità 
- temporale: quando una risorsa viene condivisa tra utenti o programmi a livello temporale ovvero che richiede del tempo per essere completata come una CPU spartita tra più utenti o programmi e viene usata a giro da ognuno
- spaziale i clienti(utenti o programmi) al posto di alternarsi prendono una parte della risorsa intesa come memoria
### Come sono nati?
Ci sono 5 generazioni
1) anni 50 le macchine avevano solo uno scopo utilizzo di schede perforate e filamenti, se volevi cambiarne l'uso dovevi buttarla giù e ricostruirla, es: colossus
2) anni 60 macchine anche chiamate ***mainframe*** con uso dei transistor che consentiva di cambiare le operazioni da far svolgere alla macchina attraverso dei programmi su schede forate e uso del sistema batch ovvero un insieme di job(programmi) ed un sistema che permetteva di eseguire le varie operazioni che necessitavano più macchine con  una organizzazione simile a una pipeline
![[Pasted image 20241010173030.jpg|450]]
3) anni 70 primi sistemi operativi come MULTICS e UNIX con multiprogrammazione, una macchina che consentiva più programmi contemporaneamente così da soddisfare i clienti ad esempio la 7094 della ibm 360 con strumenti scientifici e commerciali. POSIX chiamate a sistema che devono essere in ogni sistema operativo
4) anni 80 i personal computer di oggi con le loro peculiarità e i loro sistemi operativi
5) anni 90 i computer mobili di oggi come telefoni ecc

## PARTE HARDWARE
Ogni dispositivo ha un microprocessore che si interfaccia con il sistema operativo e viceversa
#### il processore
Sono il cervello del computer prelevano le istruzioni dalla memoria e le eseguono in cicli contraddistinti 
Ricordare almeno i registri:
- PC, Program Counter, contiene l'indirizzo di memoria della prossima istruzione da eseguire
- PSW, Program Status Word, contiene bit con il codice di condizione, impostati da istruzioni a confronto, la priorità della CPU, la modalità (utente o kernel) e altri diversi bit di controllo
- SP, Stack Pointer, punta alla cima dello stack
Concetto di multiplexing delle operazioni nel tempo pipeline
Cache nella CPU
![[Pasted image 20241010180055.jpg|450]]
### memorie
Più  una memoria e' veloce più costa e di solito e' meno capiente
![[Pasted image 20241010180415.jpg|450]]
### dispositivi di I/O
Sono costituiti da due parti un controller che gestisce il dispositivo e il dispositivo stesso
Il controller fa da interfaccia per il sistema operativo
La CPU parla con un controller del disco che parla poi a sua volta con un controller e quest'ultimo parla con la CPU

![[Pasted image 20241010180537.jpg|500]]
##### DMA
E' un chip che consente l'accesso diretto tra un controller di un dispositivo e la memoria senza mettere in mezzo la CPU che dovrà solo comunicare la dimensione di byte che si possono scambiare i due
### bus
Sono una serie di fili che consentono la comunicazione tra dispositivi, se il bus e' di scarsa qualità il sistema avrà un collo di bottiglia
![[Pasted image 20241010183402.jpg]]
## AVVIO DEL SISTEMA

Ogni PC ha una motherboard con un BIOS ovvero un software di I/O di basso livello ora risiede in una piccola memoria flash non volatile nella mobo e gestisce varie cose del 
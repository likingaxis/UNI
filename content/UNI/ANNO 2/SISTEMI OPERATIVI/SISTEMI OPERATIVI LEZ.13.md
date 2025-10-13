## ASTRAZIONE DI MEMORIA
le memorie che considereremo si suddividono in
- memoria principale (RAM)
	- costosa, poco capiente, veloce
- memoria "normale" dischi ma non solo dischi
	- meno costosa, più capiente, meno veloce(tranne ssd)
###### Il ruolo del sistema operativo
gestire questa gerarchia di memoria in un modello utile e astratto

- non è solo importante avere tanta memoria ma anche gestirla bene

>[!info] definizione di astrazione di memoria
>i processi pensano che la memoria sia in un modo ma invece è in un altro, 
>questa illusione la fa il s.o.

## LE ORIGINI
### MEMORIA SENZA ASTRAZIONE
Qui abbiamo un uso diretto della memoria fisica
uso i registri e ci metto dentro byte di informazioni `mov reg1,1000`
>[!bug] problemi di sovra scrizione e di accesso ai dati

==9:40== sono cazzi
==quanti bit servono per fare riferimento a un numero==
==da 0 a 32764==
la multiprogrammazione senza astrazione
con indirizzi assoluti posso avere problemi di sovrascrizione

##### MODI DI ORGANIZZARE UNA MEMORIA NON ASTRATTA
ci sono tre modelli
- a) OS in RAM(es. nei mainframe)
- b) OS in ROM(es. sistemi embedded)
- c) OS+ driver in ROM+RAM(es. primi pc)
![[Pasted image 20241120192034.png|500]]
è possibile scambiare i programmi in esecuzione attraverso uno **swapping**
- metto il processo da togliere in una memoria non volatile
>[!bug]- esempio di conflitto di indirizzamenti
>![[Pasted image 20241120195800.png]]
>- la memoria più grande sarà suddivisa da programma 1 e poi programma 2(figura c)
>- il programma 1 fa un jump a riga 24 (freccia rossa)
>- il programma 2 può andare dove gli pare e quindi andrà a intasare il programma 1 (freccia blu)
### ASTRAZIONE
ad ogni processo viene assegnato un insieme unico di indirizzi separato dagli altri
- lo spazio degli indirizzi è quell'insieme unico di indirizzi che può usare un processo per indirizzare la memoria
###### Un vecchio esempio di astrazione
lo spazio di indirizzi del processo veniva mappato e inserito in parti diverse di memoria fisica.
questo concetto prevede l'utilizzo di:
- registro base(offset): contiene l'indirizzo fisico di ogni inizio programma
- registro limite: contiene quanto è lungo un programma
>[!example] se ad esempio un processo chiede indirizzo 1000 il s.o. gli assegnerà 1000+k
>- k rappresenta il registro base
>- ogni processo ha la sua base e se la sfora so cazzi
>- il s.o. ha il compito di capire il limite delle richieste in memoria del processo

>[!tip] IN POCHE PAROLE ogni volta che avviene un riferimento in memoria da parte di un programma
>- Aggiunge il registro base all'indirizzo generato dal programma
>- Il registro limite viene usato per non far superare eventuali limiti di accesso

>[!example]- esempio diretto
>![[Pasted image 20241121093055.png]]
>riprendiamo l'esempio delle memorie non astratte
>- stavolta effettuiamo dei controlli per verificare se rimaniamo nella nostra area di memoria
>- il registro limit viene usato per definire il limite di dove può stare il processo

è vero, ogni programma ha il suo spazio, ma calcolare tutte queste cose comporta un rallentamento del sistema
#### cosa succede se sforo la memoria?
se la memoria viene riempita faccio 
- uno swapping, sposto le informazioni da memoria volatile a non volatile
	- questa tecnica si usa solo se necessario
- memoria virtuale
	- cerca di lasciare i processi in esecuzione lasciandogli parziali memorie disponibili

#### Frammentazione della memoria
i processi nel corso della loro esecuzione possono chiedere sempre più memoria.
per questo motivo il s.o. potrebbe assegnare più del necessario per evitare problemi
>[!quote] mi chiedi 10 ti do 14 dai ;)
>![[Pasted image 20241121161639.png]]

la coperta però e corta quindi spreco memoria.
Se termino la memoria faccio una di queste 3 cose
- lo swapping
- trasferisco il processo
- uccido il processo
>[!bug]- quando tolgo un processo dalla memoria e ne metto altri potrei creare delle frammentazioni di memoria
>- la ricompattazione di quei frammenti di memoria che si creano provoca un rallentamento del sistema
>- una soluzione è quella citata prima ma non é troppo efficiente (quella del mi chiedi 10 ti do 14)
>
>![[Pasted image 20241121161540.png|500]]

### GESTIONE DINAMICA DELLA MEMORIA
Come gestisco la memoria libera?
cerco di tenere traccia della memoria cercando di minimizzare il fenomeno della frammentazione
ho 2 metodi principali
- metodo Bitmap tiene traccia di quali blocchi vengono allocati
- metodo usando una lista collegata che tiene traccia della memoria non allocata

prima di iniziare a spiegare i due metodi vorrei precisare una cosa:
>[!tip]- modi per scrivere una matrice di valori e rappresentarla
>matrice:
>- densa: memorizzo tutto così com'è
>- sparsa: tolgo gli 0 inutili e le ripetizioni
>
>rappresentazione:
>- densa: rappresento tutto così com'è
>- sparsa: tolgo gli 0 inutili e le ripetizioni
##### metodo Bitmap:
Questo metodo fa uso di una Bitmap per indicare dove sono presenti degli Hole(spazi vuoti) oppure dei Process(spazi pieni), si fa spesso uso anche di una linked list per rappresentarla
- con la linked list possiamo vedere che non é granché efficiente perché per arrivare alla fine dobbiamo scorrerla tutta

![[Pasted image 20241121164525.png]]
- è suggerito l'uso di una lista collegata da ambe le parti per ottimizzare le cose
	-  tornare indietro è figo perché consente di guardarsi alle spalle senza ricominciare
![[Pasted image 20241121165040.png|400]]

### METODOLOGIE PER ANDARE AD ALLOCARE MEMORIA
- First fit: Seleziona il primo spazio disponibile (usata in MINIX3 molto semplice)
- Next fit: Seleziona il successivo spazio disponibile(più lento)
- Best fit: Sceglie il più adeguato
- Worst fit: Sceglie il meno adeguato
- Quick fit: Crea dei preset di spazi(le più utilizzate)
- Buddy allocation: Migliora le performance del quickfit(lo vediamo subito dopo)
### PRECISAZIONI SUL Buddy allocation
- usato in linux
- La memoria inizia come un singolo pezzo
- Ad ogni richiesta la memoria viene divisa in una potenza di 2
- quando una allocazione di memoria viene rilasciata avviene una coalescenza e si riuniscono
>[!question]- coalescenza?
>è tipo agar.io oppure il merge.
>![[LFZDzY.gif]]

![[Pasted image 20241121172719.png]]
- **a)** la memoria consiste in un unico pezzo da 64 blocchi
	- appena un processo ha bisogno di tot blocchi di memoria li divide per 2 appena gli bastano
- **b)** 32 ti bastano? no
- **c)** 8 bastano? si va bene grazie ciao
appena un processo termina viene ricompattata la cosa **(h->i)**
![[Pasted image 20241121172901.png]]

###### FRAMMENTAZIONE NEL BUDDY
>[!bug] Il problema del buddy algorithm e che ho delle piccole frammentazioni di memoria (caccolette) che si possono formare e che sono difficili da riunire

- il buddy algorithm è l'algoritmo
- il buddy allocator è il processo che fa avvenire l'allocazione
###### UNA SOLUZIONE: SLAB ALLOCATOR
Se io dovessi allocare $65$ pagine con il buddy, dovrei richiederne $128$ e $63$ sarebbero inutilizzate
![[Pasted image 20241121173526.png]]
Lo slab allocator usa l'algoritmo buddy per farsi allocare tot pagine di memoria e poi ci fa quello che vuole:
se a un processo serve $1$ pagina di scarto lo slab ne prende $2$ e $1$ la da a quel processo
- i piccoli blocchi di memoria vengono chiamati $slabs$ suddivisi in $chunk$
>[!quote] lo slab allocator e tipo un monnezzaio che prende tutte le caccolette e crea una memoria decente

Ogni **chunk** corrisponde a un oggetto o una porzione più piccola di memoria.

Gli **slab** sono classificati in 3 stati:

- **Full**: Tutti i chunk sono occupati.
- **Partial**: Alcuni chunk sono occupati, altri liberi.
- **Empty**: Tutti i chunk sono liberi.

![[Pasted image 20241121175739.png]]
###### IL CACHING
Quando un oggetto viene deallocato non viene immediatamente restituito alla memoria libera
viene mantenuto nella cache così da soddisfare richieste nell'immediato senza sprecare troppe risorse
##### Cosa contiene uno slab?
- puntatore che punta agli oggetti
- un indice che indica il prossimo slot libero
- `bufctl` è un array con gli indici dei prossimi oggetti liberi
![[Pasted image 20241121180749.png]]
#### Concetto di memoria virtuale
ogni programma ha un proprio spazio di indirizzi suddiviso in pagine
page fault
48 bit perche 48 sono gia un botto
==0k-4k 4k-8k...==
il programma chiede 32780
ho delle pagine che vanno a 4kb
se mi chiedi 32k siamo nella pagina 8
se non ha ancora puntato alla memoria vera, punta a una area vuota che soddisfa ad esempio il blocco n.1
4096 
calcolo logaritmo in base bho bisogna fare log_custom/lob_bho
==1:18==
un s.o. deve anche contenere la tabella delle pagine
viene utilizzata una cache speciale sul processore per salvare queste tabelle
==1:25== compito per casa


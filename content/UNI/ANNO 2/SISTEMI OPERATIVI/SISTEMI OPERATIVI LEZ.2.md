### QUANTI NE ESISTONO 
Tanti ma ci sono famiglie
1. Sistemi per mainframe(grandi computer per banche)
	- gestiscono più transazioni quindi concetto di gestione simultanea e Multiplexing
	- non è richiesta l'interazione dall'utente
	- transazione una sequenza di operazioni con garanzia che vengano eseguite con successo
2. Sistemi per Server
	- computer con funzionalità, risorse e operazioni complesse
	- possono accedervi più utenti
3. Sistemi per personal computer
	- supportano un singolo utente
	- hanno una interfaccia facilitata
4. Sistemi per Smartphone e Tablet
	- prevedono un solo utente e ottimizzazione delle librerie per uso di app di terze parti software e hardware
5. Sistemi per IoT e embedded(dispositivi perfetti per svolgere un solo compito)
	- componenti di circuito hardware come frigoriferi, lavatrici ecc...
	- non general purpose e leggeri e limitate
6. Sistemi real-time
	-  quando deve rispettare scadenze rigide con quanti temporali da dover rispettare e che non venga mai rimandato
7. Sistemi operativi per Smart Card:
	- Sistemi estremamente recenti come carte con contatti ecc
	- tante volte si usa Java

#### COSA Hanno in comune?
1) Extended machine
	- estraggono nascondono e estendono funzionalità hardware e cose complicate
2) Resource manager
	- l'uso simultaneo con condivisione equa delle risorse e eventuali limitazioni


### Concetti base di un sistema operativo
- il s.o. offre le sue funzionalità attraverso delle chiamate di sistema
- il s.o. ha dei servizi ovvero n chiamate di sistema es(file system,Process management Service)
- Ogni processo ha il proprio spazio di indirizzamento
- Un processo non avrà uno spazio di memoria dedicato fisico ma avrà una partizione della memoria: esempio con mattonella dando una piccola porzione di mattonella dinamicamente
- I file persistono rispetto ai processi
### Cos'è un processo?
Il processo è un programma in esecuzione
- è associato a uno spazio di indirizzi e a una serie di risorse come registri e file aperti
- Il s.o. deve salvare i vari SP,PC ecc per poi farlo riprendere durante l'alternarsi
- il processo può essere visto come il contenitore di tutte le informazioni necessarie per l'esecuzione del determinato programma

### IL LAYOUT DI UN PROCESSO
==Quante linee sono FFFF?==
>[!info]- come viene rappresentato in memoria il processo?
>![[Pasted image 20241016175303.jpg|300]]
> - Stack: le Active call data è una porzione di memoria che viene usata da un processo per metterci dentro informazioni durante la sua esecuzione, come risultati di funzioni che poi una volta finito il processo vengono eliminate
> - Data: vengono messe le variabili del programma e possono essere locali e globali
> - Text: viene messo il codice del programma
### CICLO DI VITA DI UN PROCESSO(generazione di un processo)
Il s.o. ha una tabella con tutte le info sui processi
- quando un processo è sospeso potrà riprendere l'esecuzione grazie alle informazioni e registri salvati nella tabella dei processi e anche grazie al suo spazio di indirizzi di memoria
un processo può:
- crearsi
- terminarsi
- sospendersi
- riprendersi
- creare un'altro sotto processo come _"figlio"_  
Ogni processo può clonarsi quindi c'è bisogno di un PID(Process-Id) per identificare i
processi 

>[!info] Un albero di processi composto da processi e processi figli
>![[Pasted image 20241016181441.jpg|400]]

### CHI POSSIEDE UN PROCESSO?
Ogni processo e' collegato a un UserId
>[!tip] su Unix un processo figlio ha stesso UId di un processo padre

Ogni utente può essere in un gruppo identificati con GUid
Poi c'è super-user root con più privilegi
### FILE
Astrazione di un dispositivo di memorizzazione reale e non tipo un disco
Ogni file non ha continuità di bit ma frammentazioni 
Risorsa=File=sequenza di $1,0$
##### STRUTTURAZIONE PER CERCARE FILE
Con win abbiamo c: ....
Con UNIX abbiamo nodo radice e sotto nodi che sono risorse ecc
- la directory principale root è /
- ci sono Absolute Path come /home/ast/todo-list
- percorsi a partire dalla directory dove siamo ../courses/slides1.pdf
- altri filesystem(CD,DVD,USB...) possono essere montati nella root /mnt/windows
>[!question]- Cartella e' un file?
>Si👍
##### proprietà file con metadati

>[!info]- I file sono protetti da tre bit che corrispondono a diverse entità di una macchina, ogni bit consente o meno determinate attività sul file
>![[Pasted image 20241016182926.jpg|400]]
>- r=read
>- w=write
>- x=execute
>- Rosso=Owner Verde=Group Blu=Other
>- 14492 sono l'unione di tutti i frammenti di questo file in memoria che formano una serie di byte

Il sistema operativo non decide nulla quindi fa le cose in base allo user che lo usa 
##### Esempio di organizzazione di un file system 
Un file system viene organizzato in una certa struttura arborea
>[!fotoesempio]-
>![[Pasted image 20241016185532.jpg|500]]

Quando eseguiamo un montaggio di un dispositivo nel s.o. la sua organizzazione deve essere riconciliata come quella del s.o.
Non è scontato questo cambiamento di struttura poiché il s.o. potrebbe non riconoscere il tipo di formattazione della chiavetta
![[Pasted image 20241016190243.jpg|400]]
- a) Prima del mount la USB non è accessibile
- b)dopo la mount la USB si è collegata nei file
##### ESEMPIO ACCESSO AI FILE
ESERCIZIO PER CASA

###### TUTTO è un file
In Linux i device hardware vengono visti come dei file
- Block special file per I dischi
- Character special file per le porte seriali
###### FILE A PIPE
Processi comunicano tra loro con le pipe, ovvero pseudo file che viaggiano su un canale FIFO
Scrivere un processo che comunica con altri processi attraverso pipe(chiede a esame)
![[Pasted image 20241016203452.jpg|400]]
## CHIAMATE DI SISTEMA
Una chiamata di sistema permette ai programmi in user space (spazio utente) di richiedere servizi o risorse direttamente al kernel del sistema operativo. È uno dei meccanismi fondamentali che consentono ai programmi di interagire con l'hardware e le risorse di sistema in modo controllato e sicuro.
Quando un programma ha bisogno di un servizio che solo il kernel può fornire (ad esempio leggere un file), deve effettuare una chiamata di sistema.
![[Pasted image 20241016205008.jpg|400]]

- Devono essere estremamente veloci
- Trap blocca il processo e lo sposta facendogli fare il cambio di contesto
- le chiamate di sistema variano a seconda del s.o. come soluzione si sono create delle chiamate di sistema generiche per ogni s.o. POSIX
#### quali sono le chiamate di sistema per la gestione dei processi che vedremo?

- il programma prepara i parametri della procedura che deve chiamare read(fd, buffer, nbytes)
- il programma chiama la procedura nella libreria 
- in un registro RAX viene immesso il numero che identifica il tipo di funzione del kernel che bisogna eseguire(read, write,open...), spesso questi numeri vengono messi in una tabella
- passaggio a modalità kernel che avviene attraverso una istruzione trap verso il kernel
- il gestore di chiamate di sistema viene eseguito
- viene ridato il controllo alla procedura utente
![[Screenshot_2024-10-17-16-19-37-53_f56466bc4bb61e6d2de1f3b0468a89d9.jpg|700]]


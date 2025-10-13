>[!question]- lista di domande
># DOMANDE
> 
> 1. **Si analizzi il concetto di multiplexing in un sistema operativo. Come si differenziano le modalità di condivisione temporale e spaziale delle risorse? Si forniscano esempi pratici.**
> >[!done]- la risposta
> >l'ho spiegato alla domanda prima
> 2. **Si illustri il ciclo di vita di un processo in un sistema operativo moderno. Quali sono le transizioni di stato principali e come vengono gestite dal kernel?**
> >[!done]- la risposta
> >un processo viene:
> >- generato
> >- eseguito
> >- viene messo in fase di blocco
> >- si riprende
> >- si può clonare
> >- può interrompersi
> >inoltre ha 3 stati principali : bloccato, esecuzione, pronto
> > se un processo viene messo in stato di blocco i suoi registri vengono salvati per poi essere riusati
> 3. **Si fornisca una spiegazione del funzionamento delle chiamate di sistema, con particolare attenzione al passaggio dalla modalità utente alla modalità kernel. Qual è il ruolo delle istruzioni `trap`?**
> >[!done]- la risposta
> >il processo può avere cambi di contesto dove passa dallo spazio utente allo spazio kernel, con esso vengono salvati tutti i registri di quel processo e vengono spostati nello spazio di memoria kernel, le istruzioni trap hanno lo scopo di prendere il processo nella sua interezza catturandolo a seconda di determinate condizioni che la innescano
> 4. **Si inviti il candidato a spiegare il funzionamento di una pipe in Linux. Qual è l’importanza delle pipe nella comunicazione tra processi? Si fornisca un esempio pratico.**
> >[!done]- la risposta
> >una pipe è uno pseudo-file utilizzato dai processi per comunicare tra loro, la pipe ha una sezione di input e una di output e funziona attraverso una logica di tipo FIFO
> 5. **Si definisca il ruolo del Program Counter (PC) e dello Stack Pointer (SP) nella gestione di un processo. Come il sistema operativo utilizza questi registri durante il cambio di contesto?**
> >[!done]- la risposta
> >questi registri sono in ogni processo
> >il program counter ha lo scopo di puntare all'istruzione successiva che deve essere eseguita dal processo
> >lo stack pointer punta alla cima dello stack del processo, infatti ogni processo ha uno stack dove vengono salvate le informazioni utilizzate nel corso del codice
> >il s.o. li usa per il cambio di contesto per far riprendere l'esecuzione del codice senza causare problemi di alcun tipo
> 6. **Si descriva il funzionamento di un file system montato in un sistema UNIX. Quali sono le implicazioni della formattazione del dispositivo per il sistema operativo?**
> >[!done]- la risposta
> >un file system in un sistema UNIX ha una gerarchia ad albero molto organizzata e che si dirama a partire dalla root / ogni file come anche cartelle sono strettamente collegate in qualche modo ad essa, quando andiamo ad inserire un dispositivo esterno di memorizzazione che ha un suo file system lo aggiungiamo a quello del nostro s.o. attraverso il mount, esso verrà adeguatamente messo nella gerarchia
> 
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
>[!question]- Quante linee sono FFFF?
>- F sono 4 bit 
>- con 4 bit puoi rappresentare fino al numero 15 1111
>- abbiamo 4 F quindi 16 bit
>- 1 byte sono 8 bit 
>- quindi sono 2 byte

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
### Stati di un processo
![[Pasted image 20250117162817.png|500]]


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
- il programma chiama la procedura nella libreria (4)
- in un registro RAX viene immesso il numero che identifica il tipo di funzione del kernel che bisogna eseguire(read, write,open...), spesso questi numeri vengono messi in una tabella(5)
- passaggio a modalità kernel che avviene attraverso una istruzione trap verso il kernel(6)
- il gestore di chiamate di sistema viene eseguito(8)
- viene ridato il controllo alla procedura utente(10)
![[Screenshot_2024-10-17-16-19-37-53_f56466bc4bb61e6d2de1f3b0468a89d9.jpg|700]]


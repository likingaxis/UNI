### Introduzione ai processi
Il processo è una cosa che ha degli stati
hanno dei limiti come il cambio di contesto nella sostituzione tra processi che ha un costo
si cerca di optare in una versione alleggerita dei processi i thread
come comunicano tra loro questi processi?
il s.o. come li deve gestire?
Lo scheduling attore fondamentale di una lezione prossima e decide chi deve andare in esecuzione

### Definizione di processo
non è solo un programma in esecuzione ma anche una serie di programmi in un processo
e una astrazione il processo
per fare l'astrazione abbiamo bisogno di un sistema operativo che
- astrae risorse
- contabilizza risorse
- limita le risorse
Il sistema operativo mantiene informazioni sulle risorse e sullo stato interno di ogni singolo processo del sistema, e tutte queste informazioni sono contenute in una tabella.

##### Il modello di un processo
>[!info] Quando abbiamo più processi da dover eseguire il SO, tramite la CPU, è in grado di passare da un processo all'altro in maniera molto repentina, dando l'idea che questi avvengano in parallelo.

Illusione come al cinema ovvero n fotogrammi che ci fanno sembrare che siano in movimento
foto con processi al fly
![[Pasted image 20241101152012.png|450]]

- Ogni processo ha una porzione specifica di memoria assegnata.
- Le frecce indicano il process switch, ossia il passaggio da un processo ad un altro. In questo modo noi abbiamo l'illusione che tutti i processi vengano svolti simultaneamente ma in realtà c'è un continuo switch repentino gestito dalla CPU.
- In questo esempio il PC(Program Counter) è uno solo.
![[Pasted image 20241101152308.png|250]]

### Processi concorrenti
Tutti i processi sono indipendenti e ognuno di loro ha una sua memoria separata astratta
ogni processo avrà a sua volta sotto processi
Quindi servono dei meccanismi per farli interagire tra loro e si va a creare una sorta di gerarchia(visibile con il comando `ps fux`)
La CPU, per poter switchare da un processo all'altro ha bisogno di salvarsi il PC e lo stato del processo corrente (quello che sta per finire) e ripristinarlo quando vuole riprenderlo.
Così tutti i processi possono progredire ma solo uno è attivo in un dato momento

#### Gerarchie di processi
Il s.o. quando viene avviato crea solo un processo chiamato `init` che rimane attivo fino allo spegnimento della macchina, questo processo `init` avrà a cascata tutti sotto processi
![[Pasted image 20241101153947.png|300]]
#### Creazione di un processo
ci sono degli eventi particolari che generano un processo
- inizializzazione del sistema
- Un processo in esecuzione che avvia una chiamata di sistema per creare un processo 
- `fork() chiamata di sistema per generare processi`
- Richiesta dall'utente di creare un nuovo processo
- Avvio di un job in modalità bash

>[!info]- spiegazione migliore di fork
>il comando `fork()` è una chiamata di sistema che permette a un processo (detto processo 
>padre) di creare una copia esatta di se stesso, creando così un nuovo processo (detto processo 
>figlio), il quale ha una copia del contesto del processo padre (inclusi i file aperti e l'ambiente). 
>Tuttavia, il figlio ha un proprio spazio di indirizzamento, quindi le modifiche alle variabili fatte dal 
>figlio non influenzano il processo padre, e viceversa; e anche un PID diverso.
#### Termine di un processo
Eventi tipici che terminano un processo in prospettiva di un processo
- Uscita normale(volontaria), semplicemente il processo termina di eseguirsi tipo alla fine di un main `return 0`
- A causa di un errore(volontario), si trova un errore e il processo decide di chiudersi
- A causa di un errore Fatale(involontario), Segmentation fault errori di programmazione esterni
- Ucciso da un altro proceso(involontario), Tipo `ctrl+c` che chiude il processo

#### Comandi di gestione dei processi
Sono chiamate di sistema
- fork 
	- concetto parent-child astrazione solo concettuale è una clonazione vera e propria che fa in modo che i processi siano uguali tranne alcune cose tipo il PID, non condividono informazioni tra loro per motivi di sicurezza(nei Thread invece lo fanno e si creano un po' di casini da gestire)
- exec 
	- ci fa eseguire nuovi processi usando fork
- exit 
	- causa terminazione volontaria del processo
- kill
	- invia un segnale, uno dei pochi meccanismi che fa comunicare tra processi
	- il segnale senza dettagli termina involontariamente il processo
#### Gli stati del processo
Tutto quel discorso che i processi si eseguono velocemente e si alternano ci rimanda agli stati di un processo
Rappresenta il modo in cui il s.o. gestisce in modo ottimale i processi con uno scheduler, ci sono tre stati:
- running, quando un processo è in esecuzione
- ready, quando è pronto per essere eseguito ma deve ancora essere messo in running
- blocked, quando è in blocco perché magari attende eventuali risorse
>[!info]- concetto di quanto di tempo
>rappresenta l'intervallo massimo di tempo assegnato a ciascun processo o thread in un sistema multitasking


![[Pasted image 20241101162437.png|500]]
#### Informazioni per un singolo processo
Un singolo processo ha queste informazioni memorizzate nella tabella dei processi del SO: 
- PID, UID, GID 
-  Spazio degli indirizzi di memoria 
-  Registri hardware (program counter) 
-  File aperti 
- Segnali Interrupt
#### Comunicazione tra processi
l'unico modo che i processi hanno di comunicare è attraverso i segnali o gli interrupt
###### differenza tra i due
- i segnali sono eventi di natura software generati da un processo o dal s.o.
	- gestione personalizzata o comportamenti predefiniti
	- il fatto che siano gestibili facilmente posso creare delle cose eccezionali ovvero fuori dalla volontà del processo e asincroni(arrivano in ogni momento)
	- i segnali sono una modalità di comunicazione 
	- ci sono questi signal handler che dicono a un determinato processo come si deve comportare in base a un determinato segnale (anziché dire chiuditi e basta)
- interrupt indica quei segnali al livello hardware
	- spesso hanno alta priorità
	- il s.o. li gestisce
	- viene chiamato lo scheduler che toglie dalle palle il processo in esecuzione e da priorità al processo che gestisce l'interrupt
	- frequenza del clock necessaria per implementare interazioni

- asincrono quando voglio lo faccio
- sincrono devo farlo subito
#### Come funzionano questi interrupt?
Ogni volta che avviene un interrupt c'è un gestore degli interrupt al livello hardware che controlla periodicamente se si sta generando un input hardware e fornisce l'informazione allo scheduler per deallocare la CPU e metterla a lavorare sul processo generato da un interrupt
##### Tabella interrupt vector
un vettore che contiene tutte le varie informazioni di ciascun dispositivo di I/O e le varie linee di interrupt(dove sono posizionate)
- L'interrupt vector è parte della tabella dei descrittori di interrupt(IDT)
	- al suo interno abbiamo il primo indirizzo della prima procedura che dice al s.o. come gestire l'interrupt
- gestore di interrupt o interrupt handler che continua l'esecuzione

#### <span style="background:#9254de">Passaggi che fa un s.o. ad un livello basso per gestire un interrupt</span>
![[Pasted image 20241102094402.png]]
UN PROCESSO NON PUO CEDERE LA CPU A UN ALTRO PROCESSO DEVE FARLO SOLO DELLO SCHEDULER NEL S.O.

##### Tipi di segnali:
ci sono due tipi di  segnali hardware e software
![[Pasted image 20241102101133.png]]
se premo x mi chiede di salvare
se premo termina attività esplode tutto
###### Passaggi di un segnale
1. il kernel invia un segnale(come abbiamo detto i segnali sono software)
2. viene interrotto il codice in esecuzione perché così si gestisce il segnale
3. Salvo il contesto, ovvero il punto in cui mi sono fermato nel codice
4. Viene eseguito il codice di gestione del segnale
5. Si ritorna al contesto originale

quindi ci sono segnali che chiedono di chiudere invece altri che fanno esplodere tutto
- interruzione immediata
- terminazione controllata
### Thread
- è una parte astratta del processo
- prendi un precesso e lo spezzi in sotto processi che hanno compiti
per ora abbiamo visto:
- un processo->1 thread
ora però approfondiremo invece multithread execution:
- 1 processo-> N thread
![[Pasted image 20241102104147.png|400]]
<font color="#e36c09">lightweight processes</font>, consentono una maggiore efficienza alleggerendo i singoli sottoprocessi(Thread) 
![[Pasted image 20241102102402.png|400]]
- un thread gestisce una tastiera
- un thread il disco
- e uno il software
Problema di eseguire queste istruzioni così al fly senza dividere in più processi e che possono esserci sovrascrizioni di variabili, questa cosa va a discapito del programmatore
<font color="#e36c09">ESEMPIO SERVER CON MULTITHREAD</font>
![[Pasted image 20241102102823.png|500]]
==i thread condividono stessa tabella del processo?==
Il cambio di contesto costa un botto è il male assoluto
###### Caratteristiche sui thread
- ogni thread sarà nello stesso spazio degli indirizzi di un singolo processo
- Gli scambi di informazioni avvengono tramite i dati condivisi tra thread
- Ogni thread ha
	- il proprio stack
	- i propri registri hardware 
	- il proprio stato
- Tabella dei thread con anche la sua tabella degli interrupt
- Ciascun Thread può chiamare qualsiasi chiamata di sistema supportata dal sistema operativo per conto del processo di cui è figlioccio
- Ogni Thread ha i suoi elementi privati(Stack) e i suoi elementi condivisi(Variabili globali)
![[Pasted image 20241102104121.png|200]]

#### I THREAD IN POSIX
<font color="#d83931">CHIEDE A ESAME</font>
![[Pasted image 20241102104411.png|400]]
Il thread e addestrato per fare un lavoro quindi praticamente esegue una funzione tipo in c

###### Implementazione dei thread nello spazio utente
un thread potrebbe essere definito o gestito nello spazio utente, oppure può gestirli il kernel quando magari deve fare particolari chiamate di sistema
![[Pasted image 20241102104903.png|600]]
>[!info]- approfondimento sui thread al livello utente
>PRO:
>- sono gestiti dal kernel come dei processi a singolo thread anche se sono più thread
>- gestiti tramite libreria e possono anche essere eseguiti da s.o. che non supportano i thread
>- Ogni processo che usa thread a livello utente necessita di una propria tabella dei thread per tracciare lo stato e altre cose
>- Non è richiesto un cambiamento di contesto completo perché sono tutti sotto lo stesso processo
>- Offrono maggiore scalabilità e personalizzazione dell'algoritmo di scheduling
>Contro:
>- se uno fa una chiamata di sistema bloccante tutti i Thread vengono fermati, questa cosa accade anche in caso di errori, perché vengono visti come un singolo individuo e quindi il s.o. potrebbe fermarli tutti
>- I thread nello spazio utente non hanno interrupt del clock quindi non possono fare round robin
>- Sebbene più veloci i Thread al livello utente non sono adatti per applicazioni che si bloccano spesso come i web server

>[!info]- approfondimento su Thread nello spazio kernel
>- Il kernel che gestisce i thread elimina la necessità di avere un sistema run-time per processo
>	- per sistema run-time si intende un sistema che compila e interpreta esegue ecc... se ho
>	   tutto nel kernel non ho bisogno di avere sistemi particolari per fare chiamate di sistema
>	   perché siamo già vicini al kernel
>- Le chiamate che potrebbero bloccare un thread vengono implementate come chiamate di 
>   sistema e quindi non avrò più quei blocchi
>- Riciclo dei thread per ridurre i costi
>- Programmazione con thread richiede cautela per evitare errori

>[!info]- approfondimento su Thread con sistema ibrido
>Alcuni sistemi effettuano un multiplexing dei thread utente su thread del kernel (praticamente 
>sceglie chi usare)
>Maggiore flessibilità per i programmatori che possono scegliere quanti thread usare in spazio 
>utente e quanti in spazio kernel
>Il kernel è a conoscenza solo dei suoi thread nello spazio kernel
>Ogni thread del kernel può gestire però i thread a livello utente anche se il kernel non li conosce
>![[Pasted image 20241102111832.png|500]]

Problemi sui thread: conflitti, sovrascrizione, problemi di implementazione anche di buffer ecc...


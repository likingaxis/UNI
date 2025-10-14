>[!question]- lista di domande
># DOMANDE
> 
> 1. **Si definisca il concetto di memoria virtuale e si descriva il ruolo del sistema operativo nella gestione delle pagine di memoria. Qual è l’effetto di un page fault sulle prestazioni del sistema?**
> >[!done]- la risposta
> >
> 2. **Si esamini la struttura di un sistema operativo monolitico. Quali sono i vantaggi e gli svantaggi rispetto a un microkernel?**
> >[!done]- la risposta
> >un sistema operativo monolitico è usato ad esempio nei sistemi UNIX, esso presenta un unico codice, è molto veloce ma allo stesso tempo è decisamente contorto poiché si trova tutto in un unico posto, ciò causa problematiche di manutenzione e aggiornamento. un sistema monolitico viene spesso usato quando è difficile disaccoppiare i vari codici, quindi ognuno di loro è strettamente dipendente da altro.
> >nei sistemi monolitici abbiamo le librerie condivise, in windows sono le DDL in UNIX si chiamano shared library, che consentono di non riscrivere mille volte lo stesso codice. il microkernel ha come vantaggio quello di essere molto più sicuro poiché si basa su un sistema client-server dove le varie chiamate di sistema avvengono attraverso dei messaggi condivisi tra le varie parti, il kernel ha l'essenziale per funzionare e tutto il resto è su più livelli, ciò aumenta di molto la sicurezza ma rallenta la velocità e l'implementazione è più difficile
> 2. **Si analizzi il concetto di containerizzazione. In che modo i container differiscono dalle macchine virtuali e quali sono i vantaggi di questa tecnologia?**
> >[!done]- la risposta
> >i container sono una sorta di mini sistema operativo che ha l'essenziale per far funzionare un determinato software, essi hanno un gestore dei container che è in grado di farci eliminare o modificare i container a nostro piacimento. Il container già in fase di installazione ha tutto il necessario per far eseguire quel software e sono molto più leggeri di una normale macchina virtuale che invece spesso è di tipo general purpose
> 4. **Si spieghi il concetto di least authority in un sistema operativo. Come questo principio migliora la sicurezza del sistema?**
> >[!done]- la risposta
> >il concetto di least authority prevede che un processo ha accesso e può controllare solo ciò di cui ha bisogno per funzionare, ciò aumenta la sicurezza di molto
> 5. **Si analizzi il concetto di hypervisor in un contesto di virtualizzazione. Quali sono le principali differenze tra un hypervisor di tipo 1 e uno di tipo 2?**
> >[!done]- la risposta
> >gli hypervisor sono degli applicativi che mettiamo per tradurre le operazioni di un sistema operativo in modo che le possano comprendere i livelli sottostanti
> >ci sono due tipi di hypervisor uno con e l'altro senza
> >- di tipo 1 è un software direttamente collegato all'hardware e traduce le istruzioni dei sistemi operativi soprastanti per rimandarle all'hardware. è molto più veloce ma è più difficile da implementare
> >- di tipo 2 è senza hypervisor effettivo, è un software che si esegue al di sopra di un s.o. general purpose, questo software prende le istruzioni dei s.o. sopra e le traduce in modo che il s.o. sottostante le comprenda, poi sarà lui a eseguirle comunicando con l'hardware. Alcuni di questi tipi presentano dei collegamenti diretti con il kernel
> 6. **Si inviti il candidato a discutere il ruolo e l’importanza delle librerie condivise in un sistema operativo UNIX. Come le librerie dinamiche riducono l’uso della memoria e migliorano l’efficienza del sistema?**
> >[!done]- la risposta
> >ho risposto prima
### Chiarimento prima della lezione
Prima di iniziare a riassumere la lezione 3 volevo spiegare una volta per tutte e in modo corretto cosa è il kernel
>[!tip]- definizioni e chiarimenti
>Il kernel è un codice che consente attraverso le sue funzioni(chiamate di sistema) di gestire le risorse hardware e fare da intermediario con i software che stanno al di sopra
>
>- Il s.o. aggiunge oltre alle cose del kernel eventuali interfacce grafiche, driver e varie utility
>- Il s.o. raccoglie anche il kernel al suo interno 


### STRUTTURA DI UN SISTEMA OPERATIVO DI TIPO MONOLITICO
Qui il s.o. viene eseguito come un singolo programma in modalità kernel

>[!question]- quando un kernel si dice monolitico?
>Quando tutte le funzionalità del kernel sono scritte in un unico spazio di indirizzamento, tutte le funzioni sono connesse tra loro e possono chiamarsi a vicenda, ciò permette maggiori performance ma porta difficoltà in termini di
>- manutenzione
>- dimensioni del kernel

>[!question]- Perché i sistemi monolitici sono stati fatti così in modo contorto?
>Perchè è molto complicato disaccoppiare un software, processo ecc..
>Disaccoppiare significa creare un codice che non abbia dipendenze da altre risorse del sistema e che quindi sia modulare

Questo sistema monolitico crea un Trade-off tra complessità e flessibilità 
Una via di mezzo tra cattive implementazioni e buone implementazioni

Ricordare che se viene aggiunto un pacchetto al kernel è necessario il riavvio della macchina, alcune volte no ma per la maggior parte delle cose si
###### Considerazioni sulla struttura monolitica
- Se ci sono dei moduli che dipendono uno dall'altro si ha comunque un sistema operativo monolitico, anche se non sono per forza scritti in un unico spazio di indirizzamento
- mancata presenza di isolamento delle diverse parti del sistema
- Presenza di una struttura a tre strati con il trap che consente la comunicazione tra questi livelli
	- user mode
	- kernel mode
	- Hardware
- Estensioni caricabili, carichi dinamicamente roba come driver ecc, funziona anche in un sistema monolitico
- Per aggiornare alcuni driver bisogna riavviare, poiché alcuni sono bloccati fino al riavvio per evitare modifiche che apportano a danni
- Presenza di Librerie condivise tra più programmi riduce copie multiple dello stesso codice in memoria
	- Windows: DDL(Dynamic Link Libraries)
	- UNIX: Librerie condivise


##### STRUTTURA DI UN SISTEMA OPERATIVO MONOLITICO
Per rappresentare un sistema monolitico con gerarchia venne usato il sistema THE 
con livelli che gestivano l'allocazione del processore, la memoria, la comunicazione, l'I/O, I dispositivi e gli utenti
>[!quote] di solito il singolo livello può parlare solo con chi gli sta sopra e chi sotto sennò sarebbe un puttanaio

![[Pasted image 20241018132619.jpg|400]]
Questo sistema venne usato da MULTICS anche se ideato per uno scopo educativo, aveva più programmi che lavoravano singolarmente senza darsi fastidio tra loro e usava degli anelli per definire i privilegi(più eri dentro agli anelli più avevi privilegi)
Con queste strutture si definivano meglio I compiti e aumentava la protezione delle risorse
###### RAPPRESENTAZIONE MENO STILIZZATA DI UN S.O. MONOLITICO
![[Pasted image 20241018133308.jpg|500]]
- Kernel Unificato: tutte le funzionalità sono centralizzate in un unico kernel
- Interconnessione: Ogni componente può chiamare qualsiasi altro componente
- Scalabilità: eccessivamente contorto al livello di codice e quindi un po' rognoso da scalare
##### MACCHINE VIRTUALI
>[!question]- cos'è una macchina virtuale?
>Permette l'esecuzione di più sistemi operativi su un unico hardware fisico, simulando un
>ambiente separato per ciascuno di essi

Virtualizzare una macchina significa aggiungere uno strato aggiuntivo per cui chi è sopra pensa di parlare con l'hardware ma invece sotto sono presenti altri elementi
- tipo 1.a sotto c'è un hypervisor software direttamente attaccato all'hardware che esegue e traduce direttamente le istruzioni di un sistema e gestisce le macchine virtuali superiori, una volta che viene eseguito si prende lui la briga di fare tutto
- tipo 2 senza hypervisor, uso un sistema operativo nato per essere generalista e sopra metto una app che esegue e traduce le operazioni sopra o sotto
	- b. È un software che traduce semplicemente le istruzioni in un linguaggio che puo' capire il s.o. sottostante, questa cosa è più lenta dell'hypervisor di tipo 1 ma è piu' semplice da applicare
	- c. Molto simile al tipo b ma ha un accesso diretto al livello kernel con un modulo e quindi molte risorse le prende direttamente senza essere schermato dal s.o. sottostante, ciò gli consente di fare chiamate di sistema direttamente al livello kernel
![[Pasted image 20241018150141.jpg|450]]

Ovviamente aggiungere uno strato porta a una diminuzione delle performance

>[!quote] consiglio dal prof per scegliere una versione di un sistema operativo 
>LTS=Long Term Service, versioni affidabili e durature
### CONTAINER
I container è un metodo di virtualizzazione che permette di eseguire applicazioni in ambienti isolati e condividere il kernel e le librerie con il sistema operativo host
È un processo a sé e contiene solo ciò di cui si necessita senza avere un completo s.o. 
Infatti I container possono eseguire dei "mini sistemi operativi" ovvero istanze di un sistema operativo 
Invece di installare sulla macchina app che richiedono librerie da scaricare ecc appesantendo il s.o. basta prendere questo container preassemblato con tutto ciò di cui si ha bisogno
Si usano i container poiché sono istanze complete già con librerie per eseguire l'app
Esiste il gestore del container che gestirà tutti i container che possono esplodere con un click
Quasi tutte le funzionalità di Google si installano con container di tipo docker
![[Pasted image 20241018164822.png|500]]
#### EXOKERNEL
Non emula l'hardware sottostante ma dà accesso diretto alle macchine virtuali al di sopra però limitando e gestendo notevolmente le risorse in modo che siano spartite nel modo corretto
Garantisce maggiore sicurezza e maggiori performance
Una GPU può usare solo 8 GB di Vram
#### UNIKERNEL
Sono sistemi minimi basati su LibOS progettati per eseguire solo un'applicazione su una macchina virtuale
Non sono general purpose, ma mettono a disposizione poche funzionalità per la singola applicazione
Ha completo accesso almeno all'utente del server
Vengono spesso usati per app come server web
Togliendo funzionalità al s.o. potrei renderlo più sicuro e leggero
## STRUTTURA DI UN SISTEMA OPERATIVO BASATO SU CLIENT-SERVER MICROKERNEL
Le chiamate di sistema si basano su dei messaggi inviati tra le componenti del kernel
Kernel semplificato
Le Service procedure vengono chiamate non nel kernel ma al livello utente
>[!tip]- concetto di least autority
>Ogni processo del s.o. può fare solo ciò che serve per svolgere il compito

Queste comunicazioni non avvengono in una rete ma all'interno del s.o.
![[Pasted image 20241018162206.jpg|400]]
Visto che nella struttura interna del kernel c'è poco e niente ed è tutto al livello user si aumenta di molto la sicurezza del sistema poiché è difficile accedere alla parte sottostante che ha poco e niente
Il passaggio di messaggi è più lento 


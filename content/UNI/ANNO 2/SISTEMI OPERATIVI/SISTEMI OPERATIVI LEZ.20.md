Nella scorsa lezione abbiamo parlato dei dispositivi di I/O ora parleremo dei software che li gestiscono
### Come deve essere il software di I/O
- indipendente dal dispositivo
	- un programma che legge un file deve funzionare se uso ssd o usb
- denominazione uniforme
	- i nomi dei file devono essere indipendenti dal dispositivo e devono essere stringhe o numeri
	- ad esempio in UNIX per andare su un file non ci indirizziamo al dispositivo con `ST6NM04` ma usiamo ad esempio `/mnt/movies` rispettando la gerarchia del file system
- Gestione degli errori
	- il software di I/O deve gestire gli errori piu vicino possibile all'hardware al livello di controller per gestirlo adeguatamente
		- errori transitori: errori di fisica del mondo delay roba elettronica ecc...
- trasferimenti sincroni o asincroni
	- I/O fisico è quasi sempre asincrono, i dati arrivano come arrivano. 
		- siamo noi con i software che li trattiamo in modo bloccante dandogli del tempo
		- il sistema operativo deve rendere sincrone e bloccanti le cose asincrone
		- il DMA viene gestito dal s.o.
- buffering dal software
	- non tutto può essere trasmesso subito e bisogna sfruttare un buffer temporaneo per spostare tutto poi interamente
	- con dispositivi che hanno vincoli real-time ce ne accorgiamo perchè ci sono vincoli sulle prestazioni, un buffer potrebbe comportare a delle attese maggiori 
- dispositivi condivisibili o dedicati
	- i dischi sono  a volte condivisi da più utenti
	- stampanti o scanner sono dedicati per la maggior parte dei casi
	- il sistema operativo deve evitare deadlock
### Tipologie di software per I/O
#### I/O programmato
La CPU gestisce tutto il processo di trasferimento dei dati
I/O viene gestito dal programma
ESEMPIO:
- un utente vuole stampare "ABCDEFGH" 
- abbiamo questa stringa in un buffer nello spazio utente 
- effettuo la chiamata di sistema per stamparlo
- copio questa stringa nello spazio kernel
- invio i caratteri uno per volta alla stampante aspettando che sia pronta a riceverne uno nuovo
###### POLLING O BUSY WAITING
Questa attesa data dal fatto che il s.o. deve andare a controllare il registro di stato della stampante per vedere se può inviare un nuovo carattere si dice 
- ciclo di polling
	- controllo periodico dello stato di un dispositivo o di una condizione
	- prevede delle pause quindi non ruba tutta la CPU
oppure
- busy waiting
	- simile a quello sopra ma non prevede pause senza però rilasciare la CPU
>[!info]- differenza tra busy waiting e cycle stealing
>- il busy waiting riguarda il controllo di variabili o dispositivi
>- il cycle stealing riguarda un dispositivo che ruba cicli alla CPU per accedere ai bus di trasferimento dati al posto di farlo usare dalla CPU

![[Pasted image 20250114160131.jpg|500]]

### Codice che usa stampante 1

![[Pasted image 20250114160453.jpg]]

- devo copiare dal buffer utente al buffer kernel `copy_from_user()`
- controllo e attendo disponibilita della stampante con un while che confronta il registro
- invio i vari caratteri al registro della stampante
>[!bug] problema del codice:
>il while crea un busy waiting

### Codice che usa stampante 2
![[Pasted image 20250114165521.jpg|400]]
![[Pasted image 20250114165545.jpg|400]]
Questo codice ottimizza le cose 
- copio il buffer utente in uno del kernel
- abilito gli interrupt che verranno utilizzati dalla stampante
- attendiamo che il registro della stampante sia pronto
- scrivo il primo carattere in assoluto
- passo il controllo a un altro processo chiamando lo scheduler
- la stampante invia un interrupt al processo  quando ha finito di scrivere il primo carattere e riprende l'esecuzione del processo
	- in sostanza gli dice "ne hai altri?"
- il processo lo verifica con count 
	- se sono finiti sblocca il processo utente "padre" ovvero quello che chiama il processo di stampa
	- viene sbloccato con `unblock_user()`
- se count non è 0
	- scrive la posizione i del buffer nel registro della stampante `*printer_data_register`
	- decrementa count perché inserisce un elemento
	- incrementa l'indice del buffer
- `akcknowledge_interrupt()` serve per dire alla stampante quindi a chi ha inviato l'interrupt che esso è stato gestito correttamente
- `return_from_interrupt()` fa riprendere alla CPU altre operazioni
ogni volta la stampante invierà interrupt il che è un <font color="#c0504d">problema</font>
### altrimenti uso il DMA gli invio tutto a lui e gli dico "cazzi tuoi"
il DMA riduce significativamente il numero di interrupt
la CPU fa un interrupt al DMA e gli dice che se la deve gestire lui
scambia le informazioni con la stampante
il DMA prende il buffer dal kernel 
restituisce allo `scheduler()`
il DMA invia un interrupt una volta finito 
fa i vari unblock ecc...
![[Pasted image 20250114190440.png|500]]
>[!tip]- chiarimento spicciolo
>in poche parole questo processo sposta il buffer nel kernel e fa fare tutto al DMA una volta che il DMA ha finito dice al processo che l'ha chiamato e restituisce tutto il controllo alla CPU

#### Struttura del software di I/O
![[Pasted image 20250114191202.png|500]]
ho quattro livelli che caratterizzano il software di I/O
ora studieremo i gestori degli interrupt -> 
### Gestori degli interrupt
- devo bloccare i driver fino al completamento dell'I/O
	- i driver devono essere usati da un dispositivo alla volta, c'è una sorta di semaforo
	- l'altra cosa è che ci deve essere la possibilità di bloccarli per sincronizzare lo scambio di informazioni
- gestione degli interrupt complesso
	- poiché bisogna salvare vari registri per poi riprendere quella determinata esecuzione, impostare contesti e usare controller degli interrupt
- impatto sulla memoria virtuale bisogna gestire ==TLB== ==MMU== e ==cache== per i dispositivi che le usano
	- vedi [[SISTEMI OPERATIVI LEZ.14]]
	- gestirli aumenta l'uso della CPU
- tutta questa roba richiede numerosi cicli della cpu
#### Cosa succede al software quando arriva un interrupt
punti molto generali
- salvo tutti i registri
- imposto il contesto con tabelle TLB MMU ecc...
	- imposto il contesto significa che mi preparo per gestire l'interrupt
- impostare lo stack, vado a posizionare il program counter sulle istruzioni per eseguire la procedura
- confermo al controller degli interrupt e riabilito l'interrupt
	- così posso mandare altri interrupt tipo CTRL+C
	- altrimenti non potrei inviare l'interrupt di terminazione della procedura
	- confermo al controller che l'interrupt è stato preso in carico
- visto che il processo è interrotto copiamo i suoi registri ecc... nella tabella dei processi
- eseguo la procedura di servizio dell'interrupt 
	- ora finalmente eseguo il codice dell'interrupt
	- Ad esempio, invia un nuovo carattere alla stampante
- determina quale processo eseguire come successivo o con alta priorità o quello che era stato bloccato dall'interrupt chiamato prima
- reimposto il nuovo contesto del processo con le varie tabelle MMU TLB ecc...
- Carico i nuovi registri come il PSW che contiene i bit di condizione ecc...
- avvio il nuovo processo

#### DRIVER DEI DISPOSITIVI
Ora ci troviamo ad un livello superiore quello dei driver dei dispositivi
i driver sono dei codici specifici per ogni dispositivo, lo gestiscono tramite i suoi registri.
Al più i driver gestiscono una classe di dispositivi correlati tra loro ma spesso sono unici per ogni dispositivo.
Tecnologie come USB utilizzano una pila di driver per gestire vari dispositivi
I DRIVER della tecnologia USB sono divisi in 3 livelli
- Livello base: Gestisce I/O seriale e questioni hardware
- Livelli superiori: trattano pacchetti per lo scambio di dati e funzionalità comuni
- API di alto livello: le varie interfacce dei dispositivi

#### Posizionamento nel Kernel
I driver di solito sono al livello Kernel per accedere meglio ai vari registri del controller del dispositivo

>[!bug] Se fossero messi nello spazio utente?
>- più facili da installare e mettono meno a rischio il sistema operativo
>- MA sono più lenti (devono passare allo spazio Kernel per ogni operazione)

#### Funzionalità e interfaccia dei driver dispositivo
![[Pasted image 20250116163956.png|500]]

I driver per essere installati vengono visti come dei veri e propri dispositivi
e vengono classificati in:
- A BLOCCHI: si leggono sequenzialmente, contengono blocchi di dati, e spesso sono dischi
- A CARATTERI: generano o accettano flussi di caratteri tipo stampanti o tastiere
alcuni driver nel passato erano caricati direttamente in binario nel s.o. ora vengono caricati in modo dinamico

### Implementazione e complessità dei driver di dispositivo
###### Funzioni
I driver svolgono diverse funzioni tra cui
- gestioni di lettura e scrittura
- inizializzazione del dispositivo 
- gestione dell'alimentazione 
- registrazione degli eventi e attività
###### Processo generale
Per assicurare una corretta comunicazione tra hardware e software, il driver esegue una serie di operazioni
- verifica la validità dei parametri di input ricevuti dal SO o dall'utente
- traduce i parametri in comandi compatibili col dispositivo
- gestisce l'utilizzo del dispositivo

###### Gestione di I/O e errori
I driver devono anche gestire efficientemente l'I/O e prevenire errori critici, aspettando in alcuni casi un interrupt per completare l'operazione.

###### Complessità e rientranza
Per supportare un ambiente multitasking e garantire stabilità, i driver devono essere progettati con caratteristiche specifiche
- devono essere RIENTRANTI, ossia poter gestire più richieste simultaneamente (quelli di "RETI" sono così)
- devono permettere la connessione e disconnessione dinamica dei dispositivi (***HOT-PLUGGING***)
	- se un nuovo dispositivo viene aggiunto, deve inizializzarlo correttamente
	- se un dispositivo viene rimosso improvvisamente deve interrompere TUTTE le operazione e evitare tentativi di accesso
## Software di I/O indipendente dal dispositivo
Saliamo ancora di livello e arriviamo a dei software dal dispositivo
È un software universale per standardizzare la comunicazione tra hardware e applicazione utente
fungendo da intermediario e interfaccia.
Le sue funzioni chiave includono:
- Fornire un'interfaccia uniforme per diversi driver
- ottimizzare il trasferimento dei dati attraverso il buffering
- gestire e segnalare errori di comunicazione
- assegnare e rilasciare dispositivi dedicati agli utenti o ai processi
- standardizzare la dimensione dei blocchi di dati, indipendentemente dal dispositivo.

>[!question] Perché è utile avere uniformità con questo software?
>L'uniformità evita di dover modificare il SO ogni volta che viene introdotto un nuovo dispositivo.
>Avere un'interfaccia standard aumenta notevolmente l'efficienza.
>- (a) INTERFACCE DIVERSE
>- (b) INTERFACCE UNIFORMI
>![[Pasted image 20250116165456.png]]
### Implementazione e gestione dell'interfaccia dei driver
sono fondamentali per la comunicazione tra SO e dispositivi hardware
i driver contengono una tabella che ha riferimenti a funzioni specifiche 
- questa tabella viene usata dal SO per facilitare le chiamate indirette
	- le chiamate indirette esistono perché il SO non fa chiamate a funzioni direttamente al driver ma si serve di un puntatore quindi le fa in modo indiretto
Ogni dispositivo ha un nome simbolico (es. `/dev/disk0` in UNIX)
- per garantire la sicurezza vengono usati permessi tipo quelli dei file
il SO fornisce una interfaccia standard per i driver facilitando l'integrazione con nuovi dispositivi
### Buffering
![[Pasted image 20250116170331.png|300]]

##### Diversi scenari
il buffering è fondamentale e lo capiamo dall'esempio
###### Buffering visto in prospettiva di input
a) Esempio di lettura dati da un modem VDSL senza uso di buffer richiede un riavvio del processo 
    utente per ogni carattere ricevuto
b) Miglioramento con buffer nello spazio utente il processo fornisce un buffer, questo processo si  
	riavvia solo quando il buffer risulta pieno
c) Problemi di paginazione e soluzione con buffer nel kernel, stavolta il buffer è nel kernel
d) Doppio Buffer nel Kernel hai due buffer, uno accumula input mentre l'altro è in copia nello spazio utente

#####  Buffering visto in prospettiva di output
gli esempi a e b sono analoghi poi ci sono
- soluzione con buffer nel kernel copia nel buffer del kernel e sblocco immediato del processo utente
Il buffering multiplo può creare problemi in termini prestazionali
Si creano troppe copie del buffer prima al kernel poi al controller poi sulla rete ecc...
trasmettere tutti questi pacchetti può rallentare la velocità di trasferimento di essi
### Gestione degli errori di I/O del sistema operativo
si utilizzano codici di errori hardware o software
- per quelli software si intendono quelli di programmazione che ritornano un codice d'errore al chiamante del processo
- per quelli hardware li gestiscono i driver 
Esistono azioni che possono dipendere dal contesto
- di tipo interattivo se c'è un utente con cose tipo (riprova, ignora, termina...) per il croce sono inutili al cazzo
- non interattivi ritornano semplicemente il codice d'errore
- per strutture critiche se succede qualcosa si hanno dei codici d'errore
### Gestione dei dispositivi dedicati o esclusivi
- esclusivi ad esempio la stampante che può essere in teoria usata da un solo processo alla volta
	- Esiste un sistema che gestisce le richieste di uso del dispositivo
###### metodi di allocazione e rilascio
- approccio tradizionale
	- un processo fa open su file speciali che indicano il dispositivo e close per chiudere il dispositivo
- approccio alternativo
	- se la open non va a buon fine si mettono i richiedenti su una coda
##### Sistema di Spooling
>[!question] cosa significa
>è una tecnica per gestire i dispositivi dedicati in ambienti multiprogrammati evitando blocchi da parte di un solo processo
>- in poche parole serve per sincronizzarli in modo armonioso
>in modo pratico uso un daemon e una directory di spooling per ordinare e gestire i lavori di stampa
>![[Pasted image 20250116174346.png]]
>tutti questi sono i livelli del sistema di I/O
>le frecce indicano i flussi di controllo che attraversano i livelli

##### Uniformità nella dimensione dei blocchi dei dispositivi
le dimensioni fisiche variano a seconda dei dispositivi
- per questo usiamo un software che astrae la memoria così tutti risultano uniformi
Astrazione dei dispositivi in unici blocchi logici
i dispositivi che lavorano a caratteri trasmettono quantità di dati differenti, attraverso software si occulta questa cosa aumentando l'uniformità

#### Librerie di I/O nell'ambito utente
ci sono librerie che facilitano le chiamate di sistema tipo write in c
poi ci sono printf e scanf per facilitare le chiamate di sistema di input e output
queste librerie semplificano di molto la programmazione di I/O per lasciare ai programmatori spazio per pensare alla logica delle applicazioni e non perdere tempo su dettagli a basso livello




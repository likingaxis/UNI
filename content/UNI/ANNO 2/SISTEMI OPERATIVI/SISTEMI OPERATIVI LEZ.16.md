
Problemi di memorizzazione:
- come memorizzo i dati a lungo termine?
>[!bug] non con la ram

>[!success] con disco rigido o ssd (non volatili)
>- può essere visto come un insieme di blocchi di dimensione fissa
>- supporta operazioni di scrittura e lettura
>- possono essere accessibili dai processi in modo simultaneo

- dobbiamo garantire l'esistenza di un arbitro che
	- salva i dati
	- garantisce la persistenza dei dati nel tempo
	- facilita l'accessibilità ai dati e la protezione di essi
questo arbitro è il **file system**
#### il SO sfrutta i file systems
Sono un modo per memorizzare e organizzare le informazioni e sono:
- organizzate in file
- directory
- spesso chiamati NFTS, Ext4, APTFS 
Abbiamo delle astrazioni in termini di interfaccia utente e implementazione tecnica
- l'utente vedrà solo le operazioni consentite e i file
- il progettista vedrà tutte le strutture interne

Esistono standard per garantire portabilità dei file system, così le chiavette funzionano sulla maggior parte dei dispositivi ecc...
#### Roadmap
Descrive il processo di accesso ai file a un Sistema Operativo

![[Pasted image 20241212190804.png]]
- possiamo vedere qui un esempio dove lo user chiede un determinato file
-  il sistema operativo interagisce con il file system per localizzare e leggere quel file
	- il **<font color="#4f81bd">virtual file system</font>** ci consente di vedere ogni file system in modo virtuale così che esso sia astratto e uguale per ogni implementazione
	- una **<font color="#4f81bd">page cache</font>** per velocizzare i lavori, salvando le varie pagine viste più frequentemente
	- esistono diversi **<font color="#4f81bd">driver</font>** per ogni tipologia di file system, convertono i comandi astratti del virtual file system in una cosa più specifica
	- **<font color="#4f81bd">buffer cache</font>** per fare il trasferimento in modo ottimizzato e rapido delle informazioni
#### definizione di file 
metodo di astrazione per salvare e leggere informazioni su disco semplificando la lettura, altrimenti sarebbero tutti 0 e 1
- ogni file ha un identificativo, un nome che per ogni SO deve rispettare dei criteri
	- In MS-DOS potevo avere 8 lettere per identificativo del file
		- ora possiamo mettere quello che ci pare con solo limiti nei formati(no caratteri speciali)(Case sensitivity),Linux e case sensitive
- il s.o. crea un ponte tra quel descrittore e quella sequenza di bit in disco
- Esistono due file
	- binari, non capibile a meno che sei matrix
	- testuali, sempre binario ma tradotto facilmente da un essere umano
- Estensione dei file, non necessaria in UNIX ma tipo .mp3, .txt ecc...
Linux se ne fotte ed e a carico nostro aprire una app corrispondente a quel file
- GNOME esiste e consente di rimandare a una determinata estensione ma è un software esterno
### ABBIAMO 3 TIPI DI STRUTTURE FILE
- <font color="#f79646">a)</font> Sequenza non strutturata di Byte che deve essere gestita e ricostruita dai software utente
	- <font color="#c0504d">(non dal SO)</font>
- <font color="#f79646">b)</font> una sequenza strutturata di Byte che andavano lette una alla volta in memoria(Nastri) 
	- supporto in cui erano scritti i vari record
- <font color="#f79646">c)</font> Struttura organizzata, i dati venivano visti come record organizzati da una struttura ad albero, ogni record aveva le sue chiavi, principalmente usato nei mainframe
![[Pasted image 20241212193435.png|500]]
##### DI COSA ABBIAMO BISOGNO PER GESTIRE TUTTA STA MERDA?
- file e cartelle normali(Come ASCII e Binari)
	- file di uso comune dagli utenti come foto video ecc 
	- cartelle di uso comune che consentono la gestione dei vari file
		- (anche le cartelle sono file in linux)
-  Tipi di file speciali
	-  A caratteri: usati per dispositivi che lavorano con byte, periferiche I/O ecc...
	- A blocchi: File usati per astrarre i vari dispositivi che consentono l'accesso ai dati come dischi ecc...

#### File eseguibili 
File speciali che contengono una sequenza di byte eseguibile dal sistema operativo con formati specifici
Come è fatto?

![[Pasted image 20241212194542.png|200]]
- **Intestazione (Header)**
	- **Numero magico**: specifica il tipo di file e se è eseguibile o meno 
	- **Dimensioni varie** (testo, dati, BSS, ecc.)
	- **Punto di ingresso**: l'indirizzo da cui il SO deve iniziare l'esecuzione (main)
	  - **Flag**: varie proprietà o comportamenti speciali del file
	- Testo e dati
		- **Testo**: parti del programma caricate e rilocate in memoria (il codice macchina eseguito dal processore)
		- **Dati**: contiene le variabili globali/statiche
	- **Tabella dei simboli**
		- Utilizzata per il debug

##### File di archivio
Un **file di archivio** come quelli creati con **`tar`** (acronimo di "tape archive") è un contenitore che raccoglie più file e directory in un unico file

![[Pasted image 20241212195906.png|300]]
Intestazioni dei moduli: 
- nome
- data di creazione
- proprietario
- codice di protezione
- dimensione 
<font color="#c0504d">Non sono leggibili dall'utente perché sono in formato binario e stamparli produrrebbe caratteri incomprensibili</font>
>[!info]- Utility in UNIX sono una serie di euristiche che determinano il nome del file e tutte le sue info

#### COME SI ACCEDE A UN FILE
Ci sono due modi:
- Sequenziale, leggo i file in modo continuo, tipo su nastri(obsoleto)
- Casuale, Salto sul settore richiesto senza leggere sul tutto il file
	- Utilizzo di `seek` che indica la posizione da cui iniziare a leggere 

##### ATTributi dei file
ogni file ha i suoi attributi e metadati che indicano diverse informazioni
![[Pasted image 20241212201056.png]]

## Operazioni su file

| **Operazione**    | **Descrizione**                                                                                                                                               |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Create**         | Creazione di un file senza dati. Principalmente per «annunciare» la presenza del file e impostare alcuni attributi. Non aggiunge dati ma lo registra nel file system (istanza vuota). |
| **Delete**         | Eliminazione di un file per liberare spazio su disco. Dopo l'eliminazione, il file non è più accessibile.                                                    |
| **Open**           | Apertura di un file per caricare in memoria gli attributi e gli indirizzi del disco. Facilita l'accesso rapido in seguito.                                   |
| **Close**          | Chiusura del file per liberare spazio nelle tabelle interne del sistema operativo. Forza anche la scrittura dell'ultimo blocco.                              |
| **Read**           | Lettura dei dati da un file, generalmente dalla posizione corrente. Richiede un buffer per memorizzare i dati letti in RAM per velocità.                    |
| **Write**          | Scrittura di dati nel file, alla posizione corrente. Può ampliare il file o sovrascrivere i dati esistenti.                                                  |
| **Append**         | Aggiunta di dati solo alla fine del file. Usata come forma limitata di scrittura in alcuni sistemi operativi.                                                |
| **Seek**           | Riposizionamento del puntatore del file a una posizione specifica (per accesso casuale). Permette lettura o scrittura dalla posizione scelta.                |
| **Get Attributes** | Lettura degli attributi di un file. Necessaria per processi come il comando `make` in UNIX per la gestione dei progetti software.                           |
| **Set Attributes** | Modifica degli attributi di un file (es. modalità di protezione o flag), effettuata dopo la creazione del file.                                              |
| **Rename**         | Rinominare un file. Utile come alternativa alla copia ed eliminazione, specialmente per file di grandi dimensioni.                                           |

# Come cazzo si scrive e legge un file?
``` c
int fd=open("foo.txt",O_RDONLY);
char buf
```
Printa sullo stdout
Scrivere in binario e una sola perche dipende dal sistema operativo
scfrivere in leggibile gode
11_write and read posix
- 0644 diritti di accesso
# Come cazzo si copia un file?
le cartelle utilizzano i file
directory di lavoro dove sono le cartelle
3

## DIRECTORY
Sono file che tengono traccia di altri file in un file system
##### DIVISIONE A DUE LIVELLI:
##### A livello singolo:
![[Pasted image 20241213102805.png|300]]
Una sola directory detta ROOT che contiene tutti i file
usata nei dispositivi embedded
##### Multilivello:
Per motivi organizzativi si è deciso di creare una struttura gerarchica con cartelle e sottocartelle così da raggruppare e individuare meglio i file 
Esiste una ROOT directory che rappresenta l'inizio di ogni directory
![[Pasted image 20241213104047.png|500]]

### Come cazzo si trova una cartella?
#### Nomi di percorso assoluto Iniziano dalla root e conducono al file, <span style="background:rgba(240, 200, 0, 0.2)">sono unici per ogni file</span>.

- Unix/LINUX: <span style="background:rgba(240, 200, 0, 0.2)">root = /</span>
    
    - `/usr/hjb/mailbox`, indica il file `mailbox` nella directory `usr/hjb`
    
- Windows: <span style="background:rgba(240, 200, 0, 0.2)">root = C:</span>
    
    - `C:\Users\Samuele\Documents\sborra.txt`, indica il file `sborra.txt` nella directory `Documents`
#### Nomi percorso relativi **Non iniziano dalla root**, il percorso è basato sulla directory di lavoro dell'utente (corrente)

- `cp /usr/hjb/mailbox /usr/hjb/mailbox.bak` **percorso assoluto**
- `cp mailbox mailbox.bak` **percorso relativo**

Ogni processo ha una **directory di lavoro indipendente** che non influisce su altri processi o sul file system quando termina il suo lavoro. Le procedure di libreria impediscono il cambio di directory o la ripristinano (es. un file cambia temporaneamente directory e, una volta concluso, può ritornare a quella originale). Per rappresenrare posizioni relative all'interno della directory corrente si usa:

- `.`: directory corrente
- `..`: directory genitore
    
    - `cp ../lib/dictionary`: copia il file dictionary della `../lib` (genitore) alla directory corrente.
### OPERAZIONI SULLE DIRECTORY
##### Operazioni di base
| **Operazione**              | **Descrizione**                                                 |
| --------------------------- | --------------------------------------------------------------- |
| <center>`CREATE`</center>   | Crea una directory con le voci `.` e `..` predefinite.          |
| <center>`DELETE`</center>   | Elimina una directory (possibile solo se la directory è vuota). |
| <center>`OPENDIR`</center>  | Apre di una directory per leggerne il contenuto                 |
| <center>`CLOSEDIR`</center> | Chiude una directory dopo la lettura per liberare risorse       |
##### Lettura e modifica
| **Operazione**             | **Descrizione**                                                                          |
| -------------------------- | ---------------------------------------------------------------------------------------- |
| <center>`READDIR`</center> | Restituisce la prossima voce in una directory aperta senza esporre la struttura interna. |
| <center>`RENAME`</center>  | Rinomina una directory.                                                                  |
##### Linking e Unlinking
| **Operazione**               | **Descrizione**                                                                                                                                                                                            |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <center>`Link`</center>      | Crea un hard link (direttamente diretto a un file nel file system), collegando un file esistente a un nuovo percorso, condividendone l'***<span style="background:rgba(240, 200, 0, 0.2)">i-node</span>*** |
| <center>`Unlinking`</center> | Rimuove una voce dalla directory, cancellando il file se è l'unico link.                                                                                                                                   |

>[!lemma] I-node (lo vedremo meglio poi)
>Un I-node è una struttura dato che rappresenta un file o una directory. Contiene informazioni essenziali sul file (metadati) e puntatori ai blocchi di dati sul disco

**Link simbolici:** sono dei link speciali che puntano a diversi tipi di file e che vedremo meglio poi
## CREAZIONE DI ARCHIVI
Per creare un nuovo archivio Usiamo il comando tar che ormai sempre si utilizza insieme a gz che consente di comprimere l'archivio(tipo zip)

- `tar -czvf nome-archivio.tar.gz /percorso/della/cartellabash`

	- c: Crea un nuovo archivio. 
    
	- z: Comprimi l'archivio usando gzip. 
    
	- v: Visualizza un output dettagliato durante l'operazione. 
    
	- f: Specifica il nome del file di archivio.

## ESTRAZIONE DI ARCHIVI

- `tar -xzvf nome-archivio.tar.gz 

	- x: Estrai il contenuto dell'archivio. 
    
	- z: Decomprimi l'archivio usando gzip. 
    
	- v: Visualizza un output dettagliato durante l'estrazione. 

	- f: Specifica il nome del file di archivio.
## Esistenza di ZIP
Zip è più veloce e supportato da windows e mac
ma Tar.GZ comprime di più e mantiene le strutture interne meglio

Comandi con: 
- zip nome-archivio.zip file1 file2 
    
- unzip nome-archivio.zip

### Indice degli Argomenti
### **1. Definizione di Sistema Operativo**

- Scopo e semplificazione delle risorse hardware.
- Differenze tra software normale e sistema operativo.

### **2. Librerie**

- Funzione delle librerie per la semplificazione dello sviluppo software.

### **3. Storia e Generazioni dei Sistemi Operativi**

- Generazione anni '50: macchine specializzate.
- Generazione anni '60: mainframe e sistemi batch.
- Generazione anni '70: primi sistemi operativi (MULTICS, UNIX).
- Generazione anni '80: personal computer.
- Generazione anni '90: dispositivi mobili.

### **4. Componenti Hardware**

- Microprocessori e interazione con il sistema operativo.
- Processore: funzioni e registri principali.
- Memorie: caratteristiche e velocità.
- Dispositivi di Input/Output (I/O): struttura e funzionamento.

### **5. Concetti Fondamentali**

- Multiplexing: condivisione temporale e spaziale delle risorse.
- Tipi di sistemi operativi:
    - Mainframe.
    - Server.
    - Personal Computer.
    - Smartphone e tablet.
    - Sistemi embedded e IoT.
    - Sistemi real-time.
    - Smart card.

### **6. Concetti di Processo**

- Definizione e ciclo di vita di un processo.
- Alberi di processi e gerarchie.
- Layout della memoria di un processo (stack, heap, registri).

### **7. File e File System**

- Strutturazione e organizzazione ad albero.
- Accesso ai file: montaggio e utilizzo.
- Protezione dei file tramite permessi (read, write, execute).

### **8. Chiamate di Sistema**

- Funzionamento e scopo delle chiamate di sistema.
- Tipi di file speciali per dispositivi hardware.

### **9. Strutture di Sistemi Operativi**

- Sistemi monolitici.
- Microkernel e client-server.
- Virtualizzazione (macchine virtuali e container).

### **10. Introduzione a Linux e Bash**

- Storia di Linux.
- Comandi di base e scripting.
- Gestione di variabili d'ambiente e file di configurazione.

### **11. Approfondimenti su Comandi Linux**

- Utilizzo di comandi come `grep`, `awk`, `cat`, `tail`.
- Visualizzazione e modifica di file (`sed`, `sort`).

### **12. Segnali e Gestione dei Processi**

- Comunicazione tra processi.
- Utilizzo di `kill`, `nohup`, e gestione dei job.

### **13. Navigazione nel File System**

- Struttura delle directory principali (es.: `mnt`, `root`, `usr`, `bin`).
- Comandi di base:
    - `pwd`, `cd`, `ls` (con opzioni).
    - Copia e spostamento (`cp`, `mv`).
    - Identificazione file (`file`, `tac`).
- Permessi di accesso:
    - Concetti di `chmod` e mapping permessi (lettura, scrittura, esecuzione).

### **14. Gestione dei Processi**

- Comandi per visualizzare processi (`ps`, `top`).
- Interazione con i processi:
    - Esecuzione in foreground e background.
    - Uso di `nohup` e `screen` per processi persistenti.
- Segnali e gestione:
    - `kill`, `SIGINT`, `SIGKILL`.

### **15. Creazione e Gerarchia dei Processi**

- Il modello di un processo:
    - Differenza tra `fork` ed `exec`.
    - Stato dei processi (`running`, `ready`, `blocked`).
    - Gestione delle risorse tramite PID, UID, GID.
- Chiamate di sistema per i processi:
    - `wait`, `execv`.

### **16. Thread**

- Introduzione ai thread:
    - Differenze con i processi.
    - Condivisione di memoria tra thread.
- Implementazione dei thread:
    - Thread in spazio utente e kernel.
    - Approcci ibridi.
    - Pro e contro della programmazione multithread.

### **17. Chiamate di Sistema (Syscall)**

- Differenza tra:
    - Librerie standard (`libc`), `unistd.h`, `syscall.h`.
- Esempio di chiamate di sistema:
    - Stampa con `write`.
- Passaggi della chiamata `read` da libreria a kernel.

### **18. Segnali e Interruzioni**

- Funzionamento dei segnali:
    - Signal handler e tipi di segnali.
    - Uso di `alarm` per gestire temporizzazioni.
- Differenza tra segnali hardware e software.
- Gestione degli interrupt:
    - Interrupt vector e interrupt handler.

### **19. Esempi Pratici di Programmazione**

- Shell minimale:
    - Creazione di processi e gestione dei comandi.
    - Uso di `execv` per eseguire programmi.
- Programmi esempio per:
    - Gestione segnali (`signal`, `alarm`).
    - Comunicazione tra processi.

### **20. Gestione dei Processi**

- Comunicazione tra processi:
    - Pipe: utilizzo e gestione (`open`, `close`, `dup`).
    - Differenze tra `dup` e `dup2`.
- Esempi pratici:
    - Creazione di pipeline tra processi.
    - Reindirizzamento di input e output.
- Problemi comuni:
    - Blocco delle pipe e soluzioni.

### **21. Race Conditions e Regioni Critiche**

- Definizione di race condition.
- Implementazione delle regioni critiche:
    - Algoritmo di Peterson.
    - Soluzioni al busy waiting.
- Concetti di sincronizzazione:
    - Uso di variabili di blocco.

### **22. Concetto di Produttore-Consumatore**

- Problemi e soluzioni:
    - Utilizzo di semafori per sincronizzazione.
    - Implementazione di codice per produttore e consumatore.
- Problemi comuni:
    - Sincronizzazione dei segnali `wakeup`.

### **23. Mutua Esclusione e Semafori**

- Definizione e utilizzo dei semafori:
    - Operazioni `down` e `up`.
    - Atomicità e esclusione reciproca.
- Differenze tra semafori e mutex.
- Esempi di codice con semafori.

### **24. Lettori e Scrittori**

- Problema di lettori e scrittori:
    - Sincronizzazione tramite semafori.
- Gestione delle priorità tra lettori e scrittori.

### **25. Pthread e Mutex**

- Funzioni principali di Pthread:
    - `pthread_mutex_lock`, `pthread_mutex_unlock`.
    - `pthread_cond_wait` e `pthread_cond_signal`.
- Differenze tra lock e trylock.
- Uso delle variabili condizionali.

### **26. Monitor**

- Introduzione ai monitor:
    - Vantaggi rispetto ai semafori.
- Utilizzo in linguaggi come Java.
- Problema produttore-consumatore risolto con i monitor.

### **27. Scambio di Messaggi**

- Comunicazione tramite messaggi:
    - Funzioni `send` e `receive`.
- Problemi e soluzioni:
    - Perdita di pacchetti.
    - Acknowledgment e autenticazione.
- Implementazione produttore-consumatore con messaggi.

### **28. Concetti Avanzati di Sincronizzazione**

- Barriere: sincronizzazione tra processi.
- Inversione di priorità:
    - Problema e soluzioni (esempio Mars Pathfinder).
- Read-Copy-Update:
    - Separazione tra lettori e scrittori.

### **29. Scheduling**

- Funzioni dello scheduler:
    - Decisioni di esecuzione di processi e thread.
- Costi del cambio di contesto.
- Differenza tra processi CPU-bound e I/O-bound.

### **30. Introduzione allo Scheduling**

- Definizione e importanza dello scheduling.
- Stati di un processo:
    - **Esecuzione**
    - **Ready**
    - **Blocked**
- Funzione dello scheduler.
- Tipologie di scheduling:
    - **Non preemptive (senza prelazione)**
    - **Preemptive (con prelazione)**
- Momenti di intervento dello scheduler:
    - **Creazione di un processo**
    - **Uscita di un processo**
    - **Blocco del processo**
    - **Interrupt di I/O**

---

### **31. Algoritmi di Scheduling**

#### **Sistemi Batch (senza prelazione)**

1. **First Come First Served (FCFS)**
    - Esecuzione in ordine di arrivo
    - Pro e contro
2. **Shortest Job First (SJF)**
    - Ottimizzazione del turnaround
    - Problematiche con arrivi successivi
3. **Shortest Remaining Time Next (SRTN)**
    - Variante con prelazione di SJF

#### **Sistemi Interattivi (con prelazione)**

1. **Round Robin (RR)**
    - Funzionamento
    - Scelta del quantum di tempo
2. **Scheduling a Priorità (SAP)**
    - Priorità statica vs dinamica
    - Gestione delle code
3. **Shortest Process Next con Aging (SPNCA)**
    - Equilibrio tra SJF e sistemi interattivi
4. **Guaranteed Scheduling (GS)**
    - Equa ripartizione del tempo CPU
5. **Scheduling a Lotteria (SAL)**
    - Assegnazione casuale di tempi CPU
6. **Scheduling Fair-Share (SFS)**
    - Divisione equa della CPU tra gli utenti

#### **Sistemi Real-Time**

- Tipologie:
    - **Hard Real-Time**
    - **Soft Real-Time**
- Tipi di eventi:
    - **Periodici**
    - **Non periodici**
- Condizioni di schedulabilità

---

### **32. Parallelismo e Thread**

- Differenza tra processi e thread
- **Thread a livello utente** vs **Thread a livello kernel**
- Scheduling dei thread:
    - **Allocazione della CPU tra thread dello stesso processo**
    - **Problemi di starvation**
- **Esecuzione concorrente e gestione delle risorse**

---

### **33. Astrazione della Memoria**

- Definizione e necessità di astrazione
- **Memoria fisica vs memoria virtuale**
- Modelli di organizzazione della memoria:
    - **Memoria senza astrazione**
    - **Indirizzamento assoluto e relativi problemi**
- Swapping e gestione dello spazio di indirizzi

---

### **34. Gestione della Memoria**

- **Frammentazione della memoria**
- Metodi di allocazione della memoria:
    - **Bitmap**
    - **Liste collegate**
- Metodologie per l’allocazione dinamica:
    - **First Fit**
    - **Next Fit**
    - **Best Fit**
    - **Worst Fit**
    - **Quick Fit**
- **Buddy Allocation** e relativi problemi
- **Slab Allocator**
- **Caching e gestione delle risorse**

---

### **35. Memoria Virtuale**

- Concetto di memoria virtuale
- **Tabella delle pagine e traduzione degli indirizzi**
- **Gestione degli accessi alla memoria**
- **Page Fault e gestione degli errori**
- **Evoluzione delle tabelle di paginazione**:
    - **Paging a due livelli**
    - **Paging a quattro livelli**

---

### **36. Algoritmi di Sostituzione delle Pagine**

- **Page Replacement e Page Swap**
- **Lista degli algoritmi principali**:
    1. **Algoritmo Ottimale**
    2. **Not Recently Used (NRU)**
    3. **First-In, First-Out (FIFO)**
    4. **Second-Chance Algorithm**
    5. **Clock Algorithm**
    6. **Least Recently Used (LRU)**
    7. **Not Frequently Used con Aging (NFUA)**
    8. **Working Set Algorithm**
    9. **WS Clock Algorithm**

---

### **37. Traduzione degli Indirizzi e Ottimizzazioni**

- **TLB (Translation Lookaside Buffer)**
- **Funzionamento e gestione delle tabelle delle pagine**
- **Page Table Walk e accessi alla memoria**


---

### **38. Algoritmi di Sostituzione delle Pagine**

- **Second-Chance Algorithm**
- **Clock Algorithm**
- **Least Recently Used (LRU)**
- **Not Frequently Used con Aging (NFUA)**
- **Working Set Algorithm**
- **WS Clock Algorithm**
- **Allocazione Locale vs Globale**
- **Trashing e gestione della memoria**

---

### **39. Gestione della Memoria nei Processi**

- **Page Fault Frequency**
- **Allocazione equa vs proporzionale**
- **Mitigazione del trashing**
- **Swapping e scheduling a due livelli**
- **Multiprogrammazione: gestione dei processi CPU-bound e I/O-bound**
- **Dimensione ottimale delle pagine e bilancio dei fattori**
- **Paging Daemon**
- **Transparent Huge Pages**
- **Calcolo della dimensione ottimale delle pagine**
- **Metodi di compressione, compattazione e deduplicazione**

---

### **40. Memoria Virtuale e Gestione dei Processi**

- **Creazione di un processo e gestione delle dipendenze**
- **Fork e Copy-On-Write**
- **Esecuzione e Scheduling**
- **Page Fault e gestione in 10 passi**
- **Area di Swap e scenari di gestione**
- **DMA e problemi di gestione delle pagine**

---

### **41. Segmentazione della Memoria**

- **Memoria monodimensionale vs segmentazione**
- **Differenze tra paginazione e segmentazione**
- **Condivisione e protezione dei segmenti**
- **Conversione degli indirizzi nei sistemi segmentati**
- **Uso della TLB nei sistemi segmentati**
- **Esempio MULTICS e segmentazione avanzata**

---

### **42. Sistemi di Memorizzazione e File System**

- **Definizione e funzioni di un file system**
- **Organizzazione dei dati su disco**
- **Gestione dell’accesso ai file**
- **Virtual File System (VFS)**
- **Caching dei file (Page Cache, Buffer Cache)**
- **Metadati e attributi dei file**
- **Tipi di file e directory**
- **File speciali e file eseguibili**

---

### **43. Struttura e Operazioni sui File**

- **Tipologie di file**
- **Strutture di gestione dei file**
- **Attributi e metadati**
- **Operazioni di base sui file** (Creazione, Lettura, Scrittura, Eliminazione)
- **Accesso sequenziale e casuale**
- **Uso di Seek per l’accesso rapido**
- **Metodi di copia dei file**
- **Organizzazione delle directory**
- **Path assoluti e relativi**

---

### **44. Directory e Gerarchia del File System**

- **Struttura monolivello vs multilivello**
- **Operazioni sulle directory** (Creazione, Eliminazione, Lettura)
- **Gestione dei percorsi nei sistemi UNIX e Windows**
- **Gestione dei link (Hard link vs Symbolic link)**
- **Creazione ed estrazione di archivi (tar, zip)**

---

### **45. Boot System e Partizionamento**

- **BIOS e UEFI**
- **Struttura dell’MBR e partizioni**
- **GUID Partition Table (GPT)**
- **Secure Boot**
- **EFI System Partition (ESP)**

---

### **46. Allocazione dei File nel File System**

- **Allocazione contigua**
- **Allocazione con liste concatenate**
- **File Allocation Table (FAT)**
- **Problemi di frammentazione**
- **Uso degli I-node per la gestione dei file**

---

### **47. I-node e Struttura Interna dei File System**

- **Funzione e struttura degli I-node**
- **Gestione dei file di grandi dimensioni**
- **Caching degli I-node**
- **Uso della memoria RAM per migliorare la gestione del file system**

---

### **48. Approfondimenti su NTFS e Sistemi di Archiviazione**

- **Differenze tra NTFS, FAT32 ed EXT4**
- **Gestione della memoria nei moderni file system**
- **Ottimizzazioni per la gestione dei blocchi di memoria**
- **Uso della cache per migliorare le prestazioni**


---

### **49. Struttura delle Cartelle e Gestione dei File**

- **Struttura delle cartelle e voci nei file system**
- **Metodi di organizzazione delle directory**
- **I-node e gestione dei metadati**
- **Gestione dei nomi dei file nelle directory**
- **Heap e gestione delle voci**
- **Ricerca dei file all’interno delle directory**
- **Utilizzo della cache per l’accesso rapido ai file**

---

### **50. File Condivisi e Link nei File System**

- **Hard Link**
- **Soft Link**
- **Link simbolici e differenze tra hard e soft link**
- **Problemi di duplicazione dei file e backup dei symlink**

---

### **51. Gestione dello Spazio su Disco**

- **Allocazione contigua vs non contigua**
- **Strategie di ottimizzazione e latenza dei blocchi**
- **Bitmap vs Free List per la gestione dello spazio libero**
- **Gestione della latenza nei dischi**
- **Quota di utilizzo nei sistemi multiutente**
- **File System Ext2 e gestione dei blocchi liberi**

---

### **52. Performance e Ottimizzazioni del File System**

- **Caching e buffer cache**
- **Struttura interna di Ext2**
- **Ottimizzazioni per ridurre la frammentazione**
- **Uso di bitmap per la gestione delle risorse**
- **Tecniche per migliorare la velocità di accesso ai file**
- **Algoritmi di sostituzione della cache**
- **Strategie di sincronizzazione per evitare perdita di dati**
- **Page Cache e Buffer Cache**

---

### **53. Virtual File System (VFS)**

- **Struttura e funzionamento del VFS**
- **Montaggio di nuovi file system**
- **Gestione delle operazioni indipendenti dal tipo di file system**
- **Superblock e gestione dei V-NODE**
- **Compatibilità con diversi file system (Ext4, NTFS, FAT32, ecc.)**

---

### **54. Backup e Affidabilità del File System**

- **Tipologie di backup (fisico vs logico)**
- **Uso di strumenti come rsync**
- **Strategie per la coerenza dei dati dopo un crash**
- **Journaling per la protezione dei file system**
- **Differenze tra Ext2, Ext3 ed Ext4**
- **Deframmentazione e deduplicazione**

---

### **55. Principi di Hardware I/O**

- **Panoramica sui dispositivi di I/O**
- **Dispositivi a blocchi vs dispositivi a caratteri**
- **Velocità e impatto delle periferiche sul sistema**
- **Interfacce standard per la comunicazione con l’hardware**
- **Porta USB, SATA, SCSI, Thunderbolt**
- **Bus di sistema (PCIe, Northbridge, Southbridge)**

---

### **56. Comunicazione tra CPU e Periferiche**

- **Controller dei dispositivi e registri di controllo**
- **Port-Mapped I/O vs Memory-Mapped I/O**
- **Gestione degli indirizzi di memoria per i dispositivi**
- **DMA (Direct Memory Access) e riduzione del carico sulla CPU**
- **Modalità di trasferimento dati:**
    - **Polling (Busy Waiting)**
    - **Interrupt-Driven I/O**
    - **Cycle Stealing**
    - **Burst Mode**
    - **Fly-By Mode**

---

### **57. Interrupt e Gestione degli Eventi Asincroni**

- **Differenze tra Trap, Fault e Interrupt**
- **Interrupt hardware e gestione delle priorità**
- **Passaggi per la gestione di un interrupt**
- **Interrupt Precisi vs Imprecisi**
- **Pipeline e gestione dei processi interrotti**
- **Utilizzo di un Vettore degli Interrupt**
- **Salvataggio del contesto del processore**

---

### **58. Software di I/O**

- **Struttura del software per la gestione dell’I/O**
- **Denominazione uniforme dei file nei dispositivi di archiviazione**
- **Gestione degli errori nei dispositivi di I/O**
- **Trasferimenti sincroni vs asincroni**
- **Buffering e gestione dei dispositivi in tempo reale**
- **Dispositivi condivisibili vs dispositivi dedicati**
- **Esempio di stampa e gestione del buffer di stampa**

---

### **59. Approfondimenti su DMA e Comunicazione con le Periferiche**

- **Gestione degli interrupt in ambienti multitasking**
- **Polling vs Interrupt-Driven I/O**
- **Sincronizzazione tra processi e dispositivi hardware**
- **Tecniche di accesso diretto alla memoria**
- **Uso del DMA per l'ottimizzazione delle operazioni di I/O**
- **Direct Memory Access e riduzione degli interrupt della CPU**

---

### **60. RAID e Disaster Recovery**

- **Gestione della ridondanza nei sistemi di archiviazione**
- **RAID 0, RAID 1, RAID 5, RAID 6 e RAID 10**
- **Backup remoti e Disaster Recovery**
- **Riduzione delle duplicazioni di file tramite hard link**
- **Uso di snapshot e versioning per la protezione dei dati**

---

### **61. Comandi Unix/Linux per la Gestione del File System**

- **Comandi per la gestione delle partizioni (`lsblk`, `fdisk`, `mount`)**
- **Montaggio e smontaggio di dispositivi**
- **Comandi per la gestione dei file (`cp`, `mv`, `rm`, `ln`)**
- **Sincronizzazione dei dati con `rsync`**
- **Gestione delle directory e percorsi assoluti/relativi**
- **Uso di `tar` e `zip` per la compressione e archiviazione**

---

### **62. Software per la Gestione degli Interrupt**

- **Passaggi per la gestione di un interrupt software**
- **Salvataggio dello stato del processore**
- **Esecuzione della procedura di servizio dell’interrupt**
- **Ripristino del contesto del processo interrotto**
- **Esecuzione del processo successivo nella coda di scheduling**

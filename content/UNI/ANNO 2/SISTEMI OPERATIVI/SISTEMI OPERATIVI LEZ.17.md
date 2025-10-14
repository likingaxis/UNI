Nella macchina viene avviato il BIOS, un piccolo sistema operativo che gestisce l'hardware.
- controlla che non ci siano errori
- che sia tutto ok ecc...
- poi bisogna far partire il vero s.o. con una serie di codici che lo fanno partire -> 
Per scegliere quale s.o. far eseguire delle varie partizioni si usa 
L'MBR contiene una tabella con tutti i primi file di boot per ogni partizione
- nelle tabelle c'è scritto da quale settore a quale settore è scritta quella partizione 
### PARTIZIONE
![[Pasted image 20241213120813.png|500]]
- Ogni partizione deve essere contigua
- Ogni partizione del disco è strutturata come nella parte sotto della foto
- L'MBR punta ad ognuno dei blocchi di boot, che contengono i primi codici per far eseguire il s.o.
Immaginiamo di avere diverse partizioni di boot
- linux
- windows
- macos

>[!info] L'MBR tiene anche traccia delle partizioni senza s.o. ma lo specifica
### UEFI
Il BIOS vecchio è stato abbandonato e sostituito da UEFI per diversi motivi:
- per problemi di flessibilità 
- supporto di architetture a 64 bit
- utilizzo di interfacce grafiche migliori e mouse
- introduzione del Secure Boot(lo spieghiamo tra poco)
- recupero del boot record precedente
GPT andò a sostituire MBR consentendo una gestione illimitata di partizioni e dischi con capienza maggiore(2,2TB)
![[Pasted image 20241213122234.png]]
- blocco 0, consente retrocompatibilità con vecchi MBR
- blocco 1, un sistema che descrive le info sulle varie partizioni
- blocco 2, lista di puntatori a partizioni
- varie partizioni
- poi abbiamo il backup che ci consente di fare il recupero

GUID PARTITION TABLE (GPT)
- Sistema di gestione delle partizioni
- Tutte le cose dette prima e in più
- un controllo di integrità **CRC**
EFI System Partition **(ESP)**:
- è una partizione speciale sui dischi GPT
- archivia file utili all'avvio come:
	- bootloader, driver e utility di diagnostica
- Usa il file system FAT32
##### Parentesi sul Secure Boot
- Alcuni virus attaccano direttamente nella fase di boot
- il boot loader controlla le firme digitali dei vari boot, driver e utility
- riduce notevolmente la presenza di vari codici malevoli
- alcuni s.o. non la supportano a pieno e quindi bisogna disattivarla

## Come sono implementati i file nel file system
### Ci sono due modi per memorizzare file
#### 1. Allocazione contigua
![[Pasted image 20241213124122.png]]
Ogni file è memorizzato come un insieme di blocchi contigui
- problema di frammentazione nel caso di una rimozione del file
- facile implementazione
- necessità di avere punto di inizio e fine del file
#### 2. Allocazione con liste concatenate
![[Pasted image 20241213124301.png|500]]
- ogni file è memorizzato come un insieme di blocchi che vengono collegati con puntatori
- ogni directory deve solo salvarsi il puntatore di inizio e poi basta scorrerlo
- con il sistema dei puntatori risolvo il problema della frammentazione
- Problema: devo scorrere blocco dopo blocco (seek) per arrivare in quella determinata posizione
Soluzione
#### 3.Introduzione di FAT
Sistema ottimizzato delle liste concatenate
Utilizzo la memoria RAM per avere una tabella che mi punta ad ogni blocco, dicendomi del singolo file, il suo rispettivo blocco successivo
![[Pasted image 20241213125029.png|500]]
Problema:la FAT chiede un botto di RAM (1 TB di disco richiede 3GB di RAM)
- Ora si USA NTFS ma per le schede SD e altra roba si usa ancora perché sono di dimensioni limitate
## I-NODE
Introdotti in Linux l'I-node contiene tutte le info di un singolo file tranne il nome e il contenuto quindi avremo:
- data creazione
- <font color="#4f81bd">indirizzi di dove si trovano i vari blocchi</font>
- il proprietario
- i permessi di accesso
Quando apro un file solo l'I-node di quel file viene messo in memoria 
Se un file supera il limite degli indirizzi da mettere in un I-node esso punterà a un altro blocco che avrà gli indirizzi aggiuntivi(per file enormi)
Gli I-node sono in una cache che viene gestita seguendo determinati algoritmi
come è fatto un I-node:
![[Pasted image 20241213130513.png|400]]
Per windows si usa NTFS usa tipo gli I-node ma può mettere informazioni più grandi
## Le cartelle
Le cartelle sono un file che all'interno ha la lista degli altri file che sono in essa
La singola riga che descrive il singolo file si dice voce
Ci sono due modi per organizzare le cartelle:
##### Con voci fisse
negli anni 80 ogni directory aveva
- Nome file
- attributi
	- le solite cose
	- indirizzi dei singoli blocchi
![[Pasted image 20241213130919.png]]
##### Directory con riferimento
La voce prevede
- nome del file
- I-Node
![[Pasted image 20241213131110.png|400]]

>[!info] Anche una cartella essendo un file e un I-node
#### Come gestisco i nomi dei file nelle directory(la parte a sx delle dir)
Ogni file ha un nome come detto in precedenza e di solito sono memorizzate con stringhe ovvero sequenze di caratteri 
Ci sono due modi per memorizzare i nomi dei file
##### 1. Voci con lunghezza variabile
Ogni file ha il suo Header che mi dice quanto è lunga la stringa del file
e poi ho la stringa con il nome
![[Pasted image 20241213131946.png|300]]
##### 2. Gestione degli Heap
Ho una stringa enorme con tutti i nomi
Ogni voce ha un puntatore che punta all'inizio del suo nome e la scorro per la sua lunghezza dettata dall'header
![[Pasted image 20241213132131.png|300]]
# Ricerca all'interno delle directory
Inizialmente avveniva la ricerca di un file confrontando tutte le voci nelle directory
Utilizzo di una tabella che contiene tutti gli indirizzi dei file indicizzati attraverso una funzione di Hash, ne facilita la ricerca
Anche qui si usa una cache che mette i file più cercati così da facilitarne l'accesso

>[!info] se faccio `ls -l` non apro i file per vederli, apro solo le loro posizioni e le loro liste di I-node con tutti i metadati i nomi dei file vengono presi dalle liste delle directory

## File Condivisi e Link nei file system
Posso condividere i file per fare in modo che più utenti ci lavorino sopra
Per farlo si usano i LINK
#### 1. Hard Link
Condivido direttamente e brutalmente l'I-Node
- Un file si elimina davvero solo se ogni suo Hard link viene eliminato
![[Pasted image 20241213133252.png|400]]

![[Pasted image 20241213133706.png|500]]
Con il sistema Hard Link possiamo fare questo esempio che va da 
a-> c
e vedere che un singolo file ha un contatore che conta quante directory puntano ad esso finché si azzera e muore

#### 2. Soft Link
Punto solo al suo nome, se lo elimino il Soft non funziona più
- es: crea collegamento su windows
### Parentesi sui Link simbolici
Tu puoi fare un Hard link sullo stesso file system ma non su altri
con i link simbolici possiamo farlo 
Qui devo crearmi il mio I-node che indicherà poi il percorso all'altro I-node sull'altro file system
Il sistema operativo deve farsi tutto il percorso
- se faccio un backup rischio di copiare anche i file dei symlink
- se ne ho più di uno faccio 1000 copie
- ho bisogno di software avanzati che capiscono che si tratta di un symlink

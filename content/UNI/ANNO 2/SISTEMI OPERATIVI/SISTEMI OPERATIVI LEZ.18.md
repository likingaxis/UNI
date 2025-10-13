##### Spiegazione di come funziona l'esame: 
- prova su form
- programmazione c su carta + domanda a risposta aperta
- Orale facoltativo o a meno di prove sospette

in poche parole per tutto l'anno accademico si può provare SISTEMI+RETI 3 volte
### GESTIONE DELLO SPAZIO SU DISCO
#### CONTIGUA VS NON CONTIGUA
Ci sono due modi per memorizzare i file:
- ALLOCAZIONE CONTIGUA
	- Il singolo file occupa un insieme di blocchi contigui
	- ha un indirizzo di partenza iniziale e una lunghezza
	- se esso cresce e supera il limite il file deve essere assegnato a un'altra area di memoria
	- se vengono eliminati dei blocchi allora potremmo incorrere in frammentazione
- BLOCCHI NON CONTIGUI
	- Il file viene spezzettato in blocchi di dimensione fissa 
	- riduce la frammentazione
	- ogni blocco ha il riferimento del blocco successivo questo ci consente di metterli allocati dove ci pare
###### OTTIMIZZAZIONE E LATENZA DEI BLOCCHI NON CONTIGUI
c'è una proprietà che in sostanza ci dice
più il blocco è grande meno impiego nel cercare le varie informazioni di un file
- posso però incorrere in problemi di sovradimensionamento della memoria
più è piccolo più impiego a cercare i blocchi ma risolvo la cosa detta prima
Ovviamente quando si parla di ricerca di un blocco si parla proprio di ->
Latenza: tempo che perdi nel far girare la testina
![[Pasted image 20241219174832.png|400]]

Avendo dischi da TB oggi si preferisce creare blocchi +grandi


##### Come tracciamo i blocchi liberi?
Metodo 1:potrei avere una lista di indici di blocchi liberi.
![[Pasted image 20241219175443.png|400]]
- ha una rappresentazione sparsa(rivedi differenza tra sparso e denso)
- ogni blocco può contenere
	- indirizzo di inizio del blocco libero
	- lunghezza conto quanti blocchi avrò liberi
- la free list ha i puntatori utilizzati nella memoria RAM 
- gli altri nel disco
>[!tip] Queste strutture sono caricate nel s.o.

Metodo 2: bitmap, 1 indica libero 0 indica pieno
rimane sempre in memoria rispetto al metodo 1 che si svuota a secondo del numero dei blocchi pieni o liberi
- tutta la bitmap indica tutta la memoria
- ogni rettangolo una sua porzione
![[Pasted image 20241219183656.png|150]]
![[Pasted image 20241219190319.png|300]]
#### Gestione e assegnazione delle quote nei sistemi multiutente
L'amministratore assegna per ogni utente una quota
- si intende un numero massimo di blocchi liberi e file
il SO controlla se non si supera questa quota e tiene traccia di quanti file aperti ha un utente o un processo nella tabella dei file aperti ogni file aperto contiene:
- i suoi attributi(visti nella lez scorsa)
- indirizzi del disco(dove si trova il file)
- utente: l'utente che legge il file
- puntatore alla tabella delle quote
La tabella delle quote è una tabella che tiene traccia delle quote di ogni utente e dei suoi file aperti
Abbiamo due limitazioni
soft: io singolo utente posso superare quel limite di quota per poco tempo
Hard: se lo supero mi viene fatta una restrizione in termini di accesso
![[Pasted image 20241219191036.png|400]]

#### Come è organizzato Ext2
![[Pasted image 20241221175350.png]]
Ext2 viene usato principalmente in Linux ed è un File System
- suddiviso in gruppi di blocchi 
- ogni gruppo di blocchi ha
	- super blocco
		- contiene i dettagli sui blocchi liberi e non del disco e il numero di I-node
	- descrittore del gruppo
		- dettagli aggiuntivi sui blocchi liberi, I-node e posizione delle varie Bitmap
	- Bitmap
		- traccia i blocchi liberi e I-node liberi
	- I-node i meta 
		- dati di un file
	- blocchi di dati 
		- contengono i file e le directory del file system, non sono necessariamente contigui sul disco
nella scrittura di file Ext2 si tende a minimizzare la frammentazione cercando di scrivere il più possibile nell'area di blocchi della stessa directory genitore finché non si esaurisce lo spazio 
- per determinare le aree libere Ext2 usa le bitmap
![[Pasted image 20241222075517.png]]
una voce di questi blocchi si legge così
- "Colossale" è un file (Tipo, F) 
- con nome lungo 9 
- con numero I-Node 19.
quando elimino un file esso viene marchiato come libero ma rimane presente in memoria in attesa di una eventuale riscrittura 
per accedere ai file uso soft e hard link, inoltre uso anche eventuali comandi di open
- viene sfruttata una cache che migliora l'accesso agli ultimi file visitati o in base ad altre caratteristiche
#### Performance(tecniche per migliorarle)
Velocità di accesso:

tutto il computer è molto più veloce del disco quindi bisogna ottimizzare le cose in modo che il File system sia veloce
All'interno del sistema operativo vengono usate delle cache
- buffer cache: memorizza i blocchi del disco in RAM per ridurre gli accessi ai blocchi in disco
- page cache: prima di essere blocchi ovviamente in modo più virtuale e astratto sono pagine dei file, qui in questo caso vengono salvate le pagine più utilizzate collegate al VFS virtual file system(spiego sotto)
![[Pasted image 20241222084633.png]]
###### Precisazione sulla cache
è sempre la stessa struttura dove ho dei blocchi con uso di hash per identificare rapidamente se un blocco è nella cache 
se si cerca un file nella cache e non c'è viene messo dal disco alla cache
Ogni elemento della cache viene messo in questa lista doppiamente collegata
![[Pasted image 20241222085650.png|400]]
Se ho la memoria cache piena che faccio?
applico degli algoritmi come quelli già visti con dei vantaggi e svantaggi
se ad esempio volessi usare LRU potrei avere limiti di inconsistenza in caso di crash
Per prevenire la perdita di dati faccio sync dove ogni volta scrivo il "backup" su disco 
il sistema viene sempre basato sul fatto che può sempre saltare la corrente
Cache buffer e Cache delle pagine sono entrambe da sincronizzare
###### Avremo un virtual file system
che punta a tutti i file system e fa da intermediario
Quando dei file system vengono implementati devono avere un vettore da dare ai virtual file system
Ritorniamo alle slide prima
Page Cache Buffer cache
tutte e due sono nella ram e quindi devo gestirle entrambi cercando di ottimizzare la loro allocazione
###### Comandi già visti e non
free
- già visto
defrag
- cerca di scansionare tutti i blocchi di memoria e metterli vicini così da evitare spazi piccoli non contigui di memoria
impiega molto tempo
in Ext4 è ottimizzato preallocando dei blocchi contigui così da ridurre la frammentazione

##### deduplicazione e compressione
Alcuni File System possono comprimere i file ad esempio sostituendo sequenze ripetute in modo da ridurre il peso di un file
- NFTS
- ZFS
Inoltre altri possono ridurre le duplicazioni di file creando ad esempio Hard link e avere una sola copia in memoria
per scoprire duplicazioni si fa durante la creazione del file **inline** oppure
**Post process** in 
- background un processo scansiona il tutto
#### AFFIDABILITÀ
Possono incorrere errori al File System di diverso tipo
- umano
- software
- hardware
##### per risolvere si fanno i Backup
ci sono due tipi di backup
- fisici
	- copio i byte bit a bit 1:1
- logici
	- copio in base alle ultime modifiche apportate all'albero dei file
	- oppure uno specifico file
	- si effettua una copia ad alto livello basandosi su database o strutture dati astratte
![[Pasted image 20241222101927.png|500]]
wayback machine di apple fatta bene


Strumento **rsync** sincronizza una volta i file e poi modifica alle prossime sincronizzazioni solo i file cambiati
- molto versatile
- consente anche accessi da remoto
con a manteniamo i permessi e la struttura precedente
con v ci ritorna i dettagli sul trasferimento 
normale:
```scss
rsync -av /sorgente/cartella /destinazione/cartella
```
da remoto:
```scss 
rsync -av /sorgente/cartella utente@remoto:/destinazione/cartella
```
### Coerenza dei file
IMPORTANTE
se avviene un crash potrebbe avvenire la perdita di informazioni
uso delle utility per verificare la coerenza dei dati
- vengono eseguite all'avvio dopo un crash
Journaling
prima di eseguire una modifica sul file sysem si salvano le operazioni da fare in un registro journal.
- si controllano

se salta la corrente posso capire cosa non e stato fatto e posso ripristinarlo
### Virtual File System(VFS)
il VFS consente di utilizzare diversi File System in un'unica macchina virtualizzandoli
- NFTS
- FAT-32
- Ext2
- ecc...
Il VFS ha due livelli principali: 
- Superiore: 
    - Interagisce con le chiamate di sistema POSIX come OPEN, READ E WRITE    
- Inferiore: 
    - Decine di funzioni che il VFS invia ai file system sottostanti
![[Pasted image 20241222220015.png|400]]

#### Struttura del VFS
- Superblock: tipo di file system, nome, dimensione e dove si trova

- V-NODE: 
	- rappresenta ogni file o directory del VFS, contiene i metadati (permessi, proprietà, dimensione del file e riferimenti ai dati sul disco). 
	- È usato dal VFS per rendere l'accesso ai file indipendente dal tipo di file system. 

- Directory del FS: 
	- permette al VFS di mappare i nomi dei file ai loro v-node indipendentemente dal FS in cui questi file si trovano.
	- facilita la navigazione e l'accesso ai file.
![[Pasted image 20241222221253.png|400]]
Quando viene aggiunto un nuovo file system questo deve registrarsi al VFS fornendo un serie di funzioni specifiche (lettura, scrittura, montaggio, ecc... )

Quando viene montato un nuovo file system (es. USB), il VFS crea un v-node per i file presenti e mappa le operazioni richieste a quel file system. 

Il VFS poi tiene traccia dei file aperti e utilizza il v-node per sapere quale file system deve gestire una specifica richiesta.
#### RAID
Disaster recovery: backup in un altro posto
è decisamente a basso livello legato all'hardware
[[3.Le memorie#RAID|lezione RAID]]
### FILE SYSTEM V7 UNIX
![[Pasted image 20241222221827.png]]
Ha reso UNIX famoso con una gestione con il numero di i-node e il nome del file
Da notare che per ogni i-node vi era un contatore incrementato o decrementato in base al numero di link con esso. 
Anche in questo file system era possibile muoversi attraverso 
- percorsi assoluti(parto dalla radice)
- relativi(parto da una generica cartella)

Il passaggio a EXT avvenne soprattutto per
- aver introdotto il VFS
- superare i limiti di 2GB
- 2 e 3 introdussero blocchi di dimensione variabile
- con Ext3 venne introdotto il journaling
- con BTFRS venne introdotto il copy on write 

### UNA CARRELATA DI COMANDI
##### Visualizzazione delle partizioni  
```scss
Comando lsblk  
```
Mostra un elenco dei dispositivi a blocco dove per blocco si intendono proprio i blocchi del disco, mi permette di vedere anche dischi e partizioni. 
```scss
Comando fdisck -l 
```
Elenca tutte le partizioni su disco comprese quelle non montate  
```scss
Comando mount -l 
```
Elenco dei file system appena montati con le loro opzioni di montaggio ed etichette 

Comando per fare il mount di una partizione su file system
```scss
mount [opzioni] <dispositivo> <directory>
tipo
sudo mount /dev/sda1 /mnt/mydisk
```
quindi dev monta mnt
![[Pasted image 20241222222528.png]]

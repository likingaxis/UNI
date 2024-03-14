argomenti:
- memoria secondaria
libro(50)
riassunto(14)
## Gerarchie di memorie
più la memoria è grande più ci metti tempo ad accedervi  e costa meno
esempio:
- registri della CPU sono più veloci e meno capienti ma costano di più
- nastri e dischi ottici sono più capienti ma più lenti però costano meno
le varie memorie si possono mettere su una piramide dove più vai in basso più sono lente come accesso, più capienti e meno costose, dove è sottolineato in verde c'è un gap 
![[Screen Shot 2024-03-12 at 10.49.07.png]]
>[!simonettata]-
>la macchina non deve mai stare in attesa sennò inefficiente
>
>quando andiamo dalla memoria centrale al disco meccanico c'è ancora più ritardo
>
>perchè la testina dell'hard disk è meccanica
>
>i dispositivi ottici potrebbero ESPLODERE nel tempo
>
#### dischi magnetici
Sono uno o più piatti di alluminio rivestiti da materiale magnetico.
Si dà una polarità a questi magneti con una carica elettrostatica dalla testina che corrispondono a (+/-) che poi letti dalla stessa testina corrispondono a  0 e 1
testina:si muove in modo longitudinale e copre tutta la superficie del disco che gira, la testina ha questo solenoide che permette di cambiare le particelle ferrose di una piccola porzione del disco che cambiano polarità
![[Screen Shot 2024-03-12 at 11.05.03.png]]
##### la traccia
la traccia è la sequenza di bit che percorre il disco(quella in blu)
le tracce sono divise in settori e tra i settori c'è un gap di intersezione
più la traccia è vicino al centro più è densa di informazioni ma sempre con lo stesso numero di informazioni
![[Screen Shot 2024-03-12 at 11.06.25.png]]

- **ogni traccia è formata da un preambolo che sincronizza le testine**
- **ogni traccia ha un ECC che serve per il controllo degli errori e la correzione**
#### hard disk
Sfruttano più dischi magnetici
Ogni disco ha diverse tracce e per le tracce parallele a tutti gli altri dischi si dice come la figura che forma, cilindro 
Ogni disco ha la sua testina e ha un processore chiamato controller del disco che sincronizza i controlli dettati dal software
ci sono 3 tipi tempi:
- **Tempo di seek** è di circa 5/10 ms ed è il tempo che impiega la testina per posizionarsi nella parte giusta
- **Latenza rotazionale** il disco deve girare per trovare l'informazione giusta con rpm(rotazioni-per-minuto)con latenza tra 3-6 ms
- **tempo di trasferimento** tempo necessario per il passaggio dei dati al cervello della macchina con un tempo di 3,5/4 µs(micro-secondi)
![[Screen Shot 2024-03-12 at 11.34.55.png]]

#### I floppy disk
sono piccoli ma contengono poca memoria 
sono tipo gli hard disk ma non sono immersi da un liquido e quindi le testine(punzone) che servono per leggerli toccano direttamente la superficie 

#### Dischi IDE
Su questi dischi il controllore è su una scheda separata.
Il sistema operativo leggeva e scriveva dati sul disco e scriveva anche sul registro della CPU, invocando il BIOS nella ROM
**IDE** si è poi evoluto in **EIDE** che con uno schema di indirizzamento **LBA**(Logical Block Addressing) aumentò la capacità massima e la velocità di lettura sfruttando anche il parallelismo
#### SCSI disk
meglio di quelli IDE perché il controllore permetteva di collegare fino a 7 dispositivi insieme
(scanner, cd-rom, unità a nastro...)

### RAID

#### Dischi sempre più grandi per tanti dati
avere un disco solo enorme **SLED** che tiene tutti i dati non è il massimo,  si decise così di farne tanti **PICCOLINIIII**
e nacque così l'idea del RAID ovvero quella di fare tanti dischi separati ma che poi il calcolatore li vede come un unico disco e distribuiscono i dati sulle diverse unità per permetterne una gestione parallela.
Sostituendo la scheda contenente il controllore del disco con un controllore di tipo RAID
Ci sono 5 livelli di RAID:
#### Raid livello 0
i dischi vengono usati per memorizzare le cose in ordine sequenziale applicando appunto il concetto di Round-Robin(riempio lo strip 0 poi strip 1 poi 2 e così via...)
Avendo le cose divise in 4 dischi puoi cercarle in parallelo e fare prima
non è un vero RAID perché quando un disco si rompe non hai possibilità di recuperare i dati
![[Screen Shot 2024-03-12 at 15.03.51.png]]

#### Raid livello 1
ha lo stesso concetto del raid 0 solo che in questo caso si crea una copia del disco nello stesso momento in cui si scrive su quello originale
quali sono gli svantaggi? ci sono troppi dischi e la memoria si riduce
![[Screen Shot 2024-03-12 at 15.09.21.png]]
#### Raid livello 2 
Scomponi una parola distribuendola su ogni disco così se hai un errore puoi scovarlo meglio con l'uso del codice di Hamming vedi:[[Organizzazione sistemi di calcolo]]
ad esempio nell'immagine abbiamo 7 dischi,
ogni disco avrà 1 bit della parola ma ogni 4 bit(nibble) ci saranno 3 bit di parità ovvero quei bit che con il codice di Hamming ci segnalano l'errore
problema: tutti dischi devono essere gli stessi e devono essere sincronizzati e andare alla stessa velocità
![[Screen Shot 2024-03-12 at 15.11.10.png]]
#### Raid livello 3
è simile al RAID 2 ma solo un disco è dedicato ai bit di parità.
Ogni parola ha un bit di parità che spesso non è sufficiente a risolvere l'errore
![[Screen Shot 2024-03-12 at 15.25.41.png]]
#### Raid livello 4
è come il raid 0 solo che ha un disco di parità che prende in considerazione tutti gli strip, quindi se un disco si guasta si può riparare recuperando i byte dal disco di parità.
Ha prestazioni scarse e si può creare un collo di bottiglia quando il disco di parità è pieno
![[Screen Shot 2024-03-12 at 15.31.37.png]]
#### Raid livello 5
![[Screen Shot 2024-03-12 at 15.44.00.png]]
Ogni disco ha una sezione dedicata alla parità
il problema è che per recuperare i dati ci metti troppo

#### SSD
Sono basati su memoria flash non volatile(se spegni il pc le informazioni ci sono ancora)
non hanno elementi meccanici e costano di più ma sono molto più veloci dei normali dischi
il principale guasto che può avvenire è che un transistor potrebbe rompersi e che può rimanere o sempre spento o sempre acceso

#### CD-ROM
Inventati dalla sony nel 1984
sono dei dischi fatti di policarbonato con un alluminio riflettente, sopra questo materiale venivano creati dei solchi pit o venivano lasciati piatti land, questi funzionano come un vinile ovvero che un solco corrisponde a 1 e un land corrisponde a 0.
Per essere rilevati questi solchi o colline venne usato un laser
cd-rom vs magnetici 
cd rom tipo vinili in modo sequenziale 
magnetici le informazioni sono sparse e a livello magnetico
![[Screen Shot 2024-03-12 at 16.00.52.png]]
**formato di memorizzazione:**
il cd rom ha per ogni simbolo(?) fa corrispondere ogni byte in  14 bit di cui 3 sono del codice di Hamming e due ne rimangono liberi
ogni 42 simboli hai un frame(588bit)
e un sector ogni 98 frame
![[Screen Shot 2024-03-12 at 16.14.20.png]]
#### i settori del cd rom
le informazioni vengono memorizzate con o senza controllo di errore
un settore contiene
un preambolo(serve per dire che è una nuova sequenza) da 12 byte fissi+4 byte che specificano il numero del settore(i settori sono numerati in ordine)
e il modo, se stai usando o no la correzione di errore
il modo 2 dove non sono attesi errori viene usato per musica e video

Poi ci furono i **CD-R registrabili**, sono irreversibili dove i laser rompono il pigmento e corrispondono al pit
![[Screen Shot 2024-03-12 at 16.27.41.png]]
**CD-RW** sono quelli riscrivibili
venivano utilizzate dei materiali per ripristinare lo stato iniziale del disco trasformare un pit in un land
il laser ha 3 modalità
- bassa
	- leggi lo stato del pigmento senza alterarlo
- media
	- scioglie il materiale e lo ripristina allo stato naturale
- alta
	- lo scioglie creando il pit


#### DVD
sono simili ai cd ma più innovativi
- hanno pit più piccoli
- spirale più stretta
- laser rosso
- maggiore capacità
- maggiore troughput (velocità di trasfermento)
si dividono in 4 formati:

| nr. | side(dischi incollati) | layer(due livelli) | GB  |
| --- | ---------------------- | ------------------ | --- |
| 1   | single-sided           | single-layer       | 4.7 |
| 2   | single-sided           | dual-layer         | 8.5 |
| 3   | double-sided           | single-layer       | 9.4 |
| 4   | double-sided           | dual-layer         | 17  |
![[Screen Shot 2024-03-12 at 16.49.54.png]]
### conclusioni
finito a 
pag(59)
riassunto(22)



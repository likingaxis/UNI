### STORIA DI LINUX
- Linux è una copia di UNIX, scritto da Linus Torvalds 
- il 64% dei server nel mondo sono con varianti di Unix o Linux
- Unix ha una serie di programmi che funzionano da soli ma altri sono molto complessi e danno il meglio di se quando sono con altri programmi

Bash è il linguaggio di scrittura per la gestione dei sistemi operativi come Linux e Unix.
Oltre a essere un linguaggio di scripting è anche una Shell ovvero un software su riga di comando che esegue gli script 

#### Carrellata di comandi 
Man serve per mostrare il manuale di Linux di un determinato comando o tutto il manuale
``` bash
Man comando
```

![[Pasted image 20241019131736.jpg|500]]

### Cosa fanno tutti i comandi?
Questi comandi prendono n byte in input e mandano fuori n byte in stream di output:
- standard output, un tipo di output usato per le normali operazioni
- output con errori standard error, consente di inviare solo i messaggi preoccupanti che contengono errori problemi da risolvere ecc..
>[!question]- cosa sono gli stream?
>sono dei flussi astratti al livello software gestiti dal sistema operativo e bisogna vederli come degli spazi in memoria su cui ci si scrivono sopra le informazioni da streammare

### Carrellata di comandi
Questi comandi mettono a disposizione alcune chiamate di sistema che non si possono usare su software che devono fare trap cambi di contesto ecc

Quindi, abbiamo visto questi comandi. 
>[!info]- **AWK** -> serve per l'elaborazione di file in particolare di testo, CSV e log usando piccoli script
>![[Pasted image 20241023163545.png|500]]

> [!info]- **GREP**-> cerca una stringa specifica all'interno di un testo.
>la stringa si dice pattern e avremo la possibilità di modificare ciò che fa GREP usando dei comandi predefiniti
>-i stampa senza fare distinzioni tra maiusc e minusc
>-v stampa tutto tranne quella riga di quella parola
>-n indica il numero della riga
>![[Pasted image 20241023165601.png|500]]

>[!info]- **CAT** -> il comando che accede ad un file per esempio, e lo invia allo standard output.
>il comando CAT viene spesso usato con simboli di redirect come >  e >>
>- ">" indirizza una cosa da una parte all'altra in questo caso potrebbe sovrascrivere da un file a un altro
>- ">>"è essenzialmente un append quindi aggiunge alla fine del file senza sovrascrivere
>![[Pasted image 20241023171750.png|500]]

>[!info]- **CUT** -> ti permette di selezionare alcuni campi, colonne all'interno di un file usando delle opzioni di comando. 
>- f1 consente di specificare la colonna in cui siamo creata da eventuali delimitatori o specificatori
>- d è un delimitatore che divide le righe in colonne basandosi su un carattere
>- c specifica i caratteri da estrarre tipo -c 1-4 per i primi 4 caratteri
>![[Pasted image 20241023174113.png|500]]

>[!info]- **DIFF** -> è la fantastica applicazione che permette di confrontare due file. Con DIFF puoi evidenziare tutte le modifiche che sono state fatte al file
>- w ignora gli spazi bianchi come caratteri di differenza
>- i ignora maiusc e minusc
>- q ti dice solo se i file sono diversi
>![[Pasted image 20241023181145.png|500]]

>[!info]- **HEAD**->  ti permette di vedere le prime righe di un file
>- default 10 righe
>- -n 5 si usa per indicare ad esempio le prime 5 righe
>![[Pasted image 20241023181511.png|500]]

>[!info]- **TAIL** -> ti permette di vedere le ultime righe di un file
>- -n indica il numero delle righe
>- -f refresha le ultime righe in real-time utile per analizzare eventuali log
>![[Pasted image 20241023181717.png|500]]

>[!info]- **LESS** -> è un visualizzatore di file che visualizza i file in base ai limiti del nostro display,
>quindi non carica tutto in memoria(in questo caso di tipo ram) a differenza di cat e altri comandi.
>quindi se ad esempio il nostro schermo visualizza 5 righe lui dinamicamente caricherà in 
>memoria il punto dove siamo e toglierà dalla memoria alcune cose che non vediamo
>- `-N` indica il numero di righe

>[!info]- **OD** -> visualizza i file in diversi formati
>- -x converte in esadecimale
>- -c converte in ASCII
>- -n specifica il numero di righe da visualizzare
>![[Pasted image 20241023185708.png|500]]

>[!info]- **SED** -> è un file editor che manipola i file 
>- sostituendo determinate porzioni di testo
>- eliminando righe o parti di testo specifiche
>- inserendo testo in porzioni specifiche
>- trasformando il testo mettendo maiuscole o minuscole
>- filtrare righe in base a dei criteri
>![[Pasted image 20241023190652.png|500]]

>[!info]- **SORT** dovrebbe prendere l'intero oggetto in memoria e ordinarlo.
>le opzioni per ordinarlo di default in ordine alfabetico
>- `-n` in ordine numerico
>- `-r` in ordine decrescente
>- `-k` indica la colonna
>- `-u` rimuove duplicati
>- `-o` manda in output in un file specifico
>![[Pasted image 20241023191436.png|500]]

>[!info]- **SPLIT**-> lo uso se ho un file di grandi dimensioni e voglio dividerlo in file più piccoli
>- `-l` indica il numero di n righe ciascuno
>- `-b` indica il peso in kilobyte (K), megabyte (M) o gigabyte (G).
>- `-a` poi un numero che indica il numero del suffisso di ogni file, creerà ad esempio con 
>  `-a 3` farà tutti piccoli file come "`output_aaa`, `output_aab`, ecc. 
>  ![[Pasted image 20241023192821.png]]

>[!info]- **TR** -> ci permette di sostituire un singolo carattere ovunque vogliamo.
>- `-d` per eliminare i file sostituiti
>uso dei redirect per salvare e mandare al comando `tr` il file da modificare
>![[Pasted image 20241023193910.png|500]]

>[!info]- **UNIQ** -> toglie le ripetizioni da un file e fa tante altre cose
> Funziona generalmente insieme al comando `sort`, poiché `uniq` elimina solo le righe duplicate adiacenti. IL `SORT` NON MODIFICA IL FILE, quindi se voglio salvare le modifiche dovrò inserirle in un altro file e ogni volta devo aspettare che il `sort` finisca
> - `-c` conta il numero di elementi
> - `-d` mostra solo i duplicati
> - 
> ![[Pasted image 20241023201601.png]]

>[!info]- **WC** ->  utilizzato per contare righe, parole e byte (o caratteri) in file o input.
>`-l` conta solo il numero di righe 
>`-w` conta solo il numero di parole 
>`-c` conta il numero di byte 
>`-m` conta il numero di caratteri 
>`-L` mostra la lunghezza della riga più lunga.
>![[Pasted image 20241023202004.png]]

### Precisazione sul significato di console
Console è un modo generico per definire tutti quei tipi di shell come `bash sh zsh ecc...` ovvero i vari software terminali
### COMANDI FONDAMENTALI CHE SI USANO PER UN FILE
Conosciamo bene Open, Read e Write ma esiste anche il comando di seek
>[!question]- cosa fà il comando di seek?
>il comando di seek è quel comando che ci consente di muoverci all'interno di un file.
>questo serve perchè i file non vengono scritti in modo sequenziale e quindi abbiamo bisogno di spostarci
### Spiegazione della pipe
significato di pipe a [[SISTEMI OPERATIVI LEZ.2]]
in termini di linguaggio bash le pipe si scrivono con `|` e sono utilizzate per collegare l'output di un comando all'input di un altro, permettendo la creazione di catene di comandi.
- il comando esegue prima il comando a sinistra del `|`
>[!info]- ESEMPIO
>![[Pasted image 20241023211140.png]]
>altro esempio:
>```bash
> cat nomefile |grep"-file"|sort|uniq -c|sort -k 1 -n -r
>```

==Come prendere dalla riga 17 alla 23==

Le funzioni sono ESTREMAMENTE ottimizzate
Ci sono alcune funzioni che sono un _**collo di bottiglia operazionale**_ come il sort 

## La shell
La shell è un ambiente di scripting che ci consente di creare file con una serie di comandi da eseguire in modo sequenziale e nella Shell introducono degli elementi condizionali(if,for ecc...)
Visto che ho dei condizionali posso fare molte computazioni
>[!info]- Definizione di Script
>Script sequenza di tutti i comandi necessari per eseguire quel compito
>
>

#### Script di tipo Bash
Il nostro script si chiamerà Bash-> "Bourne again-shell"
Il linguaggio Bash usa delle variabili d'ambiente che permettono di capire cosa c'è nel sistema
Cambiare le variabili d'ambiente nel PATH dove andare a cercare I vari comandi
Il s.o. è una struttura arborea estremamente complessa
PATH privilegiati 
PATH è una stringa di directory
Per vedere il corrente valore del PATH
==Echo $PATH==
Printenv stampa tutte le variabili del sistema 
Combinazioni tra variabili proprie e variabili personali
Diff tra printenv e Echo $PATH
Forse Path è una variabile tra tutte le variabili del sistema
Se io chiudo la sessione bash perdo le variabili che creo
Quando apro un terminale avvio una applicazione che si inizializza e poi esegue I comandi di base bash.rc 
Per creare una variabile per sempre bisogna scrivere il bash.rc per farle leggere per sempre modificare il file bash.rc con vim
Bash esegue e interpreta comandi che gli diamo su riga
Comandi come whoami hostname ecc ti danno informazioni sul sistema
Esercizio per creare uno script che ti saluta con il tuo nome con vim
```bash
MIONOME=$(whoami)
echo "CIAO" $MIONOME  
```
### comandi per usare history e semplici editing per comandi
CTRL+R PER GIRARE LA HISTORY
Oppure scrivi e poi freccia su

## COMANDI DI AIUTO🛟
==1h e 07==
INVENTORE DI HTML E WEB TIM BURTON
Diff tra HTML e XML
Linguaggio markup HTML troppe ridondanze ecc e anche XML
Ora si usa JSON
Yaml nuovo modo per scrivere in markup
Markup language= scriverla da internet
Al posto di aprire tag ecc si usano le graffe
==File JSON==
HTML->XML->JSON->YAML
==diff tra markup e markdown==
Cat dir | grep "testo" | wc
==-n -k -r??==
==RICORDARE TUTTI I COMANDI==

# TIPI DI PROGRAMMAZIONE
### NEGLI ANNI 60
- astrazione di memoria per variabili ecc...
- presenza di operazioni con flusso
	- salto incondizionato GOTO per definire le decisioni di algoritmo
- fine anni 60 revisione con programmazione strutturata e Jacopini Böhm
### Programmazione procedurale
Utilizzo di blocchi di codice identificati con nomi come:
- <span style="color: red;"><u>subroutine</u></span>: programmi per intero che possiamo eseguire più volte
- <span style="color: blue;"><u>procedure</u></span>: blocchi di istruzioni con parametri senza ritorno modificando variabili "globali"
- <span style="color: green;"><u>funzioni</u></span>: procedure ma meglio con ritorno di variabili
- <span style="color: orange;"><u>metodi</u></span>: fanno parte della object oriented
## PROGRAMMAZIONE A OGGETTI
Con la programmazione a oggetti ci si avvicina al pensiero umano rendendo il codice più intuitivo.
- Ci consente di separare il codice in oggetti ovvero creare elementi del nostro software che hanno il loro ciclo di vita e che possono essere creati e distrutti, un oggetto può essere di una singola tipologia
- Una famiglia di oggetti si chiama classe e indica un nuovo tipo di dato 
- Permette di suddividere i lavori tra vari programmatori 
#### PRINCIPI FONDAMENTALI
1) INCAPSULAMENTO
	- incapsulare il codice dividendo i problemi in più parti. Facendo così alcuni aspetti implementativi non sono visibili da alcuni utilizzatori del codice
	- (non significa che il codice sia più sicuro semplicemente è più  leggibile per chi non deve modificare determinate parti)
	- accessors: metodi che ti permettono di leggere delle informazioni private di una classe(get)
	- mutators: metodi che ti permettono di modificare una parte della classe(set)
2) ASTRAZIONE
	- programmi sfruttando gli oggetti e le classi senza interagire con cosa sono veramente quindi in modo astratto semplificando il codice
3) EREDITARIETÀ
	- L'ereditarietà consente di ridurre le ridondanze con sotto-gruppi che ereditano le caratteristiche del gruppo principale
4) POLIMORFISMO
- Il polimorfismo è la capacità di un linguaggio di programmazione di gestire in modo uniforme oggetti o funzioni che in realtà possono avere comportamenti diversi. In altre parole, uno stesso “nome” (un metodo o una funzione) può assumere forme differenti a seconda del contesto.
### **Linguaggi tipizzati**

- Un linguaggio può essere **debolmente tipizzato** (o "ipizzato" come avevi scritto, nel senso di più generico), cioè i tipi sono usati in modo meno rigoroso e possono anche essere convertiti implicitamente.
    
- Un linguaggio **fortemente tipizzato** invece ha un sistema di **type checking**: ogni variabile o funzione appartiene a un tipo preciso e ci sono regole rigide per l’uso e la compatibilità dei tipi.
    
- Nei linguaggi orientati agli oggetti (come Java, C++, C#, ecc.), quasi sempre si usa un **controllo dei tipi statico** (in compilazione), che permette anche di gestire il polimorfismo in modo sicuro.

### **Polimorfismo nelle classi**

- Immagina una **classe base** (ad esempio `Animale`) e più **classi derivate** (`Cane`, `Gatto`).
    
- Tutte queste classi possono avere un metodo con lo stesso nome, ad esempio `verso()`, ma ciascuna implementa il metodo in modo diverso.
    
- Se io scrivo `animale.verso()`, il risultato dipenderà dal **tipo effettivo** dell’oggetto (se è un cane abbaierà, se è un gatto miagolerà).
    
- Questo è il cuore del **polimorfismo ad oggetti**.
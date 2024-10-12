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
1) ENCAPSULATION
	- incapsulare il codice dividendo i problemi in più parti. Facendo così alcuni aspetti implementativi non sono visibili da alcuni utilizzatori del codice
	- (non significa che il codice sia più sicuro semplicemente è più  leggibile per chi non deve modificare determinate parti)
	- accessors: metodi che ti permettono di leggere delle informazioni private di una classe(get)
	- mutators: metodi che ti permettono di modificare una parte della classe(set)
2) ABSTRACTION
	- programmi sfruttando gli oggetti e le classi senza interagire con cosa sono veramente quindi in modo astratto semplificando il codice
3) INHERITANCE
	- L'ereditarietà consente di ridurre le ridondanze con sotto-gruppi che ereditano le caratteristiche del gruppo principale
4) POLYMORPHISM
	- parliamo prima di linguaggi ipizzati(1) o tipizzati(2), ovvero dei tipi di dato sono generici nel caso 1 oppure appartengono a gruppi e sottogruppi nel caso 2 con typechecking
	- un linguaggio con programmazione a oggetti e' al 90% con typechecking
	- più oggetti di classe diverse che fanno parte di una classe superiore e che hanno stesso metodo ma modificato
	- override: quando una classe ha un metodo con un nome e una sottoclasse ha un metodo con lo stesso nome ma che fa cose diverse(in fase di runtime si capisce il da farsi)
	- overload: quando in una classe si scrive più di un metodo con lo stesso nome ma con parametri diversi(in fase di compilazione si capisce il da farsi)

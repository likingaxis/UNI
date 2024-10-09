# TIPI DI PROGRAMMAZIONE
### NEGLI ANNI 60
- astrazione di memoria per variabili ecc...
- presenza di operazioni con flusso
	- salto incondizionato GOTO per definire le decisioni di algoritmo
- fine anni 60 revisione con programmazione strutturata e Jacopini Böhm
### Programmazione procedurale
Utilizzo di blocchi di codice identificati con nomi come:
- ==**subroutine**==: programmi per intero che possiamo eseguire piu' volte
- ==**procedure**==: blocchi di istruzioni con parametri senza ritorno modificando variabili "globali"
- ==**funzioni**==: procedure ma meglio con ritorno di variabili
- ==**metodi**==:fanno parte della object oriented
## PROGRAMMAZIONE A OGGETTI
Separare in oggetti ovvero gli elementi del nostro software che hanno il loro ciclo di vita e che possono essere creati e distrutti
Con diverse tipologie
Permette di suddividere i lavori con schemi ad albero ad esempio
#### PRINCIPI FONDAMENTALI
1) ENCAPSULATION
	- incapsulare il codice dividendo i problemi in più parti
	- accessors: conoscere uno stato del software
	- mutators: cambi una parte senza conoscere dettagli implementativi
2) ABSTRACTION
	- programmi sfruttando gli oggetti senza interagire con cosa sono veramente quindi in modo astratto
3) INHERITANCE
	- L'ereditarietà consente di ridurre le ridondanze con sotto gruppi che ereditano le caratteristiche del gruppo principale
4) POLYMORPHISM
	- parliamo prima di linguaggi ipizzati(1) o tipizzati(2), ovvero dei tipi di dato sono generici nel caso 1 oppure appartengono a gruppi e sottogruppi nel caso 2 con typechecking
	- un linguaggio con programmazione a oggetti e' al 90% con typechecking
	- un oggetto può assumere più tipi e presentarsi come uno dei tipi che può assumere
	- override: 
	- overload:
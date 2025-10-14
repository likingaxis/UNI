# DBMS vs File System
il DBMS non è l'unico modo efficiente per gestire un insieme di dati bensì ne esistono molti e dipendono dall'utilizzo che ne vogliamo fare
un esempio sono i File System
I DBMS non sono usati per un solo scopo ma per scopi diversi e presenta un dizionario con la descrizione dei vari dati centralizzata
### Modello di dati
Un modello di dati è un insieme di regole e costrutti e viene usato per creare schemi per i database con descrizioni dei dati, i loro vincoli ecc...
costituito più precisamente definito anche da Ullman da:
- costrutti sintattici per definire i dati
- regole semantiche per interpretare i dati
- linguaggi per manipolare i dati
## Conosceremo due tipi di modelli
### Logico
Ha lo scopo di descrivere il modo in cui i dati sono organizzati nel DBMS in un modo che sia visibile all'utente si divide a sua volta in diversi tipi
- Gerarchico e reticolare
	- utilizzato in modo esplicito per puntatori e record
- Modello ad oggetti
	- l'informazione è sottoforma di oggetti
	- mercato di nicchia
- Relazionale
	- i riferimenti che ci sono tra i dati in strutture differenti sono rappresentate con dei valori, questi riferimenti vengono detti relazioni
	- descrivono i concetti nel mondo reale


### Concettuale
Un modello definito è lo schema E-R e il modello classi associazioni UML
![[Pasted image 20250313213952.png]]

# Schemi e istanze
in ogni base di dati esistono schemi e istanze
### Schema 
- descrive la struttura del database non varia troppo nel tempo
	- le intestazioni ad esempio
![[Pasted image 20250313214324.png]]

### Istanza
- I valori stessi che variano molto nel tempo
	- ad esempio il corpo di ciascuna tabella
![[Pasted image 20250313214341.png]]

# Architettura standard di un DBMS
È a tre livelli
![[Pasted image 20250313214549.png]]
- schema logico
	- descrizione della base di dati nel modello logico del DBMS
- schema fisico
	- rappresentazione dello schema logico per mezzo di strutture di memorizzazione
		- tipo memorizzazione dei byte con un vettore ecc...
- schema esterno
	- descrizione di parte della base di dati in un modello logico
		- schema costituito da ad esempio una funzione
		- $f(i) = \sum_{j=1}^{m} a_{i,j}$
		- vista personalizzata su dati

<font color="#c0504d">Indipendenza fisica</font>
<font color="#c0504d">logica</font>
### Per fare operazioni su dati abbiamo il  DML
- Data Manipulation Language
- Attraverso Query Language
Esempio di DML con una determinata istanza
Seleziona i campi docenti dalla tabella orario che abbiano solo aula=N1
```SQL
SELECT docente
FROM orario
WHERE aula = 'N1';
```
### Per fare operazioni su schemi abbiamo DDL
- Data Definition Language
Esempio di DDL con una creazione di una tabella
```SQL
CREATE table orario(
	insegnamento char(20);
	docente char(20);
	aula char(4);
	ora char(5);
	)
```
## Diversi tipi di linguaggi in un DBMS
- Linguaggi testuali interattivi come SQL
- comandi immersi in un linguaggio ospite come Java C Spark etc...
- comandi immersi in un linguaggio ad hoc con altre funzionalita
- interfacce amichevoli senza codici
## Esempio di Query che generano tabelle
```SQL
SELECT corso,aula,piano
FROM aule,corsi
WHERE Aula='N3'
AND piano='Terra';
```
# Transazioni
Proprieta acide
- le vedremo nelle prossime lezioni
Transazioni insieme di piccole transazioni che devo fare tutte
come il prelievo dal conto corrente che fa transazioni che tolgono soldi mettono ecc...

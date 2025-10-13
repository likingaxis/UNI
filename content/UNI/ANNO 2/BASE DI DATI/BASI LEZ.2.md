# Differenza tra Dato e Informazione
Dato: in informatica e una singola informazione codificabile, come un bit 
Informazione: notizia, dato o elemento che consente di avere conoscenza su fatti o situazioni
Una informazione sono un insieme di dati collegati ad esempio da una loro logica
### Definizione di sistema informativo
Componente di una organizzazione che gestisce le informazioni
Un sistema informativo va studiato in base al contesto in cui esso e inserito
# Database
e una collezione di dati all'interno di un sistema informativo
- ha il compito non solo di memorizzarli ma anche di rappresentarli con le corrette relazioni
# DBMS(Database Management System)
Il nome del software dato per gestire i dati del Database con collezioni di dati che siano(non per forza):
- Grandi
- Persistenti nel tempo
- condivisi tra più utenti
	- riducendo 
		- ridondanza dei dati
		- inconsistenza dei dati
Un DBMS deve in particolare garantire
- affidabilità, evitare errori
- privatezza dei dati
- efficienza e quindi un sistema efficace 
## Alcuni esempi di DBMS
📍 DB2 
📍 Oracle 
📍 SQLServer 
📍 Postgres 
📍 MySQL 
📍 SQLite
# Data Independence
È alla base del concetto di gestione dei database
- concetto che i dati hanno una loro indipendenza logica
- se cambio sistema o computer posso comunque usare i dati
# Archiviazione dei file
# Approccio senza DBMS
Di solito un comune programma senza uso di database salva le informazioni e i dati all'interno del file system
Ogni file e composto da record all'interno di questi record abbiamo memorizzati i vari dati elementari come
- attributi
- campi
più programmi possono condividere gli stessi file attraverso file condivisi
I file possono avere diversi formati che sono incompatibili e quindi li rendono più difficili da condividere su diversi programmi
![[Pasted image 20250307151843.png|300]]
# Approccio con DBMS
Il DBMS fa da intermediario in modo indipendente dalle applicazioni che vengono usate
esso offre una interfaccia che saranno le applicazioni a dover usare e a cui si dovranno adattare
Grazie a questo approccio riusciamo a ridurre i tempi di progettazione e si semplifica e standardizza
![[Pasted image 20250307151812.png|500]]


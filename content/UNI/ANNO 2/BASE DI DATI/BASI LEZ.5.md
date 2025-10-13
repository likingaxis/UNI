I **vincoli d’integrità** sono regole che una base di dati deve rispettare per garantire la correttezza e la coerenza delle informazioni. Esistono basi di dati che, pur essendo sintatticamente corrette, contengono informazioni non valide per l’applicazione. 
![[Pasted image 20250322125510.png]]

I vincoli servono proprio a evitare questi casi, assicurando che i dati riflettano la realtà del sistema che rappresentano.

I vincoli sono quindi delle funzioni booleane che associano ad ogni istanza un valore **vero** o **falso**.

### **Tipologie di vincoli**

I vincoli si distinguono in:
1. **Vincoli intrarelazionali**, che riguardano singole relazioni:
    - **Vincoli di dominio**: limitano i valori ammessi per un attributo (es. un voto deve essere compreso tra 18 e 30).
    - **Vincoli di ennupla**: stabiliscono condizioni sui valori degli attributi all’interno di una singola ennupla (sono indipendenti dalle altre ennuple).
2. **Vincoli interrelazionali**, che regolano le relazioni tra diverse tabelle:
    - **Vincoli di integrità referenziale**: impongono che i valori di un attributo in una tabella siano presenti come chiave primaria in un’altra.

### **Vincoli di ennupla**
I vincoli di ennupla garantiscono che i dati all’interno di una riga siano logicamente coerenti tra loro. 
Un esempio è quello di una tabella di stipendi, dove il valore lordo deve essere sempre la somma di netto e ritenute.
![[Pasted image 20250322125520.png]]

### **Chiavi e schemi di relazione**
Le chiavi servono a **identificare univocamente** ogni riga (o **ennupla**) di una tabella. 
Senza le chiavi, potremmo avere dati duplicati e perdere la possibilità di distinguere in modo chiaro un'entità da un'altra.

Esistono diverse tipologie di chiavi:
- **Superchiave**: un insieme di attributi che distingue univocamente ogni ennupla.
- **Chiave primaria**: una superchiave scelta per identificare le righe, su cui non sono ammessi valori nulli.
- **Chiavi alternative**: altre superchiavi possibili ma non scelte come chiave primaria
	![[Pasted image 20250322125534.png]]
	La chiave in questo caso è TUTTA {Cognome, Nome, Nascita} perché: 
	- **Rossi, Mario, 5/12/78** compare solo una volta. ✅
	- **Rossi, Mario, 3/11/76** compare solo una volta. ✅
	- **Neri, Piero, 10/7/79** compare solo una volta. ✅
	- **Neri, Mario, 3/11/76** compare solo una volta. ✅
	- **Rossi, Piero, 5/12/78** compare solo una volta. ✅
	Se vedi io ho scelto una chiave per cui tutte le RIGHE sono diverse TRA LORO.


Ad esempio, considera una tabella **Studenti**:

| Matricola | Nome  | Cognome | Data di Nascita |
| --------- | ----- | ------- | --------------- |
| 12345     | Mario | Rossi   | 01-02-2000      |
| 12346     | Luca  | Bianchi | 03-04-2001      |
| 12345     | Mario | Neri    | 01-02-2000      |

- `{Matricola}` è una superchiave perché identifica ogni studente, ed è minimale perché nell'insieme c'è solo un elemento.
- `{Matricola, Cognome}` è anch’essa una superchiave, ma include un attributo ridondante (basta la Matricola da sola).

##### Vincoli, schemi e istanze
Un database rappresenta una parte del mondo reale e deve rispettare alcune regole per essere considerato **corretto**.
- **Vincoli**: regole che assicurano la validità dei dati.
- **Schema**: struttura del database con le sue tabelle e relazioni.
- **Istanza**: un insieme di dati che devono rispettare i vincoli dello schema.
Un'istanza è considerata **valida** se soddisfa i vincoli, anche se può rispettare accidentalmente altri vincoli "per caso".
	es. magari impongo come vincolo solo la matricola, ma a culo anche il cognome può essere usato (quindi "per caso").
![[Pasted image 20250322125551.png]]


Una relazione (tabella) **non può avere due righe uguali**, quindi deve sempre esistere **almeno una chiave** per distinguerle.

Si prediligono sempre superchiavi "minimali"

### **Chiavi e valori nulli**
La presenza di valori nulli in una chiave crea problemi, perché impedisce di identificare univocamente una riga e di realizzare riferimenti da altre tabelle. 
Per questo motivo, **nelle chiavi primarie non sono ammessi valori nulli**.

### **Vincoli di integrità referenziale**
I dati tra tabelle diverse devono essere coerenti. 
Per esempio, una tabella delle infrazioni stradali deve contenere solo codici di vigili presenti nella tabella dei vigili. 
![[Pasted image 20250322125623.png]]
Se un valore della colonna "Vigile" non trova corrispondenza nella tabella "Vigili", si ha una **violazione del vincolo di integrità referenziale**.

![[Pasted image 20250322125635.png]]
Oppure stessa cosa con provincia e numero.

Quindi, un vincolo di integrità referenziale fra gli attributi `X` di una relazione `R1` e un'altra relazione `R2` impone ai valori su `X` in `R1` di comparire come valori della chiave primaria di `R2`.

###### VIOLAZIONE
![[Pasted image 20250322125648.png]]

### **Gestione delle violazioni dei vincoli referenziali**
Quando un’operazione minaccia l’integrità referenziale, il sistema può adottare diverse strategie:
1. **Rifiutare l’operazione**, bloccando la modifica.
2. **Eliminazione in cascata**, rimuovendo tutti i dati correlati.
	![[Pasted image 20250322125703.png]]
3. **Introduzione di valori nulli**, per mantenere il riferimento senza violare il vincolo.
	![[Pasted image 20250322125714.png]]Così non devo eliminare TUTTA la riga nelle varie tabelle ma posso far sì che dalla tabella principale non posso accedere a quella secondaria.

Questi meccanismi garantiscono che il database rimanga coerente anche in presenza di operazioni di aggiornamento o eliminazione.
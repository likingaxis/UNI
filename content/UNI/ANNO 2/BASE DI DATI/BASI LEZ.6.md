## 🧠 Cos’è un Modello di Dati?

Quando ci troviamo a progettare un database, dobbiamo innanzitutto chiederci: **come rappresentare la realtà con i dati?** Per farlo, ci serviamo di un **modello dei dati**, ovvero un insieme di regole e strumenti che ci permettono di **organizzare le informazioni**, definirne la **struttura**, e capire **come interagiscono** tra loro.

Un modello di dati è un po’ come una mappa: non rappresenta tutto nei minimi dettagli, ma fornisce una **visione chiara dei concetti fondamentali** e delle loro connessioni.

### 🧱 Esempio

Pensa al gestionale di una palestra. I dati che vuoi rappresentare sono: iscritti, abbonamenti, corsi, allenatori, prenotazioni. Il modello di dati ti aiuterà a organizzare tutto ciò in modo logico e coerente, evitando confusione e ridondanza.
## 🔍 Tipi di Modelli

I modelli si dividono in due grandi categorie:
### 1. **Modelli Logici**

Sono quelli usati **nei DBMS**, i software che gestiscono i database (come MySQL, PostgreSQL, Oracle...). Descrivono **come** sono organizzati i dati nel sistema informatico.

Esempi di modelli logici:

- **Relazionale** (il più comune): i dati sono organizzati in **tabelle**.
    
- **Gerarchico**: struttura ad albero.
    
- **Reticolare**: struttura a grafo.
    
- **A oggetti**: simile alla programmazione a oggetti.
    
### 2. **Modelli Concettuali**

Sono più **astratti**: servono per rappresentare la realtà senza preoccuparsi di **come** sarà implementata. Sono ideali per la **fase di analisi e progettazione**.

Il più noto è il **modello Entità-Relazione (ER)**, che descrive:

- Quali sono gli oggetti rilevanti (entità)
    
- Come sono collegati (relazioni)
    
- Quali informazioni portano (attributi)
#### Modelli moderni:
- Modello ER Esteso (EER): include costrutti avanzati come l’ereditarietà. 
- UML (Unified Modeling Language): un linguaggio standardizzato per la progettazione dei dati; 
- Modello concettuale → dati e relazioni attraverso uno schema; 
- Modello logico → descrive il modo attraverso il quale i dati sono organizzati negli archivi del calcolatore; 
- Modello fisico → descrive come i dati sono registrati nelle memorie di massa.
#### Come passare da un modello all'altro
![[Pasted image 20250322110805.png]]
La progettazione di un database avviene in **3 fasi**, che rappresentano **livelli crescenti di dettaglio**:
1. **Progettazione Concettuale**
    - Cosa vogliamo rappresentare?
    - Quali sono gli oggetti? Come si collegano tra loro?
    - Esempio: _Studente_, _Esame_, _Corso_.
2. **Progettazione Logica**
    - Come trasformare quei concetti in strutture logiche?
    - Si usano tabelle, chiavi primarie, tipi di dato.
3. **Progettazione Fisica**
    - Dove e come salvare i dati su disco?
    - Ottimizzazione della memorizzazione, prestazioni, indici.
## 📐 Il Modello Entità-Relazione (ER)

È un modello **concettuale** che ci aiuta a rappresentare una realtà attraverso:
- **Entità**
- **Relazioni**
- **Attributi**
- **Cardinalità**
- **Chiavi**

È molto usato perché **separa l’analisi logica dalla tecnologia**, permettendo di lavorare sulla struttura prima di pensare al database vero e proprio.

---

## 📦 ENTITÀ: cosa sono?

Un’entità è un oggetto, **concreto o astratto**, che ha **significato proprio** e **rilevanza nel contesto che si sta studiando**.Sono l'astrazione di quello che poi diventerà una tabella

### 🧾 Esempi:
- In una **scuola**: _Studente_, _Corso_, _Docente_
- In un **e-commerce**: _Cliente_, _Ordine_, _Prodotto_
- In una **banca**: _Conto_, _Cliente_, _Movimento_

Ogni entità è rappresentata da un **tipo entità** (es. _Studente_) e da **istanze** (es. _Mario Rossi_).

---

## 🔗 RELAZIONI: come si collegano le entità?

Una **relazione** (o _relationship_) rappresenta **un legame logico** tra due o più entità.
### 🧾 Esempio:
Nel contesto universitario:
- _Studente_ partecipa alla relazione _Sostenere_ con _Esame_.
Oppure in un autosalone:
- _Persona_ e _Automobile_ sono collegate dalla relazione _Possiede_.
    - Una persona può possedere più auto.
    - Ogni auto è posseduta da una persona.
![[Pasted image 20250322112403.png]]
Le relazioni possono anche:
- Essere **unidirezionali** (si rappresenta un solo verso)
- Essere **ricorsive**: un’entità si collega con sé stessa.
- ad esempio manager è una istanza dell'entità dipendente e può avere una relazione con un'altra istanza
![[Pasted image 20250322113639.png]]
- Coinvolgere più di due entità (relazioni **ternarie** o più).
![[Pasted image 20250322113710.png|400]]
---
## 📎 ATTRIBUTI: cosa descrive un'entità o relazione?

Gli attributi sono **informazioni specifiche** associate a un’entità o a una relazione. Servono a **descriverne le caratteristiche**.

### 🧾 Esempio:

Per l’entità _Automobile_, possiamo avere:
- `numero_telaio` (univoco)
- `modello`
- `produttore`
- `cilindrata`
- `prezzo`

![[Pasted image 20250322115309.png|500]]
in questo caso abbiamo studente che ha $cognome+nome$ con chiave primaria
#### Attributi nelle relazioni
![[Pasted image 20250322115501.png]]
Nella relazione tu hai gli attributi che riguardano la singola azione

---
#### PROPRIETÀ DEL MODELLO RELAZIONALE 
- Ogni entità deve avere una chiave primaria. 
- La chiave primaria è un attributo speciale che identifica in modo univoco ogni istanza dell'entità. 
    - La chiave primaria non può avere valori ripetuti; 
        
#### DOMINIO di un attributo 
Il dominio definisce quali valori un attributo può assumere. 
Caratteristiche del dominio: 
- Tipo di dato → (numero, testo, data, ecc.). 
- Lunghezza → Quanti caratteri o cifre può contenere. 
- Intervallo → Quali valori sono accettabili. 
- Vincoli → Regole aggiuntive sui valori (es. "deve essere maggiore di zero"). 
- Supporto del valore NULL → Se l’attributo può essere lasciato vuoto o meno. 
- Valore di default → Valore che viene assegnato automaticamente se non specificato. 

Proprietà delle Chiavi Primarie e Chiavi Esterne 

Chiave primaria: 
- Deve essere univoca → Non si possono avere due record con lo stesso valore. 
- I valori NULL non sono ammessi → Ogni record deve avere una chiave primaria. 

Chiave esterna: 
- Collega una tabella a un'altra (ma questo lo vedrai più avanti). 
- Deve avere lo stesso tipo di dato, lunghezza e formato della chiave primaria a cui si riferisce. 
    - Esempio del vigile della scorsa lezione, una chiave che fa riferimento a un'altra chiave. 
### Entità forti ed entità deboli 

- Entità forti → Hanno una chiave primaria e possono esistere senza dipendere da altre entità. 
- Entità deboli → Non hanno una chiave primaria e devono essere collegate a un'entità forte per avere senso. 
![[Pasted image 20250322121353.png]]
- Movimento non ha senso se sta da sola deve per forza dipendere da altro
Un’entità debole esiste solo se esiste l’entità forte a cui è collegata.

## 🔐 CHIAVI: come si identificano le entità?
Una **chiave primaria** è un attributo (o più) che **identifica univocamente** ogni istanza dell’entità.
### 🧾 Esempi:
![[Pasted image 20250322120404.png]]
## 🔐 CHIAVI ARTIFICIALI E IDENTIFICATORI PROGRESSIVI
Spesso, anche quando abbiamo attributi che potrebbero identificare univocamente un'entità (come il numero di telaio di un'auto o il codice fiscale di una persona), si preferisce usare un **identificatore numerico progressivo**, detto **chiave artificiale**.

Questo per semplicità: è più efficiente, facile da ricordare e non cambia nel tempo.
### 🧾 Esempio:
Invece di usare `numero_telaio`, posso assegnare a ogni auto un `ID` auto-incrementante:
- Auto 1 → ID = 1
- Auto 2 → ID = 2  
    Anche se le due auto hanno modelli e targhe diverse, le identifico tramite un **intero semplice**.
---

## 📏 PROPRIETÀ DELLE CHIAVI

Le chiavi primarie devono seguire delle regole:
- **Non possono essere vuote (no NULL)**
- **Devono essere univoche**
- Ogni entità **deve avere una chiave primaria**

Per le **chiavi esterne** (cioè attributi che collegano entità diverse), valgono alcune condizioni:
- Devono avere **stesso tipo, lunghezza e formato** della chiave primaria a cui si riferiscono.
---

## 🧍‍♂️ ENTITÀ FORTI E DEBOLI
Le **entità forti** sono quelle che **possono esistere da sole**, mentre le **entità deboli** hanno senso **solo in relazione a un’altra entità**.
### 🧾 Esempio reale (banca):
- _Cliente_ → entità forte: esiste a prescindere.
- _Conto_ → anch’essa forte: identificata da `num_conto`.
- _Movimento_ → entità debole: un versamento o un prelievo **ha senso solo se associato a un conto**.
![[Pasted image 20250322123107.png]]
Spesso si può trasformare un'entità debole in forte **aggiungendo un ID numerico progressivo**.

---
## 🔢 MOLTEPLICITÀ E CARDINALITÀ

La **molteplicità** indica **quanti elementi** di un'entità possono essere collegati a un’altra entità attraverso una relazione.
### Notazione:
- (1,1): obbligatorio e unico
- (0,N): facoltativo e multiplo
- (1,N): obbligatorio e multiplo
- (0,1): facoltativo e unico
Da questa combinazione derivano **tre tipi di relazioni**:

---

### 🔁 RELAZIONI 1:1

Un'istanza di una entità può essere collegata **al massimo a una** dell’altra, e viceversa.
### 🧾 Esempio:

![[Pasted image 20250322124257.png|600]]
---

### 🔀 RELAZIONI 1:N
Un’istanza di una entità può essere collegata a **più istanze** dell’altra, ma non viceversa.
### 🧾 Esempio:

![[Pasted image 20250322124338.png|500]]

---

### 🔁 RELAZIONI N:N
Un’istanza può essere collegata a **più istanze** da entrambi i lati.
### 🧾 Esempio:
![[Pasted image 20250322124407.png|500]]

---

## 🧬 EREDITARIETÀ e RELAZIONE IS-A

Nel mondo reale, alcune entità sono **sottoinsiemi** di altre: sono **più specializzate**.

La relazione **IS-A** (è un) serve per rappresentare questo.
### 🧾 Esempi:
![[Pasted image 20250322125115.png]]
![[Pasted image 20250322125127.png]]
La proprietà è **transitiva**: un _FuoriCorso_ è anche uno _Studente_ e quindi una _Persona_.

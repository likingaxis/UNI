### 🧠 **Introduzione al Modello Entità-Relazione (ER)**

Quando si progetta una **base di dati**, lo scopo è rappresentare in modo efficace una certa realtà — ad esempio un’azienda, una scuola, un sito web — attraverso i dati. Per fare ciò si usano dei **modelli**: strumenti astratti che ci aiutano a descrivere i dati, a organizzarli, e a rappresentarne le relazioni.

I **modelli dei dati** sono un po’ come i linguaggi: ci offrono regole e costrutti per esprimere concetti. Esistono modelli **logici**, che sono quelli implementati nei sistemi di gestione dei database (DBMS) — come il **modello relazionale**, il **gerarchico**, il **reticolare**, o quello **a oggetti**. E poi ci sono i **modelli concettuali**, più astratti, che vengono usati nelle prime fasi della progettazione. Tra questi, il più famoso è proprio il **modello Entità-Relazione**, spesso abbreviato in **ER**.

---

### 🏗️ **Fasi della Progettazione di una Base di Dati**

La progettazione di una base di dati avviene su tre livelli:

1. **Progettazione concettuale**: rappresenta i concetti del mondo reale. È come se ci chiedessimo: _Quali sono gli oggetti fondamentali di questa realtà? Come si relazionano tra loro?_
    
2. **Progettazione logica**: trasforma la visione concettuale in una forma più tecnica, adatta al DBMS. Se prima parlavamo di concetti, ora parliamo di **tabelle**, **chiavi** e **relazioni**.
    
3. **Progettazione fisica**: si occupa dei dettagli su come i dati sono memorizzati su disco (es. struttura degli indici, partizionamento, ecc.).
    

Immagina di voler creare un database per un’università. A livello concettuale definisci entità come _Studente_, _Corso_, _Esame_. A livello logico, crei le **tabelle** corrispondenti. A livello fisico, decidi come archiviare queste tabelle nel sistema.

---

### 🔍 **Il Modello Entità-Relazione: Cos'è e Come Funziona**

Il **modello ER** è uno strumento per descrivere in modo astratto i dati e le loro relazioni. È utile perché ci permette di progettare **indipendentemente** dal tipo di database o dal linguaggio che useremo per implementarlo.

#### ✅ Entità

Un'entità è un **oggetto del mondo reale** che vogliamo rappresentare. Può essere una cosa concreta (una persona, un’auto) o astratta (una prenotazione, un esame). L’importante è che abbia senso anche presa da sola.

**Esempi:**

- _Studente_, con attributi come nome, cognome, matricola.
- _Automobile_, con numero di telaio, marca, modello.
- _Conto corrente_, con numero conto, tipo, saldo.

Ogni entità può avere **istanze**: ogni singolo studente è un’istanza dell’entità _Studente_.

---

#### 🔗 Relazioni

Una **relazione** rappresenta un **collegamento logico** tra due o più entità. È il modo in cui esprimiamo che gli oggetti del nostro mondo interagiscono.

**Esempio**: La relazione _Possiede_ tra _Persona_ e _Automobile_. Ogni persona può possedere una o più auto, e ogni auto deve essere posseduta da una persona.

**Altri esempi**:

- _Studente - Iscritto - Corso_
- _Dipendente - Lavora per - Azienda_
- _Autore - Scrive - Libro_

Le relazioni possono anche:

- **Essere ricorsive** (un'entità si relaziona con sé stessa, es. _Persona - Essere Genitore - Persona_)
- **Coinvolgere più entità** (relazioni ternarie, es. _Chirurgo - Effettua - Intervento - In - Sala Operatoria_)

---

#### 🧾 Attributi

Ogni entità (o relazione) ha **attributi**, che sono le **proprietà descrittive**.

**Esempio**: Per l’entità _Automobile_, gli attributi potrebbero essere:

- numero telaio
- modello
- cilindrata
- prezzo

Gli attributi hanno **formato** (stringa, numero, data), **dimensione**, possono essere **obbligatori o opzionali**, e hanno un **dominio** (insieme dei valori possibili).

---

#### 🔐 Chiavi Primarie e Artificiali

Una **chiave primaria** è un attributo (o un insieme di attributi) che **identifica univocamente** ogni istanza di un’entità.

**Esempio**:

- Per _Automobile_, potrebbe essere il numero di telaio.
- Per _Studente_, potrebbe essere la combinazione di nome, cognome e data di nascita (anche se è meglio usare qualcosa di unico, come la _matricola_).

A volte usiamo **chiavi artificiali**, cioè **ID numerici progressivi** che non hanno significato ma servono solo a identificare univocamente (es. `ID_cliente`).

Anche le **relazioni** possono avere attributi: ad esempio, nella relazione _Acquistare_ tra _Persona_ e _Automobile_, potremmo avere attributi come `data_acquisto`, `prezzo`.

---

### 🧱 Entità Forti e Deboli

- **Entità forte**: ha una propria chiave primaria, può esistere autonomamente.
- **Entità debole**: non ha una chiave autonoma, ha senso solo se associata a un'entità forte.

**Esempio**:

- _Conto_ è un’entità forte.
- _Movimento bancario_ è un’entità debole, perché esiste solo in relazione a un conto.

Spesso si assegna un ID anche alle entità deboli per renderle forti.

---

### 🔢 Molteplicità e Cardinalità

La **molteplicità** definisce **quanti oggetti** possono partecipare a una relazione. Si usa una notazione come (1,1), (0,N), ecc.

- **1:1** → un oggetto si collega a uno solo (es. _Persona - CartaIdentità_)
- **1:N** → uno si collega a molti (es. _Cliente - Ordina - Ordini_)
- **N:N** → molti a molti (es. _Studente - Frequenta - Corso_)

---

### 👨‍👩‍👧 Ereditarietà e IS-A

Nel modello ER possiamo modellare **sottoinsiemi di entità** tramite l’associazione **IS-A**, cioè una **relazione di ereditarietà**.

**Esempio**:

- _Persona_ può essere specializzata in _Studente_, che a sua volta può essere specializzato in _Fuori corso_.
- Le entità figlie **ereditano** gli attributi della madre (es. _Studente_ eredita nome, cognome da _Persona_).

Non si rappresentano di nuovo nel diagramma, ma sono **implicitamente ereditati**.

Nota: nel modello ER classico, **non si può avere ereditarietà multipla** (cioè un’entità figlia non può avere due padri).

---

### 🧬 Generalizzazione

La **generalizzazione** è l’operazione inversa alla specializzazione: si parte da più entità specifiche e si uniscono in una entità più generale.

**Esempio**:

- _Professore_, _Studente_, _Tecnico_ → tutti possono essere generalizzati come _Persona_.

Le entità figlie possono essere:

- **Disgiunte**: un’istanza è solo in una sottoclasse.
- **Overlapping**: un’istanza può essere in più sottoclassi.
- **Complete**: tutte le istanze della superclasse appartengono a una sottoclasse.
- **Incomplete**: alcune istanze non appartengono a nessuna sottoclasse.

---

Questa è la panoramica completa dei primi 40 concetti del corso. Fammi sapere se vuoi che continui con le slide successive o se vuoi trasformare questo in una presentazione, un'infografica o un file PDF!
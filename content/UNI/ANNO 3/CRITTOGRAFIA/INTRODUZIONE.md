TUTTO IL CAPITOLO 1 DEL LIBRO
## **Introduzione alla crittografia**

Il capitolo presenta una panoramica dei principali problemi studiati nella crittografia e delle tecniche utilizzate per risolverli.  
L’obiettivo è introdurre, in modo non tecnico, i concetti fondamentali che saranno approfonditi nei capitoli successivi.

---

### **1.1 – Crittosistemi e strumenti di base**

#### **Crittosistemi a chiave segreta**

È il modello più antico: due persone (Alice e Bob) condividono una chiave segreta usata per **cifrare (encryption)** e **decifrare (decryption)** i messaggi.  
Il messaggio originale (plaintext) diventa un testo cifrato (ciphertext) leggibile solo con la chiave corretta.  
La sicurezza dipende dal segreto della chiave e dalla sua lunghezza: più ampio è lo spazio delle chiavi, più difficile è un **attacco per forza bruta**.  
L’insieme delle tecniche usate per tentare di “rompere” un sistema cifrato si chiama **crittanalisi**.  
Oltre alla protezione dei dati trasmessi, la crittografia moderna viene impiegata anche per **proteggere i dati memorizzati**, come file su dischi, database o cloud.

Il limite principale di questo modello è la **distribuzione della chiave**: Alice e Bob devono accordarsi sulla chiave in modo sicuro prima di comunicare, il che può essere complesso se si trovano in luoghi diversi.

#### **Crittosistemi a chiave pubblica**

Introdotti negli anni ’70 da **Diffie e Hellman**, prevedono due chiavi diverse:

- una **pubblica** (nota a tutti) per cifrare;
    
- una **privata** (nota solo al destinatario) per decifrare.  
    Esempio classico: **RSA**.  
    Questo elimina la necessità di una chiave condivisa, ma introduce un nuovo problema: come garantire che una chiave pubblica sia autentica?  
    La soluzione è l’uso di **certificati digitali**, firmati da autorità di fiducia.
    

#### **Cifrari a blocchi e a flusso**

- **Block cipher:** divide il testo in blocchi fissi (es. 128 bit) e li cifra uno per volta.
    
- **Stream cipher:** genera un flusso continuo di bit (keystream) combinato con il messaggio tramite XOR.  
    I sistemi a chiave pubblica sono sempre a blocchi; quelli a chiave segreta possono essere di entrambi i tipi.
    

#### **Crittografia ibrida**

Combina i vantaggi dei due modelli:  
Alice genera una chiave segreta casuale per cifrare il messaggio con un algoritmo veloce, poi cifra quella chiave con la chiave pubblica di Bob.  
Bob decifra prima la chiave segreta e poi il messaggio.  
È il principio alla base dei protocolli **HTTPS/TLS**.

---

### **1.2 – Integrità dei messaggi**

La cifratura garantisce la **riservatezza**, ma non l’**integrità**: un avversario attivo può modificare o falsificare messaggi.  
Per questo, oltre all’encryption, servono strumenti che assicurino che i dati non siano stati alterati e che provengano davvero dal mittente.

#### **Avversario passivo e avversario attivo**

- Un **avversario passivo** (eavesdropper) può **intercettare i messaggi** ma **non li altera**.  
    Il suo obiettivo è leggere informazioni riservate, e la **crittografia** serve a difendersi da questo tipo di minaccia. FIGURA 1.1
    
- Un **avversario attivo** può invece **modificare, falsificare o dirottare** i messaggi durante la trasmissione.  
    Può alterare i dati, fingere di essere un altro mittente o redirigere la comunicazione verso terzi.  
    Contro questi attacchi servono strumenti che garantiscano **autenticità e integrità**, come **MAC** e **firme digitali**. FIGURA 1.2

![[Pasted image 20251007173356.png]]

Un esempio di vulnerabilità a un attacco attivo è il **bit-flipping attack** nei cifrari a flusso: se un avversario modifica alcuni bit del ciphertext, i corrispondenti bit del plaintext vengono cambiati in modo prevedibile, anche senza conoscere la chiave.

#### **Codici di autenticazione dei messaggi (MAC)**

Richiedono una chiave segreta condivisa.  
Alice genera un **tag** (una breve firma) sul messaggio usando la chiave; Bob lo ricrea per verificare l’autenticità.  
Un avversario senza chiave non può creare tag validi.  
Schema comune: **encrypt-then-MAC** (prima cifrare, poi firmare).

#### **Firme digitali**

Usano la **chiave privata** del mittente per firmare e la **chiave pubblica** per verificare.  
Chiunque può controllare la firma, ma solo il titolare può crearla.  
Esempio pratico: **aggiornamenti software firmati**.  
Schema combinato: **sign-then-encrypt** (prima firmare, poi cifrare).

#### **Non ripudio**

Le firme digitali permettono di dimostrare che un messaggio è stato firmato da un individuo, impedendogli di negarlo in seguito (**non-repudiation**).  
I MAC non offrono questa garanzia, perché la chiave è condivisa tra entrambe le parti, e nessuno può provare chi ha creato il tag.  
I MAC sono quindi “**deniable**”, utili in comunicazioni “off the record”.

#### **Certificati**

Servono a verificare l’autenticità delle chiavi pubbliche.  
Sono firmati da **autorità di fiducia (CA)**, il cui certificato è preinstallato nei browser.  
Usati in **TLS** per stabilire connessioni sicure tra client e server.

#### **Funzioni di hash**

Trasformano messaggi di lunghezza arbitraria in un digest di lunghezza fissa.  
Servono a firmare messaggi lunghi (**hash-then-sign**) e per derivare chiavi.  
Devono essere **resistenti alle collisioni** (impossibile trovare due messaggi con lo stesso hash).  
Non possono essere usate per cifrare, perché non sono invertibili né basate su chiavi.

---

### **1.3 – Protocolli crittografici**

I protocolli combinano vari strumenti (cifratura, firme, hash) per creare sistemi più complessi.  
Esempi:

- **Schemi di identificazione:** provano l’identità di un utente (es. password, challenge–response).
    
- **Distribuzione e accordo di chiavi:** permettono a due parti di stabilire una chiave segreta, con o senza l’intervento di un’autorità fidata (es. protocollo **Diffie-Hellman**).
    
- **Secret sharing:** un segreto è diviso in più parti (“share”) e può essere ricostruito solo da un numero minimo di esse, secondo uno schema **(k, n)**.
    

---

### **1.4 – Sicurezza**

Un sistema è “sicuro” se un avversario non può violarlo con le risorse disponibili.  
La sicurezza si analizza considerando tre aspetti:

1. **Modello di attacco:** quali informazioni ha l’avversario (ciphertext, plaintext, messaggi scelti, ecc.).
    
2. **Obiettivo:** cosa vuole ottenere (chiave, contenuto, o solo distinguere due messaggi).
    
3. **Livello di sicurezza:** quante risorse e quanto tempo servono per riuscirci.
    

#### **Modelli di attacco principali**

1. **Ciphertext-only attack:** l’attaccante ha solo testi cifrati.
    
2. **Known-plaintext attack:** conosce alcune coppie plaintext–ciphertext.
    
3. **Chosen-plaintext attack:** può scegliere i messaggi da cifrare.
    
4. **Chosen-ciphertext attack:** può chiedere la decifrazione di testi a sua scelta.  
    I modelli 3 e 4 sono più forti, perché offrono all’avversario più informazioni.
    

#### **Tipi di sicurezza**

- **Computazionale:** il sistema è sicuro perché richiederebbe risorse o tempo eccessivi per essere violato.
    
- **Dimostrabile (provable):** la sua sicurezza è ridotta a un problema matematico difficile (es. fattorizzazione, logaritmo discreto).
    
- **Incondizionata:** l’attacco è impossibile anche con risorse illimitate, come nel **One-Time Pad**.
    

Un esempio storico è il **caso RSA del 1977**: una sfida pubblica proponeva un messaggio cifrato con una chiave di 512 bit, che si credeva indecifrabile per “milioni di anni”. Fu risolta nel 1994 grazie a computer più veloci, nuovi algoritmi e la cooperazione via Internet — dimostrando che la sicurezza computazionale cambia nel tempo.

#### **Attacchi pratici e implementativi**

Anche un sistema matematicamente sicuro può essere vulnerabile se mal implementato.  
Esempi:

- **Padding oracle attack:** sfrutta errori nella gestione del padding nei cifrari a blocchi.
    
- **Side-channel attacks:** analizzano informazioni fisiche (tempi di esecuzione, consumo energetico, cache, errori hardware) per estrarre chiavi o dati segreti.  
    Questi attacchi dimostrano che la sicurezza deve considerare anche l’implementazione fisica, non solo la teoria.
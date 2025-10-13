# 🐷DEFINIZIONE DI INGEGNERIA DEL SOFTWARE
- leggibile a IEEE Std 610.12
- Applicazione di un approccio sistematico, disciplinato...
- ha lo scopo di rispondere a domande di ottimizzazione e manutenzione del software
# 🫚 IL SOFTWARE
- va ingegnerizzato e non solo scritto
- insieme totale di tutti i vari processi e procedimenti nella creazione del prodotto, non solo codice
- la legge di Brooks ci dice che se sono in ritardo nella consegna, se aggiungo nuovi programmatori rallento ancora di piú


# 🧮 DRE (Defect Removal Efficiency)

- Fornisce una **misura quantitativa** di quanto un processo di sviluppo riesce a **identificare e correggere i difetti**.

---

# ⚙️ Caratteristiche essenziali di Brooks

- **Complesso**
    - Numero di stati possibili del software decisamente elevato.
- **Conformità**
    - Il software deve conformarsi al contesto di quel dato ambiente operativo.
- **Cambiabilità**
    - Il software viene costantemente modificato e aggiornato.
- **Invisibilità**
    - Non abbiamo sempre la visuale su ciò che avviene nella parte _back_ del software.

---

# 💰 Costo del prodotto software

- Diversi aspetti:
    - **Dimensione**
        - Il costo in _soldini_ è proporzionale al quadrato della dimensione:  
            $C = aS²$
    - **Repliche**
        - Grazie alle piattaforme online, il costo di distribuzione è quasi nullo.
    - **Ampiezza di mercato**
        - Quante persone sono disposte ad acquistare o utilizzare un determinato prodotto.

---

# 📘 Carrellata di definizioni

- **Prodotto software**
    - Codice + Documentazione.
- **Artefatto**
    - Prodotto software intermedio con vari documenti:
        - Documento dei requisiti
        - Documento di specifica
        - Documento di progetto
- **Codice**
    - Prodotto software finale.
- **Sistema software**
    - Insieme organizzato di prodotti software (es. Office, Adobe, ecc...).
    - Oppure può significare _hardware + software_ con un hardware custom.
- **Cliente**
    - Colui che commissiona il prodotto software.
- **Sviluppatore**
    - Soggetto che lo produce.
- **Utente**
    - Soggetto che lo usa.
- **Software interno**
    - Cliente e sviluppatore coincidono.
- **Software a contratto**
    - Cliente e sviluppatore sono soggetti differenti.
- **Embedded**
    - Software integrato in dispositivi hardware specifici.

---

# 🧩 Affidabilità del software

- **Informalmente**
    - Credibilità del prodotto.
- **Formalmente**
    - Probabilità che il software lavori correttamente in un determinato intervallo temporale (detto _mission time_).

---

# 🪲 Difetti, guasti ed errori

- **Difetto o bug**
    - Anomalia nel prodotto software.
    - Tanti difetti = poca affidabilità.
- **Guasto**
    - Comportamento anomalo del prodotto software dovuto a uno o più difetti.
- **Errore**
    - Azione errata di chi, per ignoranza o distrazione, introduce un difetto nel prodotto software.

---

# 🔁 Regression false

- Trovo un difetto, lo risolvo... e ne spuntano altri due.
- Se elimino un difetto **non per forza** migliora l’affidabilità.

---

# ⏱️ Regola 10–90

- Il **90%** del tempo di esecuzione totale è speso eseguendo solo il **10%** delle istruzioni.
- Questo 10% è detto **nucleo**, e rappresenta gran parte dell’affidabilità.

---

# 📊 Operational profile

- Percentuale quantitativa che indica con quale probabilità si usano le varie parti del prodotto.
    - La classe 1 usa una certa % del prodotto.
    - La classe 2 un’altra %, e così via.
- L’affidabilità dipende dagli **utenti** e da come utilizzano il software.

---

# ⚖️ Guasti hardware e software

- **Software**
    - Difetti nei programmi.
    - Non si consumano.
    - Si correggono con attenzione, perché si può incorrere in ulteriori problemi.
    - REGRESSION FAULT
- **Hardware**
    - Prodotti che si deteriorano o si rompono.
    - Per ripararli bisogna sostituire la componente.
    - È definito un **MTTF (Mean Time To Failure)** → indica dopo quanto tempo una certa componente potrebbe fallire.
# ⚙️ Frequenza difetti hardware

- “Vasca da bagno” letteralmente.
    
- **Failure rate alto nei primi tempi** → mortalità infantile.
    
- Poi si **stabilizza nel tempo**.
    
- Aumenta di nuovo nei **tempi di usura** con il prolungarsi del tempo.
    

---

# 💾 Frequenza difetti software

- **Curva idealizzata:** decrescente.
    
- **Curva reale:** differente, con una leggera ricrescita dovuta a particolari aggiornamenti.
    
- Secondo alcuni studiosi di **software rejuvenation**, nei software grandi nel tempo possono esserci “danni di usura”.
    
    - Per risolvere, dicono che basta fare **manutenzione periodica** (es. una volta all’anno).
        
    - Secondo il prof, è “abbastanza una cazzata”: basta **spegnere e riaccendere**.
        

---

## 🖥️Software availability

- È la **percentuale di tempo** in cui il software è utilizzabile.
    
- Dipende da:
    
    - Numero di guasti.
        
    - Tempo necessario a ripararli.
        
- Le interruzioni comportano **perdite**:
    
    - Economiche.
        
    - Sociali.
        
    - Di produttività.
        

---

# 🧪 Tecniche di testing

- **Testing statistico**
    
    - Dispendioso in **tempi e risorse**.
        
    - Si prende un **lasso di tempo prefissato**.
        
    - Ad ogni fallimento si registra **l’istante di fallimento**.
        
        - Il prodotto viene **corretto** e si **ricomincia** il testing per lo stesso intervallo.
            
- **Modello più usato:** _modello del frakkone_.

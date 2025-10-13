# 🐷 DEFINIZIONE DI INGEGNERIA DEL SOFTWARE

- 📖 **IEEE Std. 610.12 (1990):**
    
    1. Applicazione di un approccio **sistematico, disciplinato e misurabile** allo sviluppo, esercizio e manutenzione del software, cioè l’applicazione di **principi ingegneristici al software**.
        
    2. **Studio** degli approcci di cui al punto 1.
        
- 🏗️ Ha lo scopo di rispondere a domande di **ottimizzazione**, **qualità** e **manutenzione** del software.
    
- 📜 **Origine del termine**
    
    - Coniato nel **1968** durante una conferenza **NATO a Garmisch (Germania)** per sottolineare la necessità di inquadrare la produzione del software come una **disciplina ingegneristica**.
        

---

# 🧠 MATRIMONIO NON CONSUMATO

- (Cit. D.L. Parnas, CACM, 1997)
    
    - La _Software Engineering_ è un “**matrimonio non consumato**” tra:
        
        - la **teoria della programmazione**, e
            
        - i **principi dell’ingegneria** (progettazione e validazione).
            
- Storicamente:
    
    - Per anni si è pensato che bastasse **saper programmare** per essere ingegneri del software.
        
    - La _software engineering_ è stata vista come una **branca dell’informatica teorica**, non come una disciplina progettuale autonoma.
        
    - Oggi serve un equilibrio tra:
        
        - conoscenze teoriche di informatica, e
            
        - capacità di **progettazione, controllo, manutenzione e qualità**.
            

---

# 🫚 IL SOFTWARE

- Va **ingegnerizzato** e non solo scritto.
    
- È l’insieme di **tutti i processi e procedimenti** che portano alla creazione del prodotto, non solo codice.
    
- Il software:
    
    - non si **consuma**,
        
    - è **complesso**, **invisibile**, **cambiabile** e deve **conformarsi** al suo ambiente.
        
- ⚖️ **Legge di Brooks:**
    
    - Se si è in ritardo e si aggiungono nuovi programmatori, si **rallenta ancora di più**.
        

---

# 🔄 CICLO DI VITA DEL SOFTWARE

- **3 stadi principali:**
    
    1. **Sviluppo** (6 fasi):
        
        - Requisiti
            
        - Specifiche (analisi dei requisiti)
            
        - Pianificazione
            
        - Progetto (preliminare e dettagliato)
            
        - Codifica
            
        - Integrazione
            
    2. **Manutenzione**
        
        - Copre circa il **60% dei costi** dell’intero ciclo di vita.
            
    3. **Dismissione**
        
- 📉 **Effetto delle modifiche:**
    
    - Le modifiche fatte in fasi avanzate costano di più e richiedono risorse aggiuntive.
        

---

# 🧪 TESTING

- Non è una **fase separata**, ma un’attività **trasversale** a tutto lo sviluppo.
    
- Si articola in:
    
    - **Verifica:**  
        “Are we building the product right?” → la fase è stata ben svolta?
        
    - **Validazione:**  
        “Are we building the right product?” → il prodotto finale è quello giusto?
        

---

# 🧮 DRE (Defect Removal Efficiency)

- Fornisce una **misura quantitativa** di quanto un processo di sviluppo riesce a **identificare e correggere i difetti** prima del rilascio.
    
- Esempio:
    
    > Se il team trova 900 difetti prima del rilascio e gli utenti ne trovano 100 dopo, il DRE è **90%**.
    
- 📊 Valore medio (USA, 2016): **≈92%**  
    _(può variare in base al modello di ciclo di vita)._
    

---

# ⚙️ ASPETTI TIPICI DELL’INGEGNERIA DEL SOFTWARE

## 🧩 Aspetti accidentali (superabili)

- Di **attitudine**
    
- Di **manutenzione**
    
- Di **specifica e progetto**
    
- Di **teaming** (collaborazione tra persone)
    

## ⚙️ Aspetti essenziali (non superabili)

- **Complesso:** numero di stati possibili elevatissimo.
    
- **Conformità:** deve adattarsi all’ambiente operativo.
    
- **Cambiabilità:** costantemente aggiornato e modificato.
    
- **Invisibilità:** non sempre visibile nelle sue parti interne.
    

---

# 💰 COSTO DEL PRODOTTO SOFTWARE

- **Dimensione**
    
    - Il costo cresce con il **quadrato** della dimensione:  
        $C = aS²$
        
    - Fare due prodotti di dimensione S/2 costa meno che farne uno solo di dimensione S.
        
- **Repliche**
    
    - Il costo di produzione di una replica è praticamente nullo.
        
- **Ampiezza di mercato**
    
    - Per vendere un prodotto di dimensione doppia:
        
        - serve un **prezzo 4× maggiore**, oppure
            
        - un **mercato 4× più ampio**.
            

---

# 📘 CARRELLATA DI DEFINIZIONI

- **Prodotto software:** codice + documentazione.
    
- **Artefatto:** prodotto intermedio (documenti di requisiti, specifica, progetto).
    
- **Codice:** prodotto finale.
    
- **Sistema software:** insieme organizzato di prodotti software (es. Office).
    
- **Cliente:** chi commissiona il prodotto.
    
- **Sviluppatore:** chi lo realizza.
    
- **Utente:** chi lo utilizza.
    
- **Software interno:** cliente e sviluppatore coincidono.
    
- **Software a contratto:** cliente e sviluppatore diversi.
    
- **Software embedded:** integrato in dispositivi hardware specifici.
    

---

# 🧩 AFFIDABILITÀ DEL SOFTWARE

- **Informalmente:** credibilità del prodotto.
    
- **Formalmente:** probabilità che il software lavori correttamente in un dato intervallo di tempo (_mission time_).
    

---

# 🪲 DIFETTI, GUASTI ED ERRORI

- **Difetto (defect):** anomalia presente nel software.
    
- **Guasto (failure):** comportamento anomalo causato da un difetto.
    
- **Errore:** azione errata di chi introduce il difetto (ignoranza o distrazione).
    

---

# 🔁 REGRESSION FAULTS

- Risolvo un difetto e ne emergono altri due.
    
- Eliminare un difetto **non garantisce** un aumento dell’affidabilità.
    

---

# ⏱️ REGOLA 10–90

- Il **90% del tempo di esecuzione** è speso nel **10% del codice** → il **nucleo** del programma.
    
- L’affidabilità dipende molto dai difetti presenti nel **nucleo**.
    

---

# 📊 OPERATIONAL PROFILE

- Indica con quale probabilità vengono usate le varie parti del prodotto.
    
- L’affidabilità **dipende dall’uso reale**:
    
    - utenti diversi → profili operativi diversi → difetti diversi.
        
- In sintesi: l’affidabilità dipende **dagli utenti**.
    

---

# ⚖️ GUASTI HARDWARE E SOFTWARE

## 💽 Hardware

- Si **consuma o si rompe**.
    
- Riparazione = **sostituzione della componente**.
    
- Obiettivo: **stabilità** della frequenza di guasto (MTTF).
    

## 💾 Software

- Non si consuma.
    
- Guasti dovuti a **difetti nel codice**.
    
- Dopo una “riparazione”:
    
    - L’affidabilità può **aumentare o diminuire**.
        
- Obiettivo: **crescita di affidabilità**, cioè riduzione della frequenza di guasto nel tempo.
    

---

# ⚙️ FREQUENZA DIFETTI HARDWARE

![[Pasted image 20251013183827.png]]


- “Curva a vasca da bagno” 🛁
    
    - Alta all’inizio → **mortalità infantile**
        
    - Poi si **stabilizza**
        
    - Cresce di nuovo → **usura**
        

---

# 💾 FREQUENZA DIFETTI SOFTWARE

![[Pasted image 20251013183852.png]]

- **Curva idealizzata:** decrescente.
    
- **Curva reale:** decresce ma poi **ricresce leggermente** per effetto di aggiornamenti e manutenzione.
    
- Alcuni parlano di **software rejuvenation** → manutenzione periodica.
    
    - Secondo il prof: “abbastanza una cavolata”, basta **spegnere e riaccendere**.
        

---

# 🖥️ SOFTWARE AVAILABILITY

- Percentuale di tempo in cui il software è **utilizzabile**.
    
- Dipende da:
    
    - Numero di guasti.
        
    - Tempo per ripararli.
        
- Le interruzioni comportano **perdite economiche, sociali e di produttività.**
    

---

# 🧪 TECNICHE DI TESTING (RIEPILOGO)

- **Testing statistico:**
    
    - Dispendioso in tempo e risorse.
        
    - Si fissa un intervallo temporale e si registra ogni fallimento.
        
    - Dopo ogni correzione, il test si ripete per lo stesso intervallo.
        

---

# 🚫 MITI DEL SOFTWARE (DA SFATARE)

- Se si è in ritardo, basta aggiungere più programmatori.
    
- Una descrizione generica è sufficiente per scrivere i programmi.
    
- Una volta messo in opera, il lavoro è finito.
    
- La qualità si valuta solo alla fine.
    
- L’ingegneria del software **rallenta e costa troppo** (falso).
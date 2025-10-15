
## DEFINIZIONE DI AGENTE

- Un **agente** è una **IA incarnata** in un ambiente, capace di **percepire, ragionare e agire autonomamente** in modo **razionale** per raggiungere i suoi obiettivi.
- **IA** è il campo di studio (la disciplina)  
- **Agente** è l’unità operativa che incarna una IA in un ambiente.

- *Agente=Software*
# 🤖 DIFFERENZA TRA UN SOFTWARE TRADIZIONALE E UN SOFTWARE AI

Un **software tradizionale** lavora in isolamento: riceve input predefiniti e produce output prevedibili.  
Un **software di tipo AI**, invece, **lavora in un ambiente**, percepisce segnali esterni, **decide autonomamente** e **agisce** in base alle condizioni che rileva.  
È un sistema dinamico, più simile a un **sistema operativo intelligente** che non a un semplice programma.

- L’**agente AI** non può sapere in anticipo le domande o gli stimoli che riceverà.
    
- Può disporre di:
    
    - **Effettori** → componenti che gli permettono di compiere azioni fisiche o logiche.
        
    - **Sensori** → apparati che gli consentono di percepire e riconoscere l’ambiente.
### 🔁 Ciclo dell’agente

![[Pasted image 20251013185628.png]]

1. **Percepire** una situazione tramite i sensori.
    
2. **Decidere** cosa fare in base alle proprie conoscenze e percezioni passate.
    
3. **Agire** sull’ambiente con gli effettori.
    
4. **Aggiornarsi** in base alle conseguenze dell’azione.
    

Gli agenti hanno **obiettivi** e una **percezione parziale del mondo**:  
l’ambiente interno che rappresentano **non è una copia perfetta del mondo reale**, ma una **versione astratta e dinamica**, arricchita solo quando nuove informazioni diventano necessarie.

---

# 🧩 PERCEZIONI E AZIONI

- **Percezione:** l’input proveniente dai sensori.
    
- **Sequenza percettiva:** la storia completa di tutte le percezioni avute fino a un certo momento.
    
- L’**azione** è sempre conseguente a una percezione: ogni nuova percezione genera una nuova decisione e quindi una nuova azione.

---
# 🧠 AGENTI RAZIONALI

Un **agente razionale** è un’entità che interagisce con l’ambiente in modo efficace, compiendo **le azioni giuste** per ottenere una **sequenza di stati desiderabile**.

> 💡 **Un agente intelligente = un agente razionale**  
> In Intelligenza Artificiale, un agente è intelligente quando agisce in modo razionale rispetto ai propri obiettivi e alle informazioni di cui dispone.

L’obiettivo non è “pensare come un umano”, ma **compiere scelte ottimali** rispetto alle percezioni e alle conoscenze attuali.

---

## 🔹 Definizione di razionalità

La razionalità di un agente dipende da:

- la **misura di prestazione** (quanto le sue azioni portano al successo),
    
- le **conoscenze pregresse** dell’ambiente,
    
- le **percezioni presenti e passate**,
    
- le **capacità operative** dell’agente.
    

Per ogni sequenza percettiva, un agente razionale sceglie **l’azione che massimizza il valore atteso della misura di prestazione**, considerando ciò che sa e ciò che ha percepito in passato.

---

## ⚖️ Criterio di valutazione oggettivo

Per stabilire se un agente è razionale, serve una **misura di prestazione esterna**, definita dal progettista, che descriva come vogliamo che il mondo evolva dopo le sue azioni.  
La razionalità quindi non è assoluta, ma **relativa al contesto e al problema**.

---

## 🔸 Razionalità ≠ Onniscienza

L’agente razionale **non è perfetto**: non conosce tutto e non prevede tutto.  
Conta solo che agisca **nel modo migliore possibile** con le informazioni che ha.  
Se non sa, può **esplorare** o **acquisire nuove informazioni** per migliorarsi.

---

## 🔹 Razionalità e apprendimento

Raramente un agente dispone di tutte le conoscenze in anticipo.  
Per questo deve **imparare dall’esperienza**, modificando il proprio comportamento in base a **percezioni passate**, **feedback** e **errori**.  
Più apprende, più diventa razionale e quindi intelligente.

---

# 🧍‍♂️ AGENTI AUTONOMI

Un agente è **autonomo** nella misura in cui il suo comportamento dipende **dalla propria esperienza**.  
Un agente che agisce solo secondo regole predefinite (**built-in**) è rigido e poco flessibile.  
Deve invece **adattarsi** e migliorare nel tempo, pur rimanendo **controllabile e collaborativo**.

---

# 🌍 AMBIENTE E CODIFICA PEAS

Un ambiente è descritto dal modello **PEAS**, che identifica gli elementi chiave del problema dell’agente:

|Lettera|Significato|Descrizione|
|---|---|---|
|**P**|Performance|Misura di successo dell’agente (obiettivi)|
|**E**|Environment|Descrizione dell’ambiente operativo|
|**A**|Actuators|Attuatori: componenti per agire|
|**S**|Sensors|Sensori: componenti per percepire|

---

## 🚖 Esempio — Agente "Guidatore di Taxi"

| **Prestazioni** | Arrivare a destinazione in sicurezza, rispettando le regole, minimizzando tempi e consumi, garantendo comfort. |  
| **Ambiente** | Strada, traffico, pedoni, clienti, segnali stradali. |  
| **Attuatori** | Sterzo, acceleratore, freni, clacson, schermo, voce sintetica. |  
| **Sensori** | Telecamere, GPS, sonar, tachimetro, microfono, sensori di motore. |

---

# ⚖️ PROPRIETÀ DELL’AMBIENTE

Un ambiente può avere diverse caratteristiche:

|Proprietà|Descrizione|
|---|---|
|**Completamente / Parzialmente osservabile**|L’agente percepisce tutto ciò che serve oppure solo una parte (limitazioni sensoriali).|
|**Agente singolo / multi-agente**|In un ambiente multi-agente gli altri agenti possono essere cooperativi o competitivi.|
|**Deterministico / Stocastico / Non deterministico**|Deterministico → stato futuro certo.  <br>Stocastico → esiste una probabilità di transizione.  <br>Non deterministico → esiti possibili equiprobabili o non noti.|
|**Episodico / Sequenziale**|Episodico → le decisioni sono indipendenti (es. riconoscimento immagini).  <br>Sequenziale → ogni decisione influenza le successive (es. guida autonoma).|
|**Statico / Dinamico / Semi-dinamico**|Statico → l’ambiente non cambia mentre l’agente decide, probabilmente perché effettua le scelte in maniera molto rapida.  <br>Dinamico → l’ambiente cambia mentre l’agente agisce (es. taxi autonomo).  <br>Semi-dinamico → ambiente stabile ma la valutazione cambia (es. scacchi con timer).|
|**Discreto / Continuo**|Discreto → numero finito di stati o azioni (esame a scelta multipla).  <br>Continuo → stati e tempi variano nel continuo (es. guida).|
|**Noto / Ignoto**|Noto → l’agente conosce l’ambiente.  <br>Ignoto → deve esplorare e apprendere.|

> Gli ambienti reali sono di solito: **parzialmente osservabili, stocastici, sequenziali, dinamici, continui, multi-agente e ignoti.**
---

**CHIEDI A LEZIONE SI INTENDE SIMULARE PER VELOCIZZARE O ASTRARRE IL VERO E PROPRIO AMBIENTE IN MODO CHE SIA COMPATIBILE CON QUEL DETERMINATO AGENTE?**
# 🧮 COME AUTOMATIZZARE UN AMBIENTE

Un **simulatore di ambienti** è un software che:

- genera stimoli per gli agenti,
    
- raccoglie le azioni in risposta,
    
- aggiorna lo stato dell’ambiente,
    
- può attivare processi secondari,
    
- valuta la prestazione degli agenti.

Serve per **testare e addestrare** gli agenti in modo controllato.

### 🔸 Ambiente reale vs simulato

- L’**ambiente reale** è il mondo fisico o operativo in cui l’agente percepisce e agisce concretamente (es. un’auto autonoma).
    
- L’**ambiente simulato** è costruito ad hoc per l’addestramento: consente di provare azioni e imparare senza rischi.  
    → In genere si addestra in un **ambiente virtuale**, poi si trasferisce il comportamento nel **mondo reale**.
    

---

# 🧠 STRUTTURA DELL’AGENTE

> **Agente = Architettura + Programma**

- **Architettura:** la parte fisica o software che esegue le operazioni (hardware, sensori, processi).
    
- **Programma agente:** l’algoritmo che decide quale azione intraprendere in base alle percezioni.
    

👉 L’architettura è il **corpo**, il programma è la **mente** dell’agente.

Un **agente** può essere visto come una **funzione matematica** che:
$$Ag : P^* \rightarrow A$$
dove:
- $P^*$ = insieme di tutte le possibili sequenze di percezioni,
    
- $A$= insieme delle azioni possibili.

> In parole semplici:  
> **un agente è una funzione che prende in input le percezioni e restituisce in output un’azione.**
> 
> Quindi, una **funzione agente** riceve una percezione (o una sequenza percettiva), decide, e **manda in output un’azione** in risposta.

---

## 📘 Funzionamento generale
```scss
memoria ← aggiorna(memoria, percezione) 
azione ← scegli_azione_migliore(memoria) 
memoria ← aggiorna(memoria, azione) 
restituisci(azione)
```

Ogni agente, indipendentemente dalla sua architettura, può **migliorare nel tempo attraverso l’apprendimento**, diventando progressivamente più razionale e adattivo.

## DIVERSI TIPI DI AGENTE
- studiare le funzioni degli agenti!
- AGENTE BASATO SU TABELLA
	- AGENTE REATTIVO SEMPLICE, DI CUI UN ESEMPIO AGENTE BASATO SU TABELLA?
	- IL PUZZO DEL WUMPUS
- AGENTI BASATI SU MODELLO 
	- molto piu complessi, non scrivi solo una tabella con match della regola e match condizionale
	- devo avere la memorizzazione del modello(ovvero, prendere i dettagli essenziali di un certo oggetto e codificarli in dati comprensibili)
	- lo scopo viene definito dall'azione, devi fare l'azione e basta
- AGENTE CON OBIETTIVO
	- un agente ancora piú complesso ragiona ponendosi degli obiettivi
	- un goal non e per forza la soluzione migliore possibile ma cio che ci direziona verso una soluzione valida e accettabile
- utility e il goal?
	- utility e una autovalutazione dell'agente
ENUMERATI E NON VALUTATI
- AGENTI CON VALUTAZIONE DI UTILITÀ
	- valutazione da parte dell'ambiente
- AGENTI CHE APPRENDONO
	- dentro performance element abbiamo state world and utility
	- il performance element quando lavora non si addestra subito, bensi una volta accumulati gli addestramenti viene interrotto il performance element e viene sostituito da una nuova versione addestrata dai feedback ricevuti
		- ambiente simulato a volte usato nel batch learning
### IMPLICAZIONI COMPUTAZIONALI
- rappresentazioni
- funzioni principale degli agenti
- sborra
## TIPI DI RAPPRESENTAZIONE
- ATOMICA
- FATTORIZZATAf
- STRUTTURATA
## Pattern linguistici via machine learning con encoder e decoders per NL
- meccanismo di encoding che ci porta ad avere per ogni d appartenente a D d freccia sopra appartenente a R con 256 che fa encoding e cardinalita di D circa 250k
- con una certa probabilita abbiamo il decoding in teoria
- si chiamano LANGUAGE MODEL perche forniscono un modello stocastico che predice la transizione successiva ovvero la parola che va detta dopo
### DESIDERATA DI UN AGENTE

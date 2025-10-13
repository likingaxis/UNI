# LO SCHEDULING
In un computer possono esserci $n$ processi o thread che competono per utilizzare la CPU
>[!question]- cosa fa lo scheduler?
>lo scheduler ha il compito di decidere quale processo o thread deve essere eseguito successivamente seguento un determinato algoritmo
>- Ci sono due tipi di scheduler uno che lavora al livello utente uno kernel, lavorano in modo indipendente e quello kernel lavora per thread

##### UN PÒ DI STORIA
1. I primi sistemi batch hanno uno scheduling lineare dove le istruzioni venivano eseguite in successione
2. con la multiprogrammazione lo scheduling divenne sempre più complesso e si dovette ricorrere ad usare algoritmi per migliorare le prestazioni 
3. Nei personal computer di solito la CPU non viene usata al 100% perché è sempre in attesa dell'input dell'utente.
### COSTI DEI PROCESSI
la cosa che costa tanto quando si ha un sistema con una CPU è il **il cambio di contesto** e quando avviene succede questo:
- Cambio la modalità da utente a kernel
- Salvo lo stato del processo interrotto così da riprenderlo
- Eseguo l'algoritmo di scheduling
- Cambio area di memoria su cui lavora il processo
- Invalidazione potenziale della memoria cache(poi lo vediamo alle prossime lezioni)
Il **cambio di contesto** non deve essere per forza efficiente solo nell'ambito di velocità ma anche di efficienza dei consumi tipo nei telefoni(IoT)(internet of things, quei dispositivi che funzionano attraverso la condivisione dei dati)
#### I nostri processi sono caratterizzati da
- processi **CPU bound** stressano il processore al 100% tenendolo sempre occupato a fare qualcosa con un cpu-burst sempre all'attivo, in questi processi non hai bisogno di attendere input output quindi la CPU lavora a massimo regime
- **i/o bound** sono quei processi che ricevono input dall'esterno e quindi che devono fare attese frequenti avendo degli short burst

>[!question]- cosa è il cpu burst
>(il cpu burst è una unità di tempo che definisce quando la CPU è in uso)

![[Pasted image 20241115154712.png|600]]

###### PRECISAZIONI SULLO SCHEDULING
- con CPU più veloci i processi tendono a essere più I/O bound 
	- perché spesso sono i processori ad attendere qualcun altro
- Gli SSD possono un po' risolvere la cosa del I/O bound ma comunque i data center per un discorso di costo x bit sono ancora sugli HDD e usano algoritmi di scheduling per questo
- Non tutti gli scheduling funzionano su tutti i dispositivi

##### GLI STATI DI UN PROCESSO
![[Pasted image 20241115155817.png|500]]
un processo ha principalmente 3 stati:
- Esecuzione: sta eseguendo il codice e usa la CPU
- Ready: è pronto per eseguire il codice ma non lo fa
- Blocked: è in attesa di qualche risorsa o comunque non è pronto
lo scheduler attraverso un algoritmo di scheduling capisce quale processo mettere in running
##### LO SCHEDULER SERVE SEMPRE
>[!question] Quando interviene lo scheduler?
> - Creazione di un processo
> 	- Decide chi eseguire se il genitore o il figlio
> - Uscita di un processo
> 	- Se un processo esce allora deve decidere chi far partire
> - Blocco del processo
> 	- Se un processo si blocca se ne deve selezionare un altro
> - Interrupt di I/O
> 	- Alla fine di un interrupt il processo potrebbe andare su ready e essere eseguito

#### Esistono due tipologie di scheduling
##### Non preemptive(senza prelazione)
- se eseguo un processo devo aspettare che finisca da solo oppure che va in blocked in attesa di un i/o

##### Preemptive(con prelazione)
- Definisce un tempo e lascia eseguire quel processo in quel determinato quanto di tempo
- viene effettuato un interrupt del clock per far tornare il controllo allo scheduler una volta scaduto il tempo

>[!tip]- parentesi sulla prelazione
>il croce dice:
>>[!quote]- se  uno scheduler ha la prelazione ho una interruzione forzata, il processore dice al processo levati dal cazzo
>
>cose importanti da dire sulla prelazione:
>- è davvero importante per mantenere il controllo e evitare processi lenti che intasano il sistema

### 3 diversi ambienti di scheduling
- Batch
	- di solito SENZA PRELAZIONE 
	- viene usato spesso in contesti aziendali
	- massimizza il troughput, il numero di job completati in un dato tempo
	- minimizzo il turnaround, il tempo che scorre dallo start all'end di un job
	- mantiene la CPU sempre attiva
- Interattivo
	- Prevedono la PRELAZIONE
	- la CPU non viene monopolizzata
	- Adatto per utenti multipli e server
	- il tempo di risposta deve essere rapido
	- la risposta deve essere adeguata in un tempo rapido, non `luc` ma `luca`
- Sistemi Real-time
	- Non devono avere pefforza la PRELAZIONE
	- Se un processo impiega troppo tempo si interrompe
	- Eseguono programmi per specifiche applicazioni
	- rispetto delle scadenze
	- il funzionamento deve essere costante e non ci devono essere errori, tipo su applicativi che servono per la vita di persone
#### Obiettivi degli algoritmi di scheduling 
tutti i sistemi devono garantire:
- Equità: una equa condivisione della CPU tra tutti i processi
- Imposizione della policy: applicare le definizioni della policy dette prima
- Bilanciamento: mantenere tutti i componenti del sistema attivi


## SCHEDULING NEI SISTEMI BATCH
#### 1. FIRST COME FIRST SERVED (FCFS)
**Chi prima arriva meglio alloggia**
- non ha prelazione
- i processi vengono assegnati alla CPU in base a come arrivano
- si mettono tutti in una singola coda
- i processi bloccati vanno in fondo alla coda
è facile da programmare ed è anche abbastanza equo
non è troppo ottimale in scenari misti(sia CPU bound che I/O bound)
si può incorrere in attese lunghe
#### 2. SHORTEST JOB FIRST (SFJ)
**Il più corto alloggia prima**
- algoritmo senza prelazione
- i tempi di esecuzione si devono sapere prima

![[Pasted image 20241115165039.png]]

è ottimale per ridurre il tempo di turnaround quando tutti i job sono disponibili
se alcuni arrivano dopo non è ottimale perché
- il SFJ si ricorda solo il tempo di esecuzione di un processo solo iniziale
- quindi se un processo va in stato di blocco e gli mancano $0,1$ secondi per essere eseguito, verrà comunque trattato come se durasse tipo $10$ ore, soluzione quello che vediamo dopo

>[!question]- turnaround cosa significa?
>si riferisce al periodo totale impiegato per completare un'attività
#### 3. SHORTEST REMAINING TIME NEXT (SRTN)
**quello che ha il tempo rimanente più corto alloggia**
- versione con prelazione di SJF
- seleziona il processo con il tempo rimanente più breve
- tempo noto
- confronta i job e vede il tempo rimanente più basso
- se entra qualche nuovo processo che dura meno verrà soddisfatto rapidamente
- trasforma gli ambienti batch in circa preemptive
## SCHEDULING IN SISTEMI INTERATTIVI
il tempo di risposta é fondamentale e abbiamo diversi algoritmi:
![[Pasted image 20241115171221.png|300]]
#### 1. ROUND ROBIN (RR)
- è il più vecchio ma 
	- semplice
	- equo
	- molto utilizzato
- ogni processo riceve un quanto se non lo rispetta va a casetta ed è soggetto a prelazione
è prevista una lista di processi eseguibili(Ready)
quando un processo termina un quanto si sposta alla fine della lista

![[Pasted image 20241115171351.png]]
##### Cose importanti del Round Robin
- è importante scegliere un quanto perché se avviene troppo spesso avrò troppi cambi di contesto e un overhead eccessivo, ovvero uno spreco della cpu sgravatus
- abbiamo un Trade-off sul quanto da definire e la reattività del sistema
- è consigliato un quanto tra $20$ e $50$ $ms$
#### 2. SCHEDULING A PRIORITÀ (SAP)
- il round robin vede tutti i processi uguali ma magari ce ne sono alcuni che hanno maggiore priorità
- ogni processo ha una sua priorità e viene eseguito il processo con priorità più alta
![[Pasted image 20241115171835.png]]

>[!question]- gestione delle priorità
>se una priorità viene subentrata da un altro processo 
>- il processo con la priorità maggiore lo supera 
>	- facendo avvenire un cambio
>- la priorità può essere
>	- **statica**: la priorità non cambia nel tempo, usato tipo dai militari
>	- **dinamica**: la priorità cambia nel tempo, tipo in sistemi I/O bound

>[!question]- se ho$3$ processi con priorità $4$ come li gestisco?
>raggruppo i processi in gruppi in base alle priorità
>poi sul singolo gruppo posso usare tipo il round-robin
>![[Pasted image 20241115173014.png|350]]


#### 3. SHORTEST PROCESS NEXT CON AGING(SPNCA)
noi vogliamo applicare shortest job first ai sistemi interattivi dove 
- non sappiamo a priori quanto ha da lavorare un job
**soluzione**
- creiamo delle stime dando un peso $a$ ogni volta che un processo viene eseguito
- così facendo abbiamo una stima e non abbiamo bisogno di sapere prima i vari quanti
![[Pasted image 20241115174050.png|500]]

#### 4. GUARANTEED SCHEDULING(GS)
cerca di creare una cosa più equa possibile garantendo a tutti del tempo sulla CPU
facendo un rapporto tra 
- tempo da quando ho creato processo $x$
- numero di processi
se un processo l'ho creato da 100 secondi e ho 10 processi farò $100/10$ così quel processo ha $10$ secondi
Esegue prima quello con il rapporto più basso

#### 5. SCHEDULING A LOTTERIA(SAL)
![[1RUO.gif|400]]
- creo dei biglietti della lotteria e li do randomicamente ad ogni processo
- chi vince si esegue e faccio $n$ estrazioni al secondo
se voglio creare una sorta di priorità posso dare più biglietti a chi ha una priorità maggiore
se ho processi figli posso fare in modo che il processo padre dia un po' dei suoi biglietti ai figli

#### 6. SCHEDULING FAIR-SHARE(SFS)
L'idea è dare una frazione predefinita di CPU ad ogni utente e si assicura che ogni utente riceva la sua frazione indipendentemente dal numero di processi posseduti. LETTERALMENTE DEFINIZIONE DI "**EQUITÀ**"
![[Pasted image 20241115180401.png|400]]

## SCHEDULING IN SISTEMI REAL-TIME
vengono utilizzati in sistemi operativi che necessitano un tempo di risposta immediata
![[Pasted image 20241120165915.png]]
###### ESISTONO DUE TIPI DI SISTEMI REAL-TIME
- Hard Real-Time: le scadenze devono obbligatoriamente essere rispettate
- **Soft Real-Time**: le scadenze devono essere rispettate ma in modo più tollerabile
###### TIPI DI EVENTI
- **Periodici** : avvengono ad intervalli regolari
- **non Periodici** : avvengono ad intervalli irregolari

###### CONDIZIONE DI SCHEDULABILITÀ:
La CPU deve essere in grado di gestire la somma totale del tempo richiesto dai processi.
	Per esempio, se ci sono
		- `m` eventi periodici
		- ogni evento `i` avviene con un periodo di $P_i$
		- ogni evento richiede $C_i$ secondi di tempo della CPU per essere gestito
		Il carico totale può essere gestito SOLO SE $$\sum_{i=1}^{m} \frac{C_i}{P_i} \leq 1$$
>[!tip] da ricordare: Ci è quanto tempo impiega l'evento e Pi è la periodicità

###### ESEMPIO
- EVENTI PERIODICI: 100ms, 200ms, 500ms
- TEMPI RICHIESTI: 50ms, 30ms, 100ms
Abbiamo quindi

| <center>Processi</center> | <center>Periodo ($P_i$)</center> | <center>Tempi richiesti ($C_i$)</center> | <center>Condizione</center>                                    |
| ------------------------- | -------------------------------- | ---------------------------------------- | -------------------------------------------------------------- |
| <center>P1</center>       | <center>100ms</center>           | <center>50ms</center>                    | <center>$\frac {C_i} {P_i} = \frac {50} {100} = 0,5$</center>  |
| <center>P2</center>       | <center>200ms</center>           | <center>30ms</center>                    | <center>$\frac {C_i} {P_i} = \frac {30} {200} = 0,15$</center> |
| <center>P3</center>       | <center>500ms</center>           | <center>100ms</center>                   | <center>$\frac {C_i} {P_i} = \frac {100} {500} = 0,2$</center> |
E QUINDI $$\sum_{i=1}^{m} \frac{C_i}{P_{i}} \space \space= \space \space 0,5 + 0,15 + 0,2 \space \space \le \space \space 1$$
###### Gli algoritmi di scheduling possono essere
- **Statici**, in cui i requisiti di calcolo e periodicità sono ben definiti in anticipo (l'esempio appena visto era statico)
	È limitato perché bisogna conoscere le esigenze e le scadenze a priori
- **Dinamici**, in cui i requisiti cambiano durante l'esecuzione
# Processi e Scheduling
i processi non sono indipendenti bensì possono esserci situazioni complesse dove un processo può avere uno o più figli sotto il suo controllo.
(ad esempio un sistema di gestione di un database)
>[!bug]- i tradizionali scheduler trattano i processi come se fossero isolati e indipendenti tra loro, questo porta a delle complicanze e a delle decisioni non ottimali per il sistema

proprio per questa ragione nasce una separazione
#### Separazione tra meccanismo e politica di scheduling
- il **meccanismo di scheduling** riguarda tutte le varie implementazioni tecniche dell'algoritmo nel kernel del sistema operativo
- le **politiche di scheduling** riguardano tutte quelle regole che decidono chi deve essere eseguito e quando
ciò ci consente di far modificare eventuali politiche ai processi utente senza però modificare le tecniche implementative nel kernel
>[!example] un processo può modificare la politica e dire "i miei due processi figli devono avere priorità 2"
>- nel frattempo il kernel sta "semplicemente" eseguendo un algoritmo di scheduling a priorità
### Parallelismo
Il **parallelismo** è la capacità di un sistema di eseguire più operazioni contemporaneamente.
Si divide in due livelli principali
- **livello di processo**, dove processi indipendenti vengono eseguiti in parallelo
- **livello di thread**, in cui più thread all'interno dello stesso processo lavorano simultaneamente, condividendo memoria e risorse
Lo scheduling varia a seconda che si tratti di **thread a livello utente** o **thread a livello kernel**


#### Thread a livello utente
il kernel non è consapevole di ciò che si cela dietro un processo e lo vede come un unico blocco
- i thread sono una cosa interna al processo ed è il processo a gestirli
- lo scheduler assegnerà quantum di tempo a un processo e non a un singolo thread
![[Pasted image 20241120180934.png|400]]

In questo esempio un possibile ordine è `A1` -> `A2` -> `A3` -> (ricomincia il giro) `A1` -> `A2` -> `A3` 
Ciò che non può MAI succedere è questo `A1` -> `B1`, perché prima eseguo SOLO `A` 

Il problema però si verifica se un thread consuma tutto il quanto di tempo, in quel caso gli altri thread dello stesso processo non verranno eseguiti fino al prossimo turno.
#### Thread a livello kernel
Qui i thread sono visibili dal kernel e possono essere scelti da esso per l'esecuzione
Se un thread eccede il quanto viene sospeso
![[Pasted image 20241120181216.png|400]]
Qui i casi possibili sono 
- `A1` -> `A2` -> `A3` -> (ricomincia il giro) `A1` -> `A2` -> `A3` 
- `A1` -> `B1` -> `A2` -> `B2`
Questo approccio aumenta la flessibilità e sfrutta meglio il parallelismo, ma può introdurre un overhead maggiore rispetto al livello utente, a causa dell'intervento più frequente del kernel.
#### Differenze prestazionali tra livello utente e kernel
***LIVELLO UTENTE***
Qui il passaggio da un thread all'altro è molto veloce, perché richiede solo poche istruzioni senza coinvolgere il kernel. Però in caso di blocco su operazioni di I/O, l'intero processo viene sospeso.

***LIVELLO KERNEL***
Qui lo scambio di thread è più lento, ma se un thread si blocca su un'operazione di I/O solo lui viene sospeso, mentre gli altri continuano ad essere eseguiti
Inoltre, il kernel può
- considerare i costi per passare da un thread all'altro
- dare priorità ai thread dello stesso processo

Alcune applicazioni hanno la possibilità di gestire direttamente lo scheduling dei propri thread, senza affidarsi completamente al kernel. In pratica, l'applicazione implementa un sistema di scheduling personalizzato (chiamato **scheduling specifico**) per decidere come e quando i propri thread devono essere eseguiti.


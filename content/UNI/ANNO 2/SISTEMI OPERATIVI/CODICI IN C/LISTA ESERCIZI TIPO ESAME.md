# **TRACCE DI ESERCIZI IN C PER SISTEMI OPERATIVI**

---

## **PROCESSI**

### **ESERCIZIO 1**

Creare un programma che legge un file e conta le occorrenze di una parola nel seguente modo:

- Il primo processo legge dall’inizio alla metà e conta le occorrenze della parola.
- Il secondo processo legge dalla metà fino alla fine e conta le occorrenze della parola.
- Inviano poi il numero di occorrenze al processo padre, il quale le somma e le stampa a video.

>[!success]  [[1.PROCESSI CHE LEGGONO OCCORRENZE FILE]]


---

### **ESERCIZIO 2**

Generare due processi figli che comunicano con il padre:

- Uno dei processi genera numeri casuali `[0-100]` ed invia al padre solo i numeri pari.
- L’altro processo genera numeri casuali `[0-100]` ed invia al padre solo i numeri dispari.
- Il padre fa la loro somma e quando la somma > 190, termina l’esecuzione dei figli.

>[!success] [[2.PROCESSI GENERATI P1 E P2]]

---

### **ESERCIZIO 3**

Un processo padre genera due processi figli:

- Il primo processo figlio invia al padre un numero casuale da `0` a `100`.
- Il padre legge questo numero, lo moltiplica per un `k` casuale e lo manda al secondo figlio.
- Il secondo figlio legge il numero inviato dal padre e lo stampa a video.

>[!success] [[3.PROCESSI CHE SI PASSANO NUMERI]]

---

### **ESERCIZIO 4**

Due processi leggono dallo stesso file che si trova all’interno di una directory (es. `/data/file.txt`):

- **Alternativa**: Usare `dirent` e `readdir` per leggere all’interno della directory e controllare se il file esiste o meno.
- Controllare che il file sia in modalità lettura, altrimenti restituire errore.
- **Alternativa**: Invece di restituire un errore, cambiare i permessi al file con `chmod`.
- Il primo processo legge dall’inizio del file fino a metà.
- Il secondo processo legge dalla metà in poi.
- I figli mandano il contenuto al padre.
- Il padre lo stampa nel seguente formato: `[PID_FIGLIO] -> TESTO`.

>[!success] [[4.PROCESSI LEGGONO SU FILE]]

---

### **ESERCIZIO 5**

Scrivere un programma che esegue la moltiplicazione tra matrici 3x3 usando la programmazione parallela:

- Il primo processo figlio computa la prima colonna.
- Il secondo processo figlio computa la seconda colonna.
- Il processo padre computa la terza colonna, riceve dai figli i due vettori colonna computati, compone la matrice finale e la stampa.

>[!success] [[5.PROCESSI MOLTIPLICANO MATRICI]]

---

### **ESERCIZIO 6**

Generare due processi figli che comunicano con il padre:

- Uno dei processi genera numeri casuali `[0-50]` ed invia al padre solo i numeri multipli di `3`.
- L’altro processo genera numeri casuali `[51-100]` ed invia al padre solo i numeri multipli di `2`.
- Il padre stampa i numeri ricevuti ed esegue la loro somma quando la somma > `130`.

>[!success] [[6.SOMMA MULTIPLI 3 E 2]]

---

### **ESERCIZIO 7**

Scrivere un programma C che crea un processo figlio:

- Il padre legge un numero casuale e lo invia al figlio attraverso una pipe.
- Il figlio fa il quadrato del numero e lo invia nuovamente al padre solo se il quadrato è pari, attraverso la pipe.
- Il padre legge il numero e lo stampa.

>[!success] [[7.PROCESSI E POTENZA DI UN NUMERO]]

---

### **ESERCIZIO 8**

Scrivere un programma C che svolge le seguenti richieste:

- Un processo padre genera due processi figli. Ciascun processo inizializza un proprio array di `N` interi.
- Il primo processo invia al processo padre solo i numeri in posizioni pari, e il secondo processo solo i numeri in posizioni dispari.
- Il padre riceve questi numeri e li scrive in un array di `N` interi, mettendo in posizioni pari i numeri ricevuti dal primo figlio, e in posizioni dispari i numeri ricevuti dal secondo figlio.
- Il padre stampa l’array e calcola il max e il min.

>[!success] [[8. array dispari pari]]

---

### **ESERCIZIO 9**

Implementare un programma che utilizzi `fork` e pipe per la comunicazione tra processi:

- Il programma crea un file di testo e poi due processi figli.
- Un processo figlio scrive una sequenza di numeri interi pari nel file.
- L’altro processo figlio scrive una sequenza di numeri interi dispari nello stesso file.
- Il processo padre legge i dati dal file e li stampa a video.

>[!success] [[9.Esercizio file]]

---

## **THREAD**

### **MUTEX**

---

### **ESERCIZIO 1**

Scrivere un programma C che segue le seguenti specifiche:

- Il programma crea un buffer come array di `11` numeri interi, inizializzati a zero.
- Genera tre thread:
    - Il primo thread sceglie casualmente una cella del buffer e vi scrive il numero `+1`.
    - Il secondo thread sceglie casualmente una cella del buffer e vi scrive il numero `-1`.
    - Il terzo thread controlla se tutte le celle del buffer sono state inizializzate. In caso positivo, determina se il numero di celle contenenti `+1` è maggiore di quelle con `-1` e termina tutti i thread.
    - Mentre un thread accede al buffer, nessun altro deve accedervi. Ogni thread attende un tempo random tra `0` e `3` secondi.

>[!success] [[10. thread +1 -1]]

---

### **ESERCIZIO 2**

Scrivere un programma con tre thread che risolvono il seguente problema:

- Un buffer di `n` elementi inizializzato a `-1` viene riempito nel seguente modo:
    - Il primo thread aggiunge nelle posizioni pari del buffer un numero casuale da `0` a `100`.
    - Il secondo thread aggiunge nelle posizioni dispari del buffer un numero casuale da `100` a `200`.
    - Il terzo thread modifica il buffer nel seguente modo:
        - `buff[0] = buff[0]`
        - `buff[1] = buff[1] + buff[0]`
        - `buff[2] = buff[1] + buff[2]`
- Utilizzare la mutua esclusione.

>[!success] [[11. thread -1 0 100]]

---

### **ESERCIZIO 3**

Scrivere un programma in C con tre thread che operano su due array di dimensione `N` inizialmente a `0`:

- Il primo thread scrive in un array `A` numeri casuali tra `1` e `150`, in posizioni randomiche.
- Il secondo thread scrive in un array `B` numeri casuali tra `150` e `300`, in posizioni randomiche.
- Il terzo thread calcola:
    - Il massimo e il minimo in `A` e `B`.
    - `max{max(A), max(B)}` e `min{min(A), min(B)}`.

>[!success] [[12. MAX E MIN]]

---

## **SEMAFORI**

---

### **ESERCIZIO 1**

Due thread:

- Il produttore inserisce numeri pari da `0` a `100` in posizioni pari e numeri dispari da `100` a `200` in posizioni dispari in un buffer di `N` elementi inizializzato a `-1`.
- Il consumatore legge dal buffer un numero pari e uno dispari, li somma e stampa la somma.


>[!success] [[13. SEMAFORI E POSIZIONI PARI]]

---

### **ESERCIZIO 2**

Scrivere un programma in C che, data una stringa di `N` caratteri, crea `N/2` thread che stampano ciascuno un carattere della stringa in maiuscolo. Usare semafori binari o mutex.


>[!success] [[14. ESERCIZIO THREAD 2]]


---

### **ESERCIZIO 3**

Sei thread: uno scrittore e cinque lettori.

- Lo scrittore scrive su un buffer numeri dispari da `0` a `50` nelle posizioni pari e numeri pari da `50` a `100` nelle posizioni dispari.
- I lettori leggono coppie di numeri (pari, dispari), li sommano e stampano i risultati.


>[!success] [[15. esercizio 5 lettori 1 scrittore]]

---
## **ESAMI**
#### ESERCIZIO SCRITTO C
Sviluppare un programma in linguaggio C che utilizza processi e pipe per implementare quanto specificato di seguito. 
Un processo padre P genera due processi figli P1 e P2. 
Inizialmente, tutti i processi devono disabilitare il segnale di interruzione SIGINT; in particolare all’arrivo di tale segnale deve essere visualizzato il messaggio di avviso “Interruzione disabilitata”. 
I due figli P1 e P2 generano ogni secondo un numero intero casuale da 0 a 100. I numeri generati dai figli vengono inviati al processo padre che provvede a sommarli e stamparli su schermo e a memorizzarli in un file.
L’esecuzione di tutti e tre i processi viene rimandata dal processo padre quando verifica che la somma dei numeri avuti dai processi figli assume il valore 100, altrimenti mette in attesa per 2 secondi prima di controllare i due numeri inviati dai processi figli.

>[!success] [[Esercizio Esame]]
#### DOMANDA APERTA
Si invita il candidato a esporre una dettagliata analisi del concetto di memoria virtuale e del suo ruolo cruciale all'interno di un sistema operativo moderno. Come contribuisce la memoria virtuale ad estendere la capacità della memoria fisica e quale effetto ha sulle prestazioni generali del sistema? In aggiunta, si fornisca una definizione chiara di 'page fault' e si illustri il processo attraverso il quale il sistema operativo gestisce tale evento.

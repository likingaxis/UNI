```c
/*

  

Esempio dello schema Produttore Consumatore in C usando POSIX

  

Autore. Danilo Croce

  

NOTA: per essere eseguito in ambiente LINUX usare gcc -pthread source_file.c -o binary_output

  

WARNING: sembra non funzionare su MAC OS X

  

*/

  

#include <pthread.h>

#include <stdio.h>

#include <stdlib.h>

#include <unistd.h>

#include <semaphore.h>

  

#define N 10 /* numero di posti nel buffer */

#define TRUE 1

  

/* Dichiarazione dei semafori */

sem_t mutex; // Semaforo per l'accesso esclusivo alla regione critica

sem_t empty; // Semaforo per contare i posti vuoti nel buffer

sem_t full; // Semaforo per contare i posti pieni nel buffer

  

int buffer[N]; // Buffer condiviso tra produttore e consumatore

int in = 0; // Indice dove inserire il prossimo elemento nel buffer

  

/* Funzioni helper per utilizzare i semafori */

void down(sem_t *sem) {

sem_wait(sem); //http://www.csc.villanova.edu/~mdamian/threads/posixsem.html#wait

}

  

void up(sem_t *sem) {

sem_post(sem); //http://www.csc.villanova.edu/~mdamian/threads/posixsem.html#post

}

  

/* Funzione per inserire un elemento nel buffer */

void insert_item() {

    int item = rand() % 100; // Genera un elemento casuale

    printf("\nInserisco %d in posizione %d\n", item, (in + 1));

buffer[in] = item; // Inserisce l'elemento nel buffer

in++; // Incrementa l'indice

}

  

/* Funzione per rimuovere un elemento dal buffer */

void remove_item() {

    printf("%i", in);

int item = buffer[in - 1];

printf("\nPrelevo %d da posizione %d\n", item, in);

in--; // Decrementa l'indice

}

  

/* Funzione per stampare il contenuto del buffer */

void print_buffer(){

    for(int i=0; i<in; i++){

        printf("%d ", buffer[i]);

	}
printf("\n");

}

  

/* Funzione eseguita dal thread del produttore */

void *producer(void *arg) {

    while (TRUE) {

        down(&empty); // Attende finché ci sono posti vuoti nel buffer

        down(&mutex); // Entra nella regione critica

  

        insert_item(); // Inserisce un elemento nel buffer

        print_buffer(); // Stampa il contenuto del buffer

  

        up(&mutex); // Esce dalla regione critica

        up(&full); // Segnala che c'è un posto pieno in più nel buffer

    }

}

  

/* Funzione eseguita dal thread del consumatore */

void *consumer(void *arg) {

    while (TRUE) {

        down(&full); // Attende finché ci sono posti pieni nel buffer

        down(&mutex); // Entra nella regione critica

  

        remove_item(); // Rimuove un elemento dal buffer

        print_buffer(); // Stampa il contenuto del buffer

  

        up(&mutex); // Esce dalla regione critica

        up(&empty); // Segnala che c'è un posto vuoto in più nel buffer

    }

}

  

int main() {

pthread_t prod, cons; // Dichiarazione dei thread

  

// Inizializzazione dei semafori

sem_init(&mutex, 0, 1);

sem_init(&empty, 0, N);

sem_init(&full, 0, 0);

  

// Creazione dei thread

pthread_create(&prod, NULL, producer, NULL);

pthread_create(&cons, NULL, consumer, NULL);

// Attesa della terminazione dei thread

pthread_join(prod, NULL);

pthread_join(cons, NULL);

  

// Distruzione dei semafori

sem_destroy(&mutex);

sem_destroy(&empty);

sem_destroy(&full);

  

return 0;

}
```

includiamo la libreria `semaphore.h` per utilizzare i semafori una struttura che consente l'accesso ai dati o lo vieta
usiamo `sem_t` per dichiarare dei contatori a semaforo globali
uno sarà un semplice lock per la regione critica dove vengono o scritte o lette le cose nel buffer
poi avremo due contatori uno per i full e uno empty
serve per dire al produttore se può produrre o al consumatore se può consumare
creiamo una funzione down che decrementa quel determinato semaforo se maggiore di 0
con `sem_wait(sem);`
un'altra che incrementa con 
`sem_post(sem);`
insert item semplicemente inserisce un elemento e aggiorna `in`
poi abbiamo quello che toglie l'ultima posizione perché tanto è una sorta di lifo questo buffer.
uno che stampa abbastanza ok
##### creiamo la funzione producer
facciamo un decremento alla empty quindi aspettiamo che ci siano dei posti liberi $>0$
abbassa il mutex se esso è libero quindi 1 e entra nella regione critica
inserisce l'item e lo stampa
alza il mutex e incrementa anche il pieno perché significa che è stato messo un elemento in più
##### il consumer invece
fa un decremento se full è >0
entra nel mutex se 1
toglie l'elemento e lo stampa
alza il mutex 
alza l'empty

Nel main creiamo due thread uno produttore uno consumatore prima li dichiariamo
poi creiamo i semafori effettivi con `sem_init` che puntano all'indirizzo dei semafori dichiarati globalmente
inizializziamo con
`sem_init(&mutex, 0, 1);`
dove il primo è un puntatore alla variabile che poi verrà modificata
la seconda indica se è un semaforo condiviso con altri thread del processo `0` oppure con altri thread di altri processi `1` il terzo indica il valore iniziale del semaforo in questo caso 1

andiamo a creare i thread produttore e consumatore puntando alle variabili dichiarate prima mettendo opzioni NULL e specifichiamo la funzione che andranno a fare e non passiamo parametri
attendiamo che i due finiscano con join senza ritornare nulla
distruggiamo i semafori con 
`sem_destroy(indirizzo semaforo)`

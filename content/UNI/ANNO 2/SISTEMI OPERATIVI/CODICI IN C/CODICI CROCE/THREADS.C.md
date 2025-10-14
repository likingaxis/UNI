  ```c
// Includi le librerie necessarie per il programma

#include <pthread.h>

#include <stdio.h>

#include <stdlib.h>

#include <unistd.h>

  

// Definisci una costante per il numero di thread da creare

#define NUMBER_OF_THREADS 10

  

// Funzione che verrà eseguita da ogni thread

void * print_hello_world(void * tid) {

    // Genera un numero casuale tra 0 e 4 (quanti secondi far dormire il thread)

    int r = rand()%5;

    // Fa dormire il thread per un numero casuale di secondi

    sleep(r);

    // Stampa un messaggio con l'ID del thread

    printf("Hello World. Greetings from thread %d\n", tid);

    // Termina il thread e restituisce NULL

    pthread_exit(NULL);

}

  

int main(int arg, char* argv []) {

    // Dichiarazione di un array di thread

    pthread_t threads[NUMBER_OF_THREADS];

    int status, i;

  

    // Ciclo per creare NUMBER_OF_THREADS thread

    for (i=0; i < NUMBER_OF_THREADS; i++) {

        // Crea un nuovo thread e assegna la funzione print_hello_world come funzione di avvio

        status = pthread_create(&threads[i], NULL, print_hello_world, (void * ) i);

        if (status == 0){

            // Stampa l'ID del thread creato e il suo stato

            printf("Process %d created with status %d\n", i, status);

        }

        // Se ci sono problemi nella creazione del thread, stampa un messaggio di errore e termina il programma

        else{

            printf("Problems while creating process %d\n", i);          

            exit (-1);

        }

    }

  

    // Ciclo per attendere che tutti i thread terminino

    for (i=0; i < NUMBER_OF_THREADS; i++) {

        status = pthread_join(threads[i], NULL);

        // Stampa l'ID del thread che ha terminato e il suo stato

        printf("Process %d terminated with status %d\n", i, status);

        // Se ci sono problemi nell'attesa del thread, stampa un messaggio di errore e termina il programma

        if (status != 0){

            printf("Problems while waiting for process %d\n", i);           

            exit (-1);

        }

    }

  

    // Termina il programma principale

    return 0;

}
```
usiamo `pthread.h` per fare operazioni su thread

creiamo una funzione con puntatore generico `void *` 

i thread funzionano creando un array che li contenga in questo caso 10 l'array sarà di tipo 
`pthread_t`
dopo aver istanziato dello spazio per ogni thread dobbiamo crearli effettivamente attraverso
`pthread_create`
con un ciclo for
`pthread_create(&threads[i], NULL, print_hello_world, (void * ) i)`
andiamo a creare un thread dando come prima cosa l'indirizzo di memoria del `pthread` detto prima poi mettiamo `NULL` perché ci sono una serie di opzioni che non ci servono e richiamiamo la funzione che deve fare passandogli come argomento la cosa dopo la virgola in questo caso i che verrà castato come un `void *`
alla fine i è il numero del thread se ci pensi

questa funzione create ritorna 0 se è stato creato con successo o valori maggiori se errore

se avvengono errori facciamo un controllo

facciamo `pthread_join(threads[i], NULL);`
per ogni thread con un ciclo for
esso attende la terminazione dei singoli thread mettendosi in wait
il secondo argomento è un puntatore che si dovrebbe salvare il valore di ritorno del thread che altrimenti andrebbe perso
errore se maggiore di 0 altrimenti 0 se è un successo

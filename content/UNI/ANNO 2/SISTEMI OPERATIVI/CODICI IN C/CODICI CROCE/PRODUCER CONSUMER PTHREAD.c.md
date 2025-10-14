```c
#include <stdio.h>

#include <pthread.h>

#include <stdlib.h>

#include <unistd.h>

  

#define MAX 10 /* Quantità di numeri da produrre */

  

/*

NOTA: rispetto all'esempio 6.2_producer_consumer_semaphore.c, questo esempio ha l'obiettivo

di mostrare l'accesso alternato (in mutua esclusione) dei due thread, non

*/

  

/* Dichiarazione di mutex e variabili condizionali */

pthread_mutex_t the_mutex;

pthread_cond_t condc, condp; /* Usate per segnalare tra produttore e consumatore */

  

int buffer = 0; /* Buffer utilizzato tra produttore e consumatore */

  

/* Funzione del produttore */

void *producer(void *ptr) {

int i;

for (i = 1; i <= MAX; i++) {

pthread_mutex_lock(&the_mutex); /* Ottiene l'accesso esclusivo al buffer */

  

/*

NOTA: La ragione per cui viene utilizzato un ciclo while invece di un semplice

if è legata alla necessità di gestire le cosiddette "false sveglie"

(spurious wakeups) che possono accadere con pthread_cond_wait.

Ci assicuriamo che ogni volta che il thread viene svegliato,

ricontrolli effettivamente la condizione.

*/

while (buffer != 0) {

pthread_cond_wait(&condp, &the_mutex);

}

  

buffer = i; /* Inserisce l'elemento nel buffer */

printf("Producing:\t%d\n", i);

sleep(rand()%2);

pthread_cond_signal(&condc); /* Sveglia il consumatore */

pthread_mutex_unlock(&the_mutex); /* Rilascia l'accesso al buffer */

}

  

pthread_exit(0);

}

  

/* Funzione del consumatore */

void *consumer(void *ptr) {

int i;

for (i = 1; i <= MAX; i++) {

pthread_mutex_lock(&the_mutex); /* Ottiene l'accesso esclusivo al buffer */

  

while (buffer == 0) {

pthread_cond_wait(&condc, &the_mutex);

}

  

printf("Consuming:\t%d\n", i);

buffer = 0; /* Preleva un elemento dal buffer e lo reinizializza */

sleep(rand()%2);

pthread_cond_signal(&condp); /* Sveglia il produttore */

pthread_mutex_unlock(&the_mutex); /* Rilascia l'accesso al buffer */

}

  

pthread_exit(0);

}

  

int main(int argc, char **argv) {

pthread_t pro, con; /* Threads del produttore e consumatore */

  

/* Inizializzazione di mutex e variabili condizionali */

pthread_mutex_init(&the_mutex, NULL);

pthread_cond_init(&condc, NULL);

pthread_cond_init(&condp, NULL);

  

/* Creazione dei threads */

pthread_create(&con, NULL, consumer, NULL);

pthread_create(&pro, NULL, producer, NULL);

  

/* Attesa che i threads completino l'esecuzione */

pthread_join(pro, NULL);

pthread_join(con, NULL);

  

/* Pulizia e distruzione di mutex e variabili condizionali */

pthread_cond_destroy(&condc);

pthread_cond_destroy(&condp);

pthread_mutex_destroy(&the_mutex);

  

return 0;

}
```
in questo caso il codice crea un thread mutex e non un semaforo
`pthread_mutex_t`
dichiariamo anche `pthread_cond_t` per fare degli eventi su cui si baseranno i mutex
creiamo la funzione del producer che blocca il mutex e finché il buffer è diverso da 0 fa
creiamo una attesa con `pthread_cond_wait` passando la variabile di condizione `condp` e il `mutex`
il mutex verrà sbloccato perché andiamo in attesa di quello che farà il consumatore

dopodiché inseriamo l'elemento nel buffer lo stampiamo e inviamo il segnale che risveglia il consumatore `condc`
sblocchiamo il mutex

funzione del consumatore analoga e risveglia `condp`
nel main creiamo due thread `pro` e `con`
inizializziamo le cond e il mutex
creiamo due thread legandoli alle dichiarazioni prima e gli passiamo le due funzioni
attendiamo che finiscano 
distruggiamo le cond e i mutex

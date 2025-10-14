```c
#include <stdio.h>

#include <unistd.h>

#include <stdlib.h>

#include <time.h>

  

int main() {

// Inizializza il generatore di numeri casuali

srand(time(NULL));

  

for (int i = 20; i >= 1; i--) {

printf("%d\n", i);

fflush(stdout); // Assicura che l'output venga visualizzato immediatamente

  

// Dormi per un tempo casuale tra 0 e 2 secondi

sleep(rand() % 3);

}

  

printf("\nBYE\n");

fflush(stdout);

  

return 0;

}
```

##### SPIEGAZIONE
##### Importo librerie in particolare
`<time.h>` che ha delle funzionalità per lavorare su date e tempo
##### Codice
`srand` imposta come deve generare numeri casuali la funzione rand in base a un determinato seme in questo caso time(null) che ritorna il numero di secondi trascorsi dal 1970 quindi una roba tipo $1708739200$

`fflush(stdout)` il `printf` prima di questo comando viene fatto immediatamente anche senza aspettare la fine del codice
`sleep` simula una attesa di tot secondi in questo caso se si fa un rand e %3 avremo dei numeri che vanno da 0 a 2 se volessimo fare da 0 a 3 dobbiamo mettere+1

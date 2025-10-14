```c
#include <stdio.h>

#include <stdlib.h>

#include <unistd.h>

  

// Definizione di costanti per leggibilità per i descrittori di file

#define STDIN 0

#define STDOUT 1

#define PIPE_RD 0 // Lato di lettura della pipe

#define PIPE_WR 1 // Lato di scrittura della pipe

  

int main(int argc, char** argv) {

  

pid_t cat_pid, sort_pid;

int fd[2]; // Descrittori di file per la pipe: fd[0] per leggere, fd[1] per scrivere

pipe(fd); // Crea una pipe. fd[PIPE_RD] sarà l'estremità di lettura, fd[PIPE_WR] sarà l'estremità di scrittura

  

cat_pid = fork(); // Fork del processo corrente

  

if (cat_pid == 0) {

// Questo è il processo figlio per 'cat'

close(fd[PIPE_RD]); // Chiude l'estremità di lettura della pipe, non necessaria qui

close(STDOUT); // Chiude l'output standard

  

/*

  

La funzione dup viene utilizzata nei programmi Unix/Linux per duplicare un

file descriptor esistente, ottenendo un secondo file descriptor che punta alla

stessa risorsa interna (ad esempio, uno stesso file o lato di una pipe).

Questo nuovo file descriptor e' il più Basso Disponibile: dup sceglie automaticamente

il numero di file descriptor più basso che è disponibile nel processo corrente.

Per esempio, se i file descriptor 0, 1, e 2 sono chiusi,

dup utilizzerà il 0 per la sua duplicazione.

  

*/

  

dup(fd[PIPE_WR]); // Duplica l'estremità di scrittura della pipe al descrittore di

// file dell'output standard. Ora, 'cat' scriverà sulla pipe invece che sul terminale

execl("/bin/cat", "cat", "names.txt", NULL); // Esegui il comando 'cat'

}

  

sort_pid = fork(); // Fork del processo corrente ancora per 'sort'

  

if (sort_pid == 0) {

// Questo è il processo figlio per 'sort'

close(fd[PIPE_WR]); // Chiude l'estremità di scrittura della pipe, non necessaria qui

close(STDIN); // Chiude l'input standard

dup(fd[PIPE_RD]); // Duplica l'estremità di lettura della pipe al descrittore di file dell'input standard

// Ora, 'sort' leggerà dalla pipe invece che dalla tastiera

execl("/usr/bin/sort", "sort", NULL); // Esegui il comando 'sort'

}

  

// Questo è il processo genitore

close(fd[PIPE_RD]); // Chiude l'estremità di lettura della pipe, il genitore non la usa

close(fd[PIPE_WR]); // Chiude l'estremità di scrittura della pipe, il genitore non la usa

  

// Aspetta che i processi figli terminino

waitpid(cat_pid, NULL, 0); // Aspetta il processo 'cat'

waitpid(sort_pid, NULL, 0); // Aspetta il processo 'sort'

  

return 0;

}
```
definisco delle costanti per facilitare la scrittura dei descrittori
ricapitolando i descrittori sono dei codici che associano a un tipo di file

|**Descrittore di File**|**Macro associata**|**Descrizione**|**Default**|
|---|---|---|---|
|**0**|`STDIN_FILENO`|Input standard|Tastiera (in interattivo)|
|**1**|`STDOUT_FILENO`|Output standard|Terminale (in interattivo)|
|**2**|`STDERR_FILENO`|Output standard per errori|Terminale (in interattivo)|
e poi le pipe con 0 e 1 dove 0 indica la lettura e 1 la scrittura

#### Creazione di pid
`pid_t` viene usato per indicare il pid di un processo, alla fine è un intero ma per chiarezza si usa questo può anche essere usato per indicare un riscontro dopo la fork tipo 0 per i figli ecc

abbiamo creato un array che contiene i 2 elementi del descriptor per la pipe
`pipe(fd)` crea una pipe associata al file descriptor
- `fd[PIPE_RD]` sarà la lettura
- `fd[PIPE_WR]` sarà la scrittura
ma semplicemente usa 0 e 1 solo che usa le costanti
creo un processo e mi salvo il suo stato in `cat_pid`
è previsto che il figlio non legga nella pipe e non scriva nello stdout 
`dup(fd[PIPE_WR]);` viene usato per dire al processo corrente di non scrivere più sullo stdout o dove doveva fare ma di scrivere nella cosa tra parentesi in questo caso la pipe in scrittura
con `dup` di default viene messo il `fd` più basso anche se è chiuso
#### Uso di execl
`execl("/bin/cat", "cat", "names.txt", NULL);`
viene usato per eseguire un comando della bash in questo caso cat
[[SISTEMI OPERATIVI LEZ.4-5-6-7#Carrellata di comandi|spiegazione cat]]
funziona così
`execl("directory del comando", "nome comando", opzioni separate da ",", NULL per indicare la fine delle opzioni);`

creazione del processo corrente e mettiamo in sort
chiudiamo le varie scritture e ci appoggiamo alla lettura facendo un sort di quello che ci ha dato cat
quando usciamo da tutti i processi 0 quindi figli dobbiamo scrivere il codice per il padre
chiudiamo le cose inutilizzate(tutto)
e aspettiamo che i due figli terminino per andare a terminare il codice
`waitpid(cat_pid, NULL, 0); // Aspetta il processo 'cat'`
funziona così
`pid_t waitpid(pid_t pid, int *status, int options);`
pid può essere uno in particolare oppure 
- **`-1`**: Aspetta qualsiasi processo figlio.
- **`0`**: Aspetta qualsiasi processo figlio appartenente allo stesso gruppo.

lo status può essere messo in una variabile per aggiornare lo stato del processo in questo caso NULL

la 3 Modifica il comportamento della chiamata. Ad esempio:
- **`0`**: Comportamento predefinito (attende fino a quando il processo termina).

da sapere?
- **`WNOHANG`**: Non si blocca se il processo specificato non è terminato.
- **`WUNTRACED`**: Con questa opzione, `waitpid` riporta anche i processi figli che sono stati **sospesi** (es. con un segnale come `SIGSTOP`).

se waitpid termina restituisce il pid del processo che termina
oppure altre cose in base a quelle opzioni

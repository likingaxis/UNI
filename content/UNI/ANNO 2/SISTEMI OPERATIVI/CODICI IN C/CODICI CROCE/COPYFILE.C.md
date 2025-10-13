```C
/* Programma di copia di file con controllo errori minimale e reportistica. */

  

#include <sys/types.h> // Include i file header necessari

#include <fcntl.h>

#include <stdlib.h>

#include <unistd.h>

#include <stdio.h>

  

#define BUF_SIZE 4096 // Dimensione del buffer: 4096 byte

#define OUTPUT_MODE 0700 // Bit di protezione per file di output

  

#define TRUE 1

  

// Prototipo della funzione main secondo lo standard ANSI

int main(int argc, char *argv[]);

  

int main(int argc, char *argv[]) {

int in_fd, out_fd; // File descriptor per i file di input e output

int rd_count, wt_count; // Contatori per la lettura e scrittura

char buffer[BUF_SIZE]; // Buffer per la lettura e scrittura dei dati



// Controllo del numero di argomenti

if (argc != 3) {

// Stampa un messaggio di errore se il numero di argomenti non è corretto

fprintf(stderr, "Errore di sintassi. Uso: %s input_file_path output_file_path\n", argv[0]);

exit(1);

}

  

// Apertura del file di input

in_fd = open(argv[1], O_RDONLY); // Apre il file di origine

if (in_fd < 0) exit(2); // Se non può aprirlo, esce

  

// Creazione del file di output

// Nota: equivalenza tra

// - creat(path, mode);

// - open(path, O_WRONLY | O_CREAT | O_TRUNC, mode);

// YES: Ken Thompson, the creator of Unix, once joked that the missing letter was his largest regret in the design of Unix.

out_fd = creat(argv[2], OUTPUT_MODE); // Crea il file di destinazione

if (out_fd < 0) exit(3); // Se non può crearlo, esce

  

// Ciclo di copia

while (TRUE) {

rd_count = read(in_fd, buffer, BUF_SIZE); // Legge un blocco di dati

if (rd_count <= 0) break; // Se fine del file o errore, esce dal ciclo

  

wt_count = write(out_fd, buffer, rd_count); // Scrive i dati

if (wt_count <= 0) exit(4); // wt_count <= 0 è un errore

}

  

// Chiusura dei file

close(in_fd);

close(out_fd);

  

if (rd_count == 0) exit(0); // Nessun errore sull’ultima lettura

else exit(5); // Errore sull’ultima lettura

}
```

`#include <fcntl.h>` serve per aprire i file con open o roba simile
definisco come dimensione del buffer 4096 byte
definisco le proprietà di accesso in questo caso solo il proprietario può fare tutto.

|**Bit**|**Valore**|**Descrizione**|
|---|---|---|
|**4**|Lettura|Permesso di leggere.|
|**2**|Scrittura|Permesso di scrivere.|
|**1**|Esecuzione|Permesso di eseguire.|
Creo un prototipo della funzione tipo le interfacce(serve davvero?bho)
creazione di un buffer che alla fine è un array di char lungo 4096
l'esercizio prevede 3 stringhe quindi si fa un controllo se sono stati messi dei numeri differenti

in caso si va a fare una print sullo standard error e un exit con errore quindi 1
`fprintf(stderr, "Errore di sintassi. Uso: %s input_file_path output_file_path\n", argv[0]);`

salva open in un intero, open restituisce il file descriptor che ormai conosciamo
e gli passiamo una stringa path e il modo in cui deve aprirlo `O_RDONLY`
se abbiamo un file descriptor negativo c'è un problema e facciamo una exit con errore
usiamo questo comando
`out_fd = creat(argv[2], OUTPUT_MODE);`
per creare un file nel path definito dalla stringa e mettiamo output mode 
anche creat ritorna il file descriptor
facciamo un ciclo while infinito e facciamo una read sul buffer
specificando il file descriptor da cui prendere il buffer su cui scrivere e la dimensione del buffer
`rd_count = read(in_fd, buffer, BUF_SIZE);`
se la read ha un valore negativo allora c'è stato un errore altrimenti conta i byte letti
funziona in modo simile la write
`wt_count = write(out_fd, buffer, rd_count);`

un errore può anche essere la fine della lettura
se l'ultima lettura ha ritornato 0 significa nessun errore e abbiamo finito di leggere e possiamo fare exit(0)

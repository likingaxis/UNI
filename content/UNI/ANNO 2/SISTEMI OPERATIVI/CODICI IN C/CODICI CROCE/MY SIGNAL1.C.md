```c
#include <stdio.h>

#include <stdlib.h>

#include <signal.h>

#include <unistd.h>

#include <string.h> // Per strsignal()


void signalHandler(int signum) {

printf("Interrupt signal %d received which is %s\n", signum, strsignal(signum));

// cleanup and terminate program

exit(signum);

}

  

int main() {

// register signal SIGINT and signal handler

signal(SIGINT, signalHandler); // CTRL+C

  

while(1) {

printf("Going to sleep...\n");

sleep(1);

}

  

return 0; // questa riga non verrà mai raggiunta a causa del ciclo while(1)

}
```

includo in particolare la libreria signal per gestire i segnali
creo una funzione che gestisce i segnali e che non ritorna nulla
strsignal ritorna una stringa descrittiva in base al segnale tipo se passo un sig int che è 2 la sua stringa descrittiva sarà "interrupt"
fa exit e ritorna la funzione exit il codice del segnale fatto
nel main genera un segnale e gli passa 
- SIGINT che è una costante della libreria signal.h e indica 2 e termina il programma
- la funzione che gestisce il segnale
creo un loop infinito che fa uno sleep di 1 secondo ma abbiamo prima creato l'attesa di un possibile segnale in questo caso CTRL+C che termina il programma
SIG_DFL per mettere un handler di default


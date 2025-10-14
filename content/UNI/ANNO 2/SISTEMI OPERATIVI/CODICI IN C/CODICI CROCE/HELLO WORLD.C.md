## 1. HELLO WORLD
```c
#include <unistd.h>

#include <stdio.h>

  

int main()

{

    printf("Hello world.\n");

    return 0;

}
```
vabbè un classico
## 2. HELLO WORLD
```c
#include <unistd.h>

#include <stdio.h>

  

#define STDOUT 1

  

int main()

{

    char msg[] = "Hello World!\n";

    write(STDOUT, msg, sizeof(msg));

  

    return 0;

}
```
si utilizza un array di caratteri e si effettua una write sul file descriptor 1
## 3. HELLO WORLD
```c
#include <unistd.h>

#include <stdio.h>

#include <sys/syscall.h>

#define STDOUT 1

  

int main(int argc, char **argv)

{

    char msg[] = "Hello World!\n";

    int nr = SYS_write;

    syscall(nr, STDOUT, msg, sizeof(msg));

    return 0;

}
```
si fa una chiamata di sistema specificando la chiamata il file descriptor e la stringa e la sua dimensione

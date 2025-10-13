>[!tip] consegna
>Sviluppare un programma in linguaggio C che utilizza processi e pipe per implementare quanto 
>specificato di seguito. 
> Un processo padre P genera due processi figli P1 e P2. 
> Inizialmente, tutti i processi devono disabilitare il segnale di interruzione SIGINT; in particolare 
> all’arrivo di tale segnale deve essere visualizzato il messaggio di avviso “Interruzione 
> disabilitata”. 
> I due figli P1 e P2 generano ogni secondo un numero intero casuale da 0 a 100. 
> I numeri generati dai figli vengono inviati al processo padre che provvede a sommarli e stamparli su schermo e a memorizzarli in un file.
> L’esecuzione di tutti e tre i processi viene rimandata dal processo padre quando verifica che la 
> somma dei numeri avuti dai processi figli assume il valore 100, altrimenti mette in attesa per 2 
> secondi prima di controllare i due numeri inviati dai processi figli.

```c
#include<unistd.h>

#include<stdlib.h>

#include<stdio.h>

#include<fcntl.h>

#include<time.h>

#include<signal.h>

#include<string.h>

void handler_SIGINT()

{

    printf("interruttione ditabilitata \n");

    exit(0);

}

int main(int argc, char **argv)

{

    signal(SIGINT,handler_SIGINT);

    srand(time(NULL));

    int num=0;

    pid_t p1,p2;

    int fd1[2],fd2[2];

    if(pipe(fd1)==-1 || pipe(fd2)==-1)

    {

        perror("errore nella pipe");

        exit(1);

    }

    p1=fork();

    if(p1==-1)

    {

        fflush(stdout);

        printf("errore di creazione fork");

        exit(1);

    }

    if(p1==0)

    {

        close(fd1[0]);

        close(fd2[1]);

        close(fd2[0]);

        while(1)

        {

            num=rand()%101;

            write(fd1[1],&num,sizeof(int));

            fflush(stdout);

            printf("sono il p1 e ho tampato quetto numero %d \n",num);

            sleep(1);

        }

    }

    if(p1>0)

    {

        p2=fork();

        if(p2==-1)

        {

            printf("errore");

            exit(1);

        }

        if(p2==0)

        {

            close(fd1[0]);

            close(fd1[1]);

            close(fd2[0]);

            while(1)

            {

                num=rand()%101;

                write(fd2[1],&num,sizeof(int));

                fflush(stdout);

                printf("sono il p2 e ho tampato quetto numero %d \n",num);

                sleep(1);

            }

        }

    }

    if(p1>0 && p2>0)

    {

        int file=open("test.txt",O_RDWR|O_CREAT|O_TRUNC,0644);

        close(fd1[1]);

        close(fd2[1]);

        int num1=0,num2=0,somma=0;

        char buffer[50];

        while(1)

        {

            read(fd1[0],&num1,sizeof(int));

            read(fd2[0],&num2,sizeof(int));

            fflush(stdout);

            somma=num1+num2;

            printf("la somma dei numeri %d + %d è %d \n",num1,num2,somma);

            sprintf(buffer,"%d %d\n",num1,num2);

            write(file,buffer,strlen(buffer));

            if(somma>100)

            {

                fflush(stdout);

                printf("numero trovato %d \n",somma);

                kill(p1,SIGTERM);

                kill(p2,SIGTERM);

                break;

            }

            else sleep(2);

        }

    }

    return 0;

}
```

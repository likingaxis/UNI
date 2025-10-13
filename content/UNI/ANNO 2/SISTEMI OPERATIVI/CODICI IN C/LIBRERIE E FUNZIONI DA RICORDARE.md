#### LISTA DI LIBRERIE
### `stdio.h`(da includere sempre)
le solite funzioni PRINTF,SCANF ecc...
- fflush
- fprintf
### `stdlib.h`
- rand
- srand
- malloc
- free
- exit
### `unistd.h`
- pipe
- fork
- close
- write
- read
- ssize_t tipo di dato
- sleep
- dup
- execl
### `sys/types.h`
- pid_t
### `time.h`
- time
### `signal.h`
- signal
- kill
- alarm
- strsignal
### `sys/wait.h`
- wait
- waitpid
### `fcntl.h`
- open
- creat
macro:
- `O_RDONLY`: Apertura in sola lettura.
- `O_WRONLY`: Apertura in sola scrittura.
- `O_RDWR`: Lettura e scrittura.
- `O_CREAT`: Crea il file se non esiste.
### `semaphore.h`
- sem_t come tipo di dato
- sem_init
- sem_destroy
- sem_wait
- sem_post
### `pthread.h`
- pthread_t come tipo di dato
- pthread_mutex_t come tipo di dato
- pthread_create
- pthread_join
- pthread_mutex_init
- pthread_mutex_lock
- pthread_mutex_unlock
- pthread_mutex_destroy
- pthread_cond_init
- pthread_cond_wait
- pthread_cond_signal
- pthread_cond_destroy
- pthread_exit
### `string.h`
- strlen

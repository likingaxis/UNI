`int fd[2]`
`pipe(fd)`
`close(fd[0])`
`int p=fd[0]`
la pipe è FIFO
`int tmp1=3`
`write(fd[1],&tmp1,sizeof(int))`
la write è divisa in
- path
- indirizzo del dato che vogliamo scrivere
- dimensione dei byte da scrivere


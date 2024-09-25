# SCHEMA RAPIDO
![[Pasted image 20240918144831.png|400]]
## DIM COMPLETA
### sia $f(x):[a,b]->R$
#### Come deve essere $f(x)$ ?
- CONTINUA
- CON $f(a)*f(b)<0$ QUINDI CON SEGNI DIVERSI

#### ALLORA $\exists{x_0}\in (a,b) t.c. f(x_0)=0$

#### costruisco due successioni 
{$a_n$}$_n$ e {$b_n$}$_n$ 
e ho $C_n=\frac{a_n+b_n}{2}$= punto medio di $(a,n)$
#### ABBIAMO 3 CASI
1) abbiamo $f(C_n)=0$ abbiamo trovato la nostra $x_0$
2) $C_n>0$ dobbiamo shiftare $b_n$ verso sx quindi diremo che $b_{n+1}=C_n$ e che $a_{n+1}=a_n$
3) $C_n<0$ dobbiamo shiftare $a_n$ verso dx quindi diremo che $b_{n+1}=b_n$ e che $a_{n+1}=C_n$
> [!info]- esempio del numero 3
>![[Screenshot_2024-09-18-15-20-10-05_45415775811cea13943236d9369df411.jpg|600]]

#### COSA SUCCEDE SE NON SI VERIFICA IL PUNTO 1?
allora $\forall{N}\in{n}$
$an\leq{a_{n+1}}<b$
$bn\geq{b_{n+1}}>a_n$
sia $a_n$ che $b_n$ convergono
$\lim_{x\to\infty} a_n=A$
$\lim_{x\to\infty} b_n=B$
e al passo n-esimo viene diviso il tutto n volte quindi avremmo
$B-A<=b_n-a_n<=\frac{b_n-a_n}{2^n}=0$
quindi abbiamo che $f(x)$ è continua in $x0\in [a,b]$
e per verificare che $f(x_0)=0$ uso doppio confronto
$a_n\to x_0$ $f(a_n)\to f(x_0)\leq0$
$a_n$ decresce e quindi per la permanenza del segno il limite è minore uguale a 0
$b_n\to x_0$ $f(b_n)\to f(x_0)\geq0$
quindi per doppio confronto $f(x_0)=0$

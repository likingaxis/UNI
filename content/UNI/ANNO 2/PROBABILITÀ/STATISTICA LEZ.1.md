# introduzione
Fenomeno aleatorio ovvero un fenomeno con esito incerto e si indica con $\Omega$
- discreto se omega è finito  {${1,2,3,...,6}$}  o numerabile {${1,2,3,...}$}
- continuo se omega è più che numerabile da {$0,\infty$}
Una famiglia di eventi $A$ fa parte di una famiglia di sottoinsiemi di $\Omega$
>[!example]-
> esce un numero pari {2,4,6} c {1,2,3,4,5,6}

## Operazioni logiche tra eventi
|              Operazione | tipo           |
| ----------------------: | :------------- |
|            Somma logica | $A\cup B$      |
|         Prodotto logico | $A\cap B$      |
| Negazione$\overline{A}$ | $A^c=\Omega*A$ |
### Definizione di $\sigma$ algebra
Sia $\Omega$ un insieme non vuoto che ha $A c P($$\omega$)
Allora $A$ è una $\sigma$ algebra di eventi se:
1. R $\in$ ad A
2. $every A\in A$  significa che $A^c \in A$
3. $\forall$ {$an$}$_n\geq 1$ c $A$ -> U $n\geq1$ {$an$} $\in A$
### Definizione di misura di probabilità
Sia $\Omega$ un insieme non vuoto e $A$ una $\sigma$ algebra di eventi
Allora una funzione $P:A->[0,\infty)$ è una misura di probabilità 
Se 
1. P($\Omega$) =1
2. $\forall$ {$A_n$}$_{n\geq1}$ c $A$ tale che $A_m \cap A_n \neq 0$ per $m\neq n$ ovvero disgiunti due a due
![[Pasted image 20241001112312.png|350]]
La terna ($\Omega,A,P$)si chiama *spazio di probabilità
Teniamo a mente che $P(0)=0$

### Formula per l'unione degli eventi
$P(E\cup F)=P(E)+P(F)-P(E\cap F)$
$P(E\cup F\cup G)=P(E)+P(F)+P(G)-P(E\cap F)-P(E\cap G)-P(F\cap G)+P(E\cap F \cap G)$
### Spazio di probabilità uniforme discreto
- $\Omega$ = insieme finito 
- A=P($\Omega$)
- $\forall A \in \Omega$
$P(A)=\frac{\# A}{\# \Omega}$=$\frac{\# A}{n}$
Si usa con estrazioni a caso di n oggetti
Si usa ad esempio nel caso di un lancio del dado con $n=6$ e $\Omega$ ={$1,2,3,4,5,6$}
### Definizione probabilità condizionata
Sia $(\Omega,A,P)$ uno spazio di probabilità e si definisce probabilità condizionata di A dato B
$P(A|B)$ = $\frac{P(A\cap B)}{P(B)}$=$\frac{\#(A\cap B)/n}{\# B/n}$=$\frac{\#(A\cap B)}{\#(B)}$ $\forall A \in A$
# ESEMPIO
Un'urna ha 10 palline numerate da 1 a 10
Si estrae una pallina a caso
1. Calcolare la probabilità di estrarre un numero maggiore di 5 sapendo che e' stato estratto un numero pari
2. Calcolare la stessa probabilità nel caso in cui vengano aggiunte due palline una con il numero 1 e una con il numero 10
Abbiamo che $A=\{6,7,8,9,10\}$ e $B=\{2,4,6,8,10\}$ quindi $A\cap B$=$\{6,8,10\}$
###### Parte 1
$P(A|B)=$ $\frac{\#(A \cap B)}{\#B}$ =$\frac{3}{5}$
###### Parte 2
$P(A|B)=\frac{P(A\cap B)}{P(B)}$ = $\frac{(1+1+2)/12}{(1+1+1+1+2)/12}$=$\frac{4}{6}$

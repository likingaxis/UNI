[[Cap1.pdf|PDF rispettivo della lezione]]
$$
F_n = \begin{cases}
    F_{n-1}+F_{n-2} & \text{se } n \geq 3 \\
    1 & \text{se } n = 1,2
\end{cases}
$$
## ALGORITMI DI FIBONACCI CON PSEUDO-CODICE
### ALGORITMO 1
Algoritmo di Fibonacci1 con le $\phi$ viene usato ma ha un problema di approssimazione ed è il seguente:
$$
F_n=\frac{1}{\sqrt{5}}*(\phi^n-\phi_2^n)
$$
$$ dove\ \  \phi=1,618 \ \ e \ \ \phi_2=-0,618
$$
##### PSEUDO CODICE
![[Pasted image 20241009153708.jpg|450]]

### Algoritmo2
lo troviamo con pseudo codice

![[Pasted image 20241009153904.jpg|400]]

sfruttando uno divide and conquer

Per calcolare il costo computazionale del Fibonacci2 
calcoliamo il numero di linee di codice mandate in esecuzione al variare di n
Usiamo T(n) ovvero $\#$ di linee di codice eseguite nel caso peggiore su un input n
E avremo che $T(n)=2+T(n-1)+T(n-2) \ \ T(1)=T(2)=1$
#### Per creare una formula generica usiamo l'albero della ricorsione
![[Pasted image 20241009155632.jpg]]
Ogni nodo superiore fa i passi delle foglie (basi)sotto l'albero
F(4) ha 3 foglie e 2 nodi interni
Ogni foglia 1 linea di codice ogni nodo interno 2 linee di codice
Creo due supposizioni
- Lemma1 il numero di foglie dell'albero è $F_n$
- Lemma2 il numero di nodi interni è $\# Foglie-1$

$F_n+2(F_n-1)=3F_n-2$
Dimostrazione sui lemmi(ipotesi)(slide 18)
L'algoritmo di Fibonacci2 fa cagare perché piu' volte ricalcola le stesse cose tipo F(6), rifaccio le stesse computazioni
### Algoritmo3
Usando un Array ausiliario in posizione i metto il risultato di quel Fibonacci
![[Pasted image 20241009164625.jpg|400]]
Contare le linee di codice
$T(n)\leq n+n+3=2n+3$
Fib3 es mejor than Fib2
### Occupazione della memoria
Fibonacci3 usa abbastanza memoria perciò useremo Fibonacci4 che dovrà usare meno memoria
### Algoritmo4
Pseudo codice Fibonacci4 
![[Pasted image 20241009165440.jpg|400]]
Possiamo dimenticare tutti i precedenti senza usare l'array risparmiando cosi' memoria ausiliaria usando memoria costante
Tempo di Fibonacci4 $4n+2$ ma solo perchè contiamo le linee di codice e quindi è un po' approssimato
## Notazione asintotica
Esprimo il costo $T(n)$ in modo qualitativo 
- ignoro costanti moltiplicative
- ignoro termini di ordine inferiore
Quindi sia Fibonacci4 che 3 sono $O(n)$

#### Matrici=Fibonacci
![[Pasted image 20250505094900.png]]
![[Pasted image 20250505094922.png]]

### Algoritmo5
Con matrici e induzione slide
Pseudo codice
![[Pasted image 20241009175301.jpg|400]]
Sarà sempre $O(n)$
### Algoritmo6
Vedi proprietà delle somme degli esponenti che permette di scomporre in sotto problemi ad esempio $3^8=3*3*3*3*3*3*3*3=((3^2)^2)^2$
sostanzialmente dimezzo la potenza perché tanto da stessi risultati
$a^n=(a^{n/2})^2$
Posso sfruttare questa cosa per diminuire la potenza senza fare tutte le moltiplicazioni
![[Pasted image 20241009183110.jpg|400]]
Per capire il costo computazionale di questo algoritmo bisogna fare degli accorgimenti arrivando al caso $log_2n$ 
$T(n)\leq c*parte \ intera \ log_2n+T(1)=O(log_2n)$
>[!info]- spiegazione raffazzonata sulla ricorsione
>![[Pasted image 20241009192241.png]]
### Quanta memoria usa un algoritmo ricorsivo?
- Algoritmo non ricorsivo: dipende dalla memoria (ausiliaria) allocata; es. variabili, array...
- Algoritmo ricorsivo: dipende dalla memoria (ausiliaria) allocata da ogni chiamata e dal numero di chiamate che sono contemporaneamente attive.quindi In base all'espansione dei nodi

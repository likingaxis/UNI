Quando si inizializza una macchina di Turing 
si definisce una quintupla con
![[Pasted image 20250314154218.jpg]]
Dagli ultimi 3 possiamo definire subito una macchina di turing
Definiremo esattamente $P$ con una funzione di transizione
![[Pasted image 20250314154351.jpg]]
Se di questo insieme $\delta$  non abbiamo delle azioni definite ad esempio $\delta(q,s)=insieme vuoto$
allora significa che la macchina starà ferma
##### Con i TRASDUTTORI
ovvero quelli che lavorano con un alfabeto ampio e output
Quando non abbiamo una istruzione possono crearsi dei problemi e non basta fermare la macchina quindi possiamo
- creare una Funzione totale con tutte le istruzioni possibili
- sono cavoli di chi usa l'input che non deve mettere roba sbagliata
##### Con i RICONOSCITORI
Con i riconoscitori abbiamo lo stesso problema ma dobbiamo definire bene gli stati perchè lo stato di rigetto non può essere usato come stato di errore di computazione quindi in questo caso dobbiamo definire un errore in scrittura come E oppure rendiamo la procedura in modo che dia un unico output corretto e tutti gli altri sono l'opposto
Anzichè scrivere pari o dispari qa qr scrivo pari oppure tutto il resto
### E se P non corrisponde a una sola funzione?
mettiamo caso di avere P che corrisponde a più funzioni avremo quindi definito una funzione di transizione di tipo multiplo
![[Pasted image 20250314163234.jpg]]
a delle condizioni corrispondono più funzioni quando tu hai un insieme A e fai $2^A$ ottieni tutti i sottoinsiemi con A
non possiamo avere due quintuple perchè la Macchina di Turing non saprebbe cosa scegliere 
$\langle q, a, b_1, q_1, m_1 \rangle, \langle q, a, b_2, q_2, m_2 \rangle, \dots, \langle q, a, b_k, q_k, m_k \rangle$
chiamiamo così questa struttura multi-quintupla
le multi quintuple vengono gestite da macchine non deterministiche 
il grado di non determinismo di una singola funzione transitoria è dato da 
![[Pasted image 20250314165744.jpg]]
invece il grado di non determinismo di tutte le funzioni transitorie di una macchina sono date da 
![[Pasted image 20250314165845.jpg]]
Il comportamento di T di una macchina non deterministica  può fare in due modi (equivalenti) quando ci si presenta una multi quintupla.
Le macchine non deterministiche sono definite con $NT$
TUTTE QUESTE DUE MACCHINE SI BASANO SU RICONOSCITORI
### 1. Macchina super iper ultra parallela o la coda di rondine con ripetizioni
Esegue tutte le k quintuple in modo parallelo si moltiplica tutto per ogni stato globale che si va a creare, se poi da una quintupla si creano altri sotto stati globali con altre quintuple si crea una sorta di albero dove ciasciun ramo(percorso) è una computazione deterministica
![[Pasted image 20250314170404.jpg]]
ora però date tutte queste istanze, come faccio a definire quale di questi esiti considerare? 
teniamo in considerazione lo stato globale in cui arriviamo a un qa
l'importante è che ce ne sia almeno 1 sennò significa rigetto
![[Pasted image 20250314172337.jpg]]

### 2. Intervento del genio burlone e pasticcione

In questo caso colui che sceglie il singolo percorso di stati globali è un genio
sceglie quali quintuple eseguire
Quando questa non rigetta?
la situazione è analoga alla macchina super iper ultra parallela
solo che adesso ci saranno più geni a scegliere

### Da macchina non deterministica a deterministica
posso dire che abbiamo una macchina T che simula la macchina NT nelle istanze in cui rigetta oppure accetta, se NT alla fine accetta allora anche T accetta se NT rigetta allora T rigetta
![[Pasted image 20250314173905.jpg]]
Prima le prova fino al livello 1 se non trova qa oppure tutte che rigettano scende al livello 2
![[Pasted image 20250314174317.jpg]]

#### Perchè lavorare con 1...i livelli di volta in volta?
perché possiamo avere un path che non termina mai e rimanere in un loop senza svolgere quello che termina se lavoriamo su livelli vediamo un po di tutti i percorsi
![[Pasted image 20250314175245.jpg]]
la scorsa lezione abbiamo visto il teorema 3.5
oggi vedremo il contro esempio con il teorema 3.6
che dice:
Per ogni macchina di Turing deterministica $T$ di tipo riconoscitore ad un nastro esiste un programma $AT$ scritto in accordo alle regole del linguaggio PascalMinimo tale che: per ogni parola $x$, se $T(x)$ termina nello stato finale $qF ∈ {qA,qR}$ allora l’esecuzione di $AT$ con input $x$ restituisce $q_F$ in output e se l’esecuzione di $AT$ con input $x$ restituisce $q_A$ in output allora $T(x)$ termina nello stato finale $q_A$
### Per dimostrarlo ci serve una macchina di Turing Universale
Utilizzeremo una macchina di Turing Universale per poi convertirla in un programma $U$ in PascalMinimo

$U$ che deve avere come input: 
- una descrizione $D$
	- il codice della macchina di Turing
- una T $\in$ $\vartheta$ $\wedge$ x $\in$ $\{0,1\}^*$ 
La nostra macchina T sarà invece definita da $<Q_1,S_1,S_2,Q_2,M>$

quindi avremo una cosa tale che l’esecuzione di $U$ con input la <font color="#c0504d">descrizione</font> di una macchina di Turing T e un input x per T simula la computazione $U(T,x)$

Avrò un insieme di quintuple $P$
Quello che faccio è dare un numero ad ogni quintupla dell'insieme P per tenerle ordinate

Ora la quintupla $H-esima$ sarà ad esempio formata da $<q_{h1},S_{h1},q_{h2},m_h>$
Definisco le prime P e mi accorgo che se le divido in strati posso creare degli array 
![[Screenshot_2025-03-27-19-11-25-10_45415775811cea13943236d9369df411.jpg|500]]
ad esempio posso avere la prima fetta che è un array di tutti gli stati iniziali
posso quindi fare $Q_1[h]$ e giungere alla posizione di quel determinato stato iniziale di quella determinata quintupla
quindi avrò
- Q1
- S1
- S2
- Q2
- M

Quindi al nostro programma U passiamo tutti gli array, in input avremo:
`Q1[],S1[],S2[],Q2[],M[]`

Ora abbiamo definito la struttura ma mancano i nastri
essi saranno un array
ogni cella del nastro rappresenta un elemento dell'array
Per far partire una macchina di Turing dobbiamo definire
- la testina t<-1
- lo stato di inizio q<-q0
- abbiamo dei delimitatori del nastro di input $pc$<-1 $uc$<-n 
	- che stanno per prima cella e ultima cella

Una macchina universale ha il compito di trovare la quintupla e eseguirla
quindi per farlo in Pascal minimo abbiamo l'obbligo di creare un while che terminerà quando si finirà negli stati $q_A$ o $q_R$ 
### Descrizione dell'input:
In input viene fornita la descrizione di T
- (negli array $Q1, S1, S2, Q2$ e $M$ e nelle variabili $q0, qA \ e \ qR$) 
- e del suo input (nell’array N)
![[Pasted image 20250327192246.png]]

### Codice

```pascal
t <- 1;   // variabile in cui memorizzo la posizione della testina (inizialmente 1)
q <- q_0;   // variabile in cui memorizziamo lo stato interno (inizialmente q_0)

primaCella <- 1; 
ultimaCella <- n;  // inizio e fine del nastro di input

// la macchina universale cercava le quintuple e le eseguiva ciclicamente, quindi la riproduco col while
while(q != q_a AND q != q_r) do begin //<- qui fa quello che dicevo prima
    j <- 1;
    trovata <- false;
    while (trovata = false AND j <= k) do   // k è il numero di quintuple
        if (q = Q_1[i] AND N[t] = S_1[j]) then 
            trovata <- true;
        else j <- j+1;
    end                   //<- in questo ciclo che finisce qui cerchiamo 
						  //la quintupla da eseguire
    if (trovata = vero) then begin   //<- quintupla trovata
        N[t] <- S_2[j];
        q <- Q_2[j];
        t <- t+M[j];
        
    // pc/uc (lo usa la prof per non riscrivere tutte queste righe sotto)
        if (t < primaCella) then begin   //<- leggi il commento * sotto
            primaCella <- t;
            N[t] <- [];
        end
        if (t < ultimaCella) then begin
            ultimaCella <- t;
            N[t] <- [];
        end
    end
    else q <- q_r;
end
Output: q;

```

Commento $"*"$
in caso di scrittura si potrebbe andare a sinistra o a destra degli elementi dell'array e quindi "uscire" dalle celle definite nel nastro, visto che il nastro è infinito dobbiamo posizionare dei blank al posto delle celle vuote nel nastro facendo $N[t]=\square$ 
 
 
# Come simulare una macchina non deterministica attraverso un algoritmo in PascalMinimo
Questo algoritmo simula la coda di rondine con ripetizioni che si trova a [[FONDAMENTI LEZ.5#1. Macchina super iper ultra parallela o la coda di rondine con ripetizioni|qui]]
La chiamiamo $U_{ND}$ , esso avrà i seguenti dettagli:
- un contatore i inizializzato a 1
- simula tutte le computazioni deterministiche di $i$ istruzioni
	- se una di esse accetta, allora accetta
	- altrimenti; se tutte rigettano, allora rigetta
- se non fa nulla delle due incrementa $i$
#### Codice in PascalMinimo
![[Pasted image 20250327195044.png]]
#### Schema di come funziona la Ricorsione
![[Pasted image 20250327195114.png]]

# Codice pazzurdo da NON ricordare
![[Pasted image 20250327195151.png]]
# Cosa bisogna ricordare?
- ESISTONO LE FUNZIONI RICORSIVE IN PascalMinimo
- ESISTONO LE FUNZIONI IN PascalMinimo
	- le funzioni sono praticamente le simulazioni delle macchine di Turing

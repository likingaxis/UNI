## Concetto di Linguaggio
Un linguaggio L è un insieme di parole x $\in$ $\Sigma$  come ${0,1}$ che hanno una certa proprietà con $i$ infatti si può definire che $L ⊆ Σ^*$ 

Possiamo dire che un linguaggio L è <font color="#f79646">deciso</font> da una macchina di Turing $T$ se  
- per ogni $x ∈ L$, la computazione $T(x)$ termina in $q_A$ 
- per ogni $x ∉ L$, la computazione $T(x)$ termina in $q_R$
#### Esempio Linguaggio di una macchina $T_{RPPAL}$
![[Pasted image 20250319184614.png]]
Ebbene, TRPPAL decide il linguaggio LPPAL (Pari e PALindrome) seguente: $$L_{PPAL} = { x_1x_2… x_{2n} ∈\{a,b\}^*: n ∈ ℕ ∧ ∀ i ∈ {1, 2, ... , n} [ x_i = x_{2n-i+1} ] }$$
$x_{2n}$ con 2 perché indica che l'ultima parola deve essere pari

Il problema qui è che con certezza possiamo dire che se x appartiene a L allora termina e termina in $q_A$ 
ma, se x non appartiene ad L, non è detto che T(x) termini in $q_R$ potrebbe anche non terminare
- quindi non posso dire con certezza che nella computazione di quella parola essa non appartenga a L
![[Pasted image 20250319190506.png]]
Qui vediamo  $T_{pal}$ che nel caso in cui  la parola sia palindroma ma dispari e al centro abbia 'a' la macchina non termina e va in loop<font color="#00b0f0">(vedi la quintupla azzurra)</font>

Possiamo dire che $T_{pal1}$ accetta il linguaggio $L_{ppal}$  
dove semplicemente se il linguaggio viene riconosciuto esso viene accettato ma se non viene riconosciuto potrebbe andare in rigetto
- grazie alla modifica qui abbiamo un loop che lo rende accettabile e non decidibile
### Def 1 Decidibile
![[Pasted image 20250319192124.png]]
### Def 2 Accettabili
![[Pasted image 20250319192138.png]]
#### La differenza tra le due
nella prima def abbiamo dato un rigetto se non è nel linguaggio invece nella def 2 sicuramente non accetta ma non è certo che rigetti

se L è decidibile allora è anche accettabile ma non il contrario
### Linguaggio complemento $L^C$
Il linguaggio complemento ci viene in aiuto quando stiamo lavorando su una macchina che lavora su un insieme $\Sigma$ definito e che non sa come comportarsi se ci troviamo al di fuori di esso ad esempio una parola in $\Sigma^*-L$ 
definiamo perciò
![[Pasted image 20250319193429.png]]
### Def 3.1
>[!lemma] $L$ $\subseteq$ $\Sigma^*$ è decidibile $\iff$ $L$ è accettabile $\land$ $L^{C}$ è accettabile.

 ($\Rightarrow$) Se $L$ è decidibile allora

- $\exists \ T$ che decide $L$ 
- $\Rightarrow$ $T$ accetta $L$ ( abbiamo visto che DECIDIBILI $\subseteq$ ACCETTABILI)
- Dobbiamo costruire una $T^{C}$ che accetta $L^{C}$, e lo facciamo prendendo $T$ e INVERTENDO i suoi stati di accettazione e rigetto
    - $T^{C} = <\Sigma, \Omega, \omega_{0}, {\omega_{A}, \omega_{R}}, P^C>$_
        - _$\Omega = {\omega_{0}, \omega_{A}, \omega_{R}, q_{A}, q_{R}}$
        FASE 1) dallo stato $\omega_0$ simula $T(x)$ (e quindi può finire o in $q_{A}$ o in $q_{R}$) 
        FASE 2) se $o_{T}(x) = q_{A} \Rightarrow o_{T^{C}}(x) = \omega_{R}$ se $o_{T}(x) = q_{R} \Rightarrow o_{T^{C}}(x) = \omega_{A}$
    

($\Leftarrow$) Se $L$ è accettabile e $L^C$ è accettabile allora

- Prendiamo le macchine $T$ che accetta $L$ e $T^{C}$ che accetta $L^C$.

- Dobbiamo costruire una macchina $\overline{T}$ che DECIDE $L$, e per farlo la dotiamo di due nastri e
    
    - N1 -> simula $T$
    - N2 -> simula $T^{C}$
    - INPUT scritto inizialmente su N1
        
INIZIALIZZAZIONE) $T$ copia `x` su N2 

FASE 1) $T$ simula un'istruzione (un passo) di $T(x)$ su N1 SE porta in $q_{A}$ $\Rightarrow$ **accetta** ALTRIMENTI _fase 2)* 

FASE 2) $T$ simula un'istruzione di $T^{C}$ su N2 SE porta in $q_{R}$ $\Rightarrow$ rigetta ALTRIMENTI fase 1)  

Visto che stiamo coprendo entrambi i casi, $x \in L$ e $x \notin L$, allora prima o poi $T_{1}$ o $T_{2}$ accettano e quindi $T$ DECIDE $L$. 
>[!question] Possiamo simulare PRIMA TUTTO UN NASTRO? 
>No, perché se un'istruzione va in loop allora non avremo mai un output. 
>Ricorda che passiamo da FASE 1 a FASE 2 (e viceversa) SOLO se non otteniamo $q_{A}$ (il loop credo sia consentito se lavoriamo passo-passo).

se chiamiamo con D l'insieme dei linguaggi decidibile possiamo dire che D sottoinsieme A(linguaggi accettabili)

### ESERCIZI
![[Pasted image 20250319205027.png|500]]
# Trasduttori
I trasduttori ricordiamo che sono quelle macchine di Turing che hanno un solo nastro di output e che terminano in uno stato $Q_f$ vengono usati per svolgere funzioni
il problema è quando una funzione non ha soluzioni tipo
$f(n)=\frac{1}{n-4}$
Per calcolo di funzione intanto definiamo così la cosa
considerando funzioni ”discrete” – ossia, dati due alfabeti finiti Σ1 e Σ2, noi consideriamo funzioni:
$$f : Σ1* → Σ2^*$$  
- ossia, funzioni che trasformano parole in altre parole
visto che questa funzione con $n=4$ non si può svolgere noi dividiamo le funzioni calcolabili in 2 tipi
1) funzione classica dove calcoliamo nei punti definiti
2) funzione TOTALE che sono definite per ogni x ∈ Σ1*
##### piccola definizione
![[Pasted image 20250319205941.png]]
T(X)=f(X) si può scrivere anche come $oT(x)=f(x)$

Qui definiamo il caso in cui x è definita ma come per quanto riguarda i casi in cui non è accettabile non abbiamo definito il caso in cui bisogna calcolare una x non definita
### funzione caratteristica
![[Pasted image 20250319210621.png]]
dove quella x in realtà si chiama $\chi$ chi

### Teorema 3.2
bho sta sulle dispense dice che una macchina $\chi_L$ deve per forza avere un linguaggio $L$ decidibile
### Due alfabeti che mi portano a una incognita risultato
![[Pasted image 20250319211945.png]]
### Teorema 3.3
![[Pasted image 20250319212052.png]]
### Teorema 3.4
Una _funzione calcolabile_ è una funzione che può essere calcolata da una **macchina di Turing con output** (cioè una macchina che scrive un risultato su un nastro e termina la computazione).

In pratica, immaginiamo che la funzione trasformi parole in altre parole. Per esempio:

- Se la funzione è: `f(n) = n²`, e inseriamo `n = 5`, il risultato sarà `25`.
- Ma se la funzione non è definita per certi valori (come √n se n è negativo), allora **non possiamo calcolare quel valore**.

➡️ Diciamo quindi che una funzione è calcolabile **se esiste una macchina di Turing che, ogni volta che la funzione è definita, riesce a scrivere il risultato corretto e fermarsi**.

Ogni linguaggio (cioè insieme di parole) può essere collegato a una funzione chiamata **funzione caratteristica**:

- Questa funzione vale **1** se la parola appartiene al linguaggio.
- Vale **0** se la parola non appartiene.

💡 Ecco il punto importante:

> **Una funzione caratteristica è calcolabile se e solo se il linguaggio è decidibile.**

Cosa vuol dire?  
Che possiamo costruire una macchina di Turing capace di **dirci sempre sì o no** per ogni parola, se questa appartiene al linguaggio.

Anche per una funzione `f(x)` possiamo costruire un **linguaggio associato** che contiene tutte le coppie `(x, y)` tali che `y = f(x)`.

Questo linguaggio è come il **grafico** della funzione.

📌 Se `f` è calcolabile e totale (cioè definita ovunque), allora questo linguaggio è **decidibile**.  
Cioè possiamo costruire una macchina che, data una coppia `(x, y)`, sa sempre dirci se `y` è il risultato di `f(x)` oppure no.
Delle lezioni precedenti mancano ancora delle cose da precisare
- delle classi di complessità non deterministiche
	- non sappiamo quanto tempo o spazio serve per rigettare le parole che non appartengono al linguaggio
	- sappiamo però che se fissiamo una quantità massima allora possiamo dire che il linguaggio è sia accettabile che decidibile
- poi abbiamo detto che se viene deciso da una macchina non deterministica
	- allora è deciso anche da una macchina deterministica
	- ma non sappiamo a quale classe di complessità collocare un linguaggio che appartiene a un certo `NTIME[f(n)]`
	- e oltretutto non sappiamo dire se dato un certo `NTIME[f(n)]` allora esso sarà uguale a quel determinato `DTIME[qualche altra funzione]`

## La prima questione aperta
##### 🧠 **Contesto**
- Hai un linguaggio $L \in \text{NTIME}$
	- Questo significa: esiste una macchina non deterministica che, **se una parola $x \in L$**, **la accetta** in tempo $O(f(|x|))$
✔️ **Per le parole nel linguaggio**, sappiamo che **esiste un ramo accettante veloce**.
##### ❗ Il problema
- **Per le parole $x \notin L$**:
    - Non c'è nessun ramo che accetta,
    - Ma **non sappiamo quanto tempo serve per rigettare**, perché bisogna **esplorare tutti i rami** (o, almeno, assicurarsi che _nessuno_ accetti).

> In altre parole: sappiamo che la macchina rigetta, ma **non sappiamo quanto tempo ci mette per concludere che “nessun ramo accetta”**.

#### Teorema 6.16 per risolvere
>[!tip] Teorema 6.16
>![[Pasted image 20250430194713.png]]

- come sempre andiamo a dimostrare solo nel tempo perché lo spazio è analogo
	- solo che avrà al posto delle istruzioni le celle e tutte le cose con space

Questo teorema dice
- se `f` è <font color="#f79646">time-constructible</font> e $L$ è in $NTIME[f(n)]$, allora una modifica della macchina $NT$ **che accetta le parole `x` di L eseguendo $O(f(|x|))$ istruzioni** è anche capace di rigettare le parole **non in $L$** eseguendo **O(f(|x|))** istruzioni;
Per dimostrarlo, ci avvaliamo del [[FONDAMENTI LEZ.21#Teorema 6.2|teorema 6.2]] molto simile
![[Pasted image 20250430195159.png]]

La dimostrazione è divisa in 2 parti
##### Parte 1
il problema di questo teorema è che abbiamo quella $O$ che rende il tutto molto "grigio" 
ma sostanzialmente essa ci serve per dire che 
- il linguaggio viene accettato in tempo $f(n)$ per una costante

Sia $NT$ la macchina che accetta L, tale che $$ntime(NT, x) \le c \cdot f(|x|)$$e, poiché f è <font color="#f79646">time-constructible</font>, allora anche $c \cdot f$ è <font color="#f79646">time-constructible</font>: allora esiste una macchina $T_{f}$ di tipo trasduttore che, per ogni $n \in ℕ$ , 
- $T_{f}(1^{n})$ termina
	- con il valore $c \cdot f(n)$ scritto sul nastro di output
	- dopo aver eseguito $O(c \cdot f(n))$ istruzioni

ora abbiamo definito che anche con $O$ rimane time-constructible
##### Parte 2
Costruiamo una nuova macchina non deterministica $\text{NT}'$, a tre nastri, che decide L.
Per ogni $x \in \Sigma^{*}$
- **Scrive** $|x|$ in unario su un secondo nastro e invoca la macchina $T_f$​ che calcola $c \cdot f(|x|)$, e lo scrive in unario su un terzo nastro.
- Poi invoca $\text{NT}(x)$ per **simulare tutte le computazioni non deterministiche**.
- Ogni volta che un ramo di $NT(x)$ esegue un passo, $\text{NT}'$ controlla che il contatore (terzo nastro) non sia esaurito.
    - Se c’è ancora un ‘1’, lo toglie e continua.
    - Se termina il tempo, rigetta.
- Alla fine accetta se $NT(x)$ accetta entro il limite, altrimenti rigetta.
##### 📌 Perché funziona?
- Per $x \in L$, esiste un ramo accettante in $\leq c \cdot f(|x|)$ passi → $\text{NT}'$ lo troverà e accetterà.
    
- Per $x \notin L$, 
	- ogni ramo rifiuta entro il tempo limite →$\text{NT}'$ li esaminerà e rigetterà
	- oppure finirà il tempo senza trovare un'accettazione → rigetta.

Quindi le computazioni su $\text{NT}'$ TERMINANO SEMPRE e, per questi ultimi due punti, possiamo affermare che $\text{NT}'$ DECIDE $L$.
##### ⏱️ **Quanto tempo usa NT’?**
- Per calcolare $f(∣x∣)$ (in unario): serve $O(f(∣x∣))$ tempo, perché $f$ è <font color="#f79646">time-constructible</font>.
- Per simulare tutte le computazioni entro $c \cdot f(|x|)$ passi: $O(f(∣x∣))$
✅ Totale: $O(f(∣x∣))$

>[!tip] Per questo possiamo concludere che $L$ è decidibile, in tempo non deterministico $O(f(n))$

## Seconda questione aperta
#### 🔍 **Punto di partenza**
Le **uniche relazioni sicure** che conosciamo finora tra classi **deterministiche** e **non deterministiche** sono le seguenti:
```
DTIME[f(n)] ⊆ NTIME[f(n)]
DSPACE[f(n)] ⊆ NSPACE[f(n)]
```
Queste derivano da un fatto banale:
> ogni macchina deterministica è un **caso particolare** di macchina non deterministica (cioè con un solo ramo).

✅ **E sappiamo anche che**:
> Tutto ciò che è **decidibile da una macchina non deterministica** è anche **decidibile da una deterministica** (concettualmente parlando).

#### ❗MA...il vero problema
Supponiamo di avere un linguaggio $$L \in NTIME[f(n)]$$cioè: esiste una macchina NON deterministica che lo decide in tempo $f(n)$
>[!bug] In questo caso non sappiamo dire
>- in quale **classe deterministica** si trova $L$
>- se c'è una funzione $g(n)$ tale che `L ∈ DTIME[g(n)]`
>- e non sappiamo quanto più grande debba essere $g(n)$ rispetto a $f(n)$

🎯 In parole semplici:
> **Sappiamo che una macchina deterministica può risolvere tutto ciò che una non deterministica può**,  
> **ma non sappiamo quanto tempo le serve per farlo.**
> a meno che la funzione limite f della classe non sia una funzione time-constructible…

#### Teorema 6.17
>[!tip] Teorema 2
>![[Pasted image 20250430203836.png]]

Cioè:  
>  Se un linguaggio è **decidibile in tempo non deterministico $f(n)$**, allora è anche decidibile **deterministicamente** in **tempo esponenziale** in $f(n)$.

🧠 **Cosa significa e perché è importante**
> Questo teorema ti risponde: **al massimo tempo $2^{O(f(n))}$**.  
> (Non sappiamo se basta meno, ma almeno abbiamo un limite superiore!)

![[Pasted image 20250502115345.png]]
Precisazioni sulla foto sopra:
- creiamo una macchina che accetta L
- usiamo una costante h per porre un limite entro in quale un ramo di una macchina non deterministica termini per forza
- con k indichiamo il grado di non determinismo, ma cosa è?
	- È il numero massimo di rami che si possono aprire da ogni configurazione della macchina.
- da non determinismo passiamo a determinismo con la macchina T
- se f è time-constructible allora anche con una costante h lo è quindi hf() è t-c

La dimostrazione anche qui è divisa in 2 parti
##### Parte 1
Simula la computazione $T_{f}(| x |)$
1. Scrive $1^{|x|}$ sul secondo nastro
	- Prende in input la stringa `x`
	- Conta i caratteri: `|x|`
	- Scrive `|x|` simboli `1` sul secondo nastro → $1^{|x|}$
	
	Questo è l'input per calcolare `f(|x|)` nella fase successiva.
 
 2. Calcola `f(|x|)` e scrive $1^{f(|x|)}$ sul terzo nastro
	- Usa una macchina trasduttore $T_f$ che:
	  - Prende $1^{|x|}$ come input
	  - Scrive $1^{f(|x|)}$ sul terzo nastro
	- Questa computazione richiede `O(f(|x|))` passi perché `f` è **time-constructible**

 3. Concatena `h` volte il contenuto del terzo nastro
	- Dal terzo nastro legge $1^{f(|x|)}$
	- Lo ripete `h` volte ottenendo: $1^{h · f(|x|)}$
	- Questo rappresenta il limite massimo di passi ammessi per ogni computazione di `NT(x)`
##### Parte 2
Simulazione delle vere e proprie computazioni deterministiche
	🎯 Obiettivo
	Simulare tutte le possibili computazioni deterministiche della macchina non deterministica $NT(x)$ entro un numero massimo di passi pari a $h(f(|x|))$.

1. 🔹Simula tutte le computazioni deterministiche di $NT(x)$ una per una:
	- Ogni computazione ha al massimo $h(f(|x|))$ passi.
	- Si usa un contatore sul terzo nastro con $1^{h(f(|x|))}$ in notazione unaria.
	- Le computazioni vengono simulate:
		 - da sinistra verso destra nell'albero delle scelte,
		  - una alla volta,
  - e ciascuna viene **interrotta** se supera il limite di passi.

Correttezza
###### ➤ Se $x \in L$:
- Almeno una computazione accetta entro $h(f(|x|))$ passi.
- Quindi T prima o poi simula quella computazione e accetta.
###### ➤altrimenti no
- $x \notin L$
 
 
 **T è corretta e decide $L$**.

#### Vari costi computazionali di questa macchina T

La fase 1:

Richiede $O(h(f(|x|)))$ passi, perché $f$ è time-constructible.

La fase 2:

- Sia $k$ il grado di non determinismo di $NT$ (costante).
- Il numero totale di computazioni deterministiche di lunghezza $h(f(|x|))$ è $k^{h(f(|x|))} = 2^{O(f(|x|))}$.
- Ogni computazione richiede al più $h(f(|x|))$ passi.

Quindi:
$$
\text{dtime}(T,x) \in O(h(f(|x|)) \cdot k^{h(f(|x|))}) = O(h(f(|x|)) \cdot 2^{O(f(|x|))}) \subseteq O(2^{O(f(|x|))})
$$
Dal Teorema 6.3 (che consente di simulare una macchina a più nastri con una a un nastro), possiamo dire che:
$$
L \in \text{DTIME}[2^{O(f(|x|))}]
$$


>[!attention]  Questi due teoremi potrebbero apparire all'esame
### Ora entriamo nel vivo della complessità computazionale
Stiamo per introdurre alcune fra le più rilevanti classi di complessità, definite sulla base di funzioni time- e space-constructible
##### 📌 Classi polinomiali
🔴 $P = ⋃ₖ∈ℕ DTIME[nᵏ]$
- Contiene tutti i linguaggi **decidibili** in **tempo deterministico polinomiale**
- Una macchina deterministica risponde sempre sì o no entro tempo $( n^k )$

🔴 $NP = ⋃ₖ∈ℕ NTIME[nᵏ]$
- Linguaggi **accettabili** in **tempo non deterministico polinomiale**
- Esiste un *ramo* della computazione che accetta entro $n^k$ se la parola è nel linguaggio
- Ma anche **decidibili** grazie alla simulazione entro tempo $O(f(n)$
##### 🟣 Classi di spazio

🟣 $PSPACE = ⋃ₖ∈ℕ DSPACE[nᵏ]$
- Linguaggi **decidibili** in **spazio deterministico polinomiale**

🟣$NPSPACE = ⋃ₖ∈ℕ NSPACE[nᵏ]$
- Linguaggi **accettabili** (e **decidibili**) in **spazio non deterministico polinomiale**

✅ **Teorema di Savitch**:  
- ci afferma che:
	- $\text{PSPACE} = \text{NPSPACE}$
##### 📌 Classi esponenziali

🔴 EXPTIME = ⋃ₖ∈ℕ DTIME$2^{p(n,k)}$
- Linguaggi **decidibili** in **tempo deterministico esponenziale**
- L'esponente \( p(n, k) \) è un polinomio

🔴 NEXPTIME = ⋃ₖ∈ℕ NTIME$2^{p(n,k)}$
- Linguaggi **accettabili** in **tempo non deterministico esponenziale**
- Ma anche **decidibili**, con le stesse tecniche di simulazione
###### 🟢 FP – Funzioni polinomiali
### FP = ⋃ₖ∈ℕ { f : Σ₁* → Σ₂* }
- Classe delle **funzioni totali calcolabili in tempo deterministico polinomiale**
- Una macchina di Turing **trasduttore calcola f(x) in tempo $O(|x|^k)$
#### Relazioni tra tutte queste classi Corollario 6.2

##### 🔴 $P \subseteq NP$, $PSPACE \subseteq NPSPACE$, $EXPTIME \subseteq NEXPTIME$
- 🧠 Conseguenza del **Teorema 6.8**:  
  Ogni macchina deterministica è un caso particolare di una macchina non deterministica (con grado di non determinismo pari a 1).  
  👉 Ogni linguaggio decidibile in tempo o spazio deterministico è anche decidibile in quello non deterministico.
##### 🔴 $P \subseteq PSPACE$, $NP \subseteq NPSPACE$
- 🧠 Conseguenza del **Teorema 6.9**:  
  Per ogni funzione totale e calcolabile $f(n)$:
  - $DTIME[f(n)] \subseteq DSPACE[f(n)]$
  - $NTIME[f(n)] \subseteq NSPACE[f(n)]$

➡️ Ogni linguaggio decidibile in tempo $f(n)$ è anche decidibile in spazio $f(n)$, ma non viceversa.  
Perché? Il tempo impone un limite superiore anche allo spazio usato.
##### 🔴 $PSPACE \subseteq EXPTIME$, $NPSPACE \subseteq NEXPTIME$
- 🧠 Conseguenza del **Teorema 6.10**:  
  Per ogni funzione calcolabile $f(n)$:
  - $DSPACE[f(n)] \subseteq DTIME[2^{O(f(n))}]$
  - $NSPACE[f(n)] \subseteq NTIME[2^{O(f(n))}]$

➡️ Una macchina che usa poco spazio può essere simulata deterministicamente in tempo esponenziale, perché lo spazio limita il numero di configurazioni possibili (che si possono esplorare in tempo).
##### 🔴 $NP \subseteq EXPTIME$
- 🧠 Conseguenza del **Teorema 6.17**:  
  Se $f(n)$ è **time-constructible**, allora:
  - $NTIME[f(n)] \subseteq DTIME[2^{O(f(n))}]$

➡️ Tutto ciò che è accettabile in tempo non deterministico è anche decidibile in tempo deterministico esponenziale.

📌 E siccome i **polinomi sono time-constructible**, allora in particolare:
  - $NP \subseteq EXPTIME$

>[!attention] SONO TUTTE INCLUSIONI DEBOLI (oppure improprie)
>Sappiamo che una classe è contenuta nell’altra, **ma non sappiamo se le due classi coincidano oppure no**.
Ad esempio:
>- Sappiamo che $\text{P} \subseteq \text{NP}$,  
  ma **non sappiamo se** $\text{P} = \text{NP}$ oppure $\text{P} \subset NP$ 

solo 2 uguaglianze sono state trovate
#### Grazie al teorema di Gerarchia temporale

>[!tip] Teorema 6.15
>![[Pasted image 20250502122804.png]]

✅ Significato:
- Esiste un linguaggio $L$ che è **decidibile in tempo** $f(n)$ ma **non** in $g(n)$.
	Questo perché $g(n)$ è troppo più piccolo (e meno potente) di $f(n)$
- Quindi $\text{DTIME}[f(n)]$ è **strettamente più potente** di $\text{DTIME}[g(n)]$.

Di conseguenza quindi abbiamo che:

- P $\subset$ EXPTIME (Teorema 6.18)
	- senza uguaglianza
	- abbiamo una inclusione propria
- $PSPACE = NPSPACE$ (Teorema 6.19)
	- qui sono uguali
	- senza dimostrazione da studiare
	- si scrive un programma in Pascal minimo



## Leggi con voce della Di Ianni
>[!quote] la lezione di oggi sarebbe finita
>ma visto che abbiamo tempo facciamo 3 esercizietti!
>va bene a TUTTI!!!???

#### Esercizi vari:

QUESTI ESERCIZI POSSONO CAPITARE ALL'ESAME IN TUTTE LE SALSE

Nota: se ho L1 accettabile non posso dire che $L1^c$ non possiamo dire nulla
- se ho L1 accettabile e precisato non decidibile allora il complemento è non decidibile

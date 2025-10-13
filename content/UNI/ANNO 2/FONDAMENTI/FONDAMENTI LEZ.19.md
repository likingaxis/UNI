## Ruolo delle grammatiche di tipo 2 e 3 nella programmazione
- **Tipo 2 (context-free)** → usato per la sintassi del linguaggio.
	- vengono usate per definire se una sintassi di un codice è corretta
		- tipo graffe { } che devono essere aperte e poi chiuse
- **Tipo 3 (regolare)** → usato per componenti lessicali (parole chiave, nomi di variabili)

## Grammatiche di tipo 3
In questa lezione parleremo principalmente di [[FONDAMENTI LEZ.13#Definiamo le varie grammatiche|grammatiche di tipo 3]], se vuoi ripassarle ecco una rapida spiegazione:
![[Pasted image 20250416192034.png]]
>[!tip] Tutti i linguaggi di tipo 3 sono REGOLARI

ecco un esempio:
![[Pasted image 20250416192120.png]]

## La domanda è sempre quella:
>[!question]  G3 $\subset$G2 oppure è $\subseteq$

##### Facciamo anche qui un pumping lemma(leggermente differente dal precedente)
>[!fire] Pumping lemma:
> 
> Per ogni linguaggio regolare **L** esiste un intero $( p_L > 0 )$ (dipendente esclusivamente da **L**) tale che per ogni parola $( z \in L )$ con $( |z| \geq p_L )$ esistono tre parole **u**, **v**, **w** tali che:
> 
> 1. $( z = u\ v\ w )$(cioè **z** si può esprimere come concatenazione di **u**, **v**, **w**)
> 2. $( |uv| \leq p_L )$
> 3. $( |v| \geq 1 )$ (**v** non può essere la parola vuota)
> 4. $( uv^h w \in L )$ per ogni $( h \geq 0 )$

>[!question]- perché v non deve essere una parola vuota e deve "pompare"?
>### 🔁 Idea fondamentale del *Pumping Lemma*
> Se un linguaggio è **regolare**, allora ogni parola abbastanza lunga può essere divisa in tre parti $u$, $v$, $w$, tali che:
> - $uv^n w \in L \quad \forall n \geq 0$
> 
> ### ⚠️ Perché $|v| \geq 1$?
> 
> Se $v = \varepsilon$, allora:
> - $uv^n w = uw$ per ogni $n$, quindi **tutte le parole sono uguali**  
> 👉 Non possiamo testare se la ripetizione di $v$ fa uscire la parola dal linguaggio.
> 
> ### 💡 Se invece $|v| \geq 1$...
> - Ripetere $v$ **modifica** la parola.
> - Se $uv^n w \notin L$ per qualche $n$, abbiamo **dimostrato che il linguaggio non è regolare**.
> in poche parole l'obiettivo è quello di pompare v finché non scoppia e la parola non è nel linguaggio

>[!attention] questa del pumping lemma è una condizione necessaria come quella delle grammatiche di tipo 2
>- sono necessari perché comunque esistono linguaggi che soddisfano il pumping lemma ma non sono comunque regolari❌
>- se fosse stato sufficiente avremmo avuto la certezza che era regolare e di tipo 2

>[!success] per questa ragione, di nuovo, il pumping lemma si utilizza ‘’al negativo’’ ´ ossia, per dimostrare che un linguaggio non è regolare
>- per farlo si cerca di mandare "fuori strada" le parole di quel linguaggio 
>	- si cerca di non far soddisfare il pumping lemma per dire che:
>		- quel linguaggio non è regolare

#### Esempio di uso del pumping lemma per far scoppiare tutta la parola
![[Pasted image 20250416195310.png]]
>[!tip]- questo esempio in poche parole
>abbiamo una parola formata da due caratteri a e b ripetuti n-volte prima uno poi l'altro
>- se prendiamo la parola e la suddividiamo in uvw possiamo dire con certezza che uv sicuramente contengono solo caratteri a
>	- invece w può avere sia a che b
>- nella dimostrazione diciamo che $|uv|\leq P_L$ solo perché lo diciamo noi
>	- fa parte della dimostrazione
>- detto questo quello che succede è che se proviamo a "pompare" la lettera v ci accorgiamo che il numero di caratteri a è diverso dalle b e quindi il linguaggio non è regolare
>- fine!

>n.b $u,v,w \in \Sigma^*$ 

Sostanzialmente anche per dimostrare che G3 $\subset$ proprio di G2 fa una sorta di pumping lemma
# Automi a stati finiti(decidibili)
i linguaggi regolari sono $\subset$ dei linguaggi di tipo 2
- quindi anche loro possono essere decidibili
	- se sono decidibili allora possono anche essere accettabili
Possiamo quindi creare un modello di calcolo (le ASFD)
che riconosce un linguaggio regolare
- per riconosce si intende se è accettabile, decidibile ecc...
### Come sono definiti(informale):
- Un **automa a stati finiti** può essere visto come una **Macchina di Turing molto limitata**, dove:
    - c’è **un solo nastro**, e **non si può scrivere** su di esso
    - la **testina è di sola lettura**
    - la computazione si ferma **quando finisce l’input**(si raggiunge il $\square$)
- La **funzione di transizione** ($\delta$) determina il passaggio da uno stato all'altro in base al simbolo letto.
- La computazione di un ASFD è **deterministica, finita e diretta**: parte da uno stato iniziale, legge ogni simbolo uno dopo l’altro, e **accetta o rifiuta** in base allo stato in cui si trova alla fine dell’input.
- le ASFD a differenza della Minchie di Turing
	- hanno stati che possono essere sia finali che non
	- mentre invece le MT hanno degli stati definiti solo come terminali
		- tu da $q_a$ non puoi muoverti
- questo creerà dei piccoli problemi quando andremo a fare la solita cosa
	- da macchina ASFD a MT
### Come sono definiti formalmente):
Un **automa a stati finiti deterministico (ASFD)** è una quintupla:
> $\langle \Sigma, Q, q_0, Q_F, \delta \rangle$

dove:
- $\Sigma$ è l'**alfabeto**
- $Q$ è l'**insieme degli stati**
- $q_0 \in Q$ è lo **stato iniziale**
- $Q_F \subseteq Q$ è l'insieme degli **stati finali**
- $\delta : Q \times \Sigma \rightarrow Q$ è la **funzione totale di transizione**, che associa a ogni coppia (stato, simbolo letto) un nuovo stato

🔁 Funzione di transizione in tabella
La funzione di transizione può essere rappresentata tramite **tabella**:

| $\delta$ | a   | b   |
|----------|-----|-----|
| $q_0$    | $q_0$ | $q_1$ |
| $q_1$    | $q_2$ | $q_0$ |
| $q_2$    | $q_2$ | $q_2$ |
>[!warning] La tabella deve essere tutta piena
>non possiamo avere caratteri con "azioni" non definite

La notazione $\delta(q, a) = q'$ è **equivalente** alla quintupla della Macchina di Turing:

> $\langle q, a, a, q', D \rangle$

(dove si legge un simbolo e ci si sposta a destra senza modificarlo)

###### 📈 Rappresentazione grafica
È possibile rappresentare l'automa anche con un **diagramma degli stati**:
- Lo **stato iniziale** ha una **freccia entrante con etichetta "start"**
- Gli **stati finali** sono indicati con un **doppio cerchio**
Esempio:
![[Pasted image 20250416205317.png]]
> Gli archi sono etichettati con i simboli letti (es. `a`, `b`, `a,b`), e i cerchi doppi rappresentano gli **stati finali**.

### Concetti delle MT trasposti sulle ASFD
Poiché un automa a stati finiti è una particolare macchina di Turing, possiamo estendere agli automi a stati finiti le definizioni di:
- stato globale
- transizione
- computazione
- esito di una computazione

tali definizioni risultano semplificate per gli automi a stati finiti perché hanno funzionalità più limitate

#### Esempio di stato globale per le ASFD
![[Pasted image 20250416205839.png]]
#### Esempio di transizione per le ASFD
![[Pasted image 20250416205945.png]]
>[!tip] la prof ha detto che se non ti ricordi di scrivere $|-$ va bene uguale perché tanto la $\rightarrow$ è praticamente la stessa cosa

### Definizione formale di computazione e transizioni
ora procediamo a spiegare come funzionano le computazioni per un modello di calcolo di questo tipo
Supponiamo di avere una parola: $$x=x_{0}​ \ x_{1} \ ​… \ x_{n}​ ∈ Σ^{∗}$$
La computazione parte da una configurazione iniziale $$(q_{0}, \ x)$$
> Cioè siamo nello stato iniziale $q_0$​ e dobbiamo leggere la parola `x`.


Ora, la sequenza di transizioni è descritta così $$(q_0, x_0x_1\ldots x_n) \vdash (q_1, x_1\ldots x_n) \vdash (q_2, x_2\ldots x_n) \vdash \ldots \vdash (q_n, x_n) \vdash (q, \square)$$Spiegazione:
- ad ogni passo leggiamo un simbolo $x_{i}$
	- si può anche dire che esso viene "consumato"
- lo stato cambia da $q_{i}$ a $q_{i+1}$ in base alla funzione di transizione $\delta(q_{i}, \ x_{i})$
- alla fine abbiamo letto tutto, e ci troviamo nello stato $q$ e con input vuoto ($\square$), ossia siamo a fine parola
#### Funzione di transizione estesa $\delta^{*}$ (delta star)
Una definizione ricorsiva di quello che abbiamo detto prima.
Viene definita funzione di transizione estesa  $\delta^*(q, x)$, e dice:
- $\delta^*(q, \square) = q$  (se l’input è vuoto, restiamo nello stato corrente)
- $\delta^*(q, a_1 a_2 \ldots a_n) = \delta(\delta^*(q, a_1 \ldots a_{n-1}), a_n)$

>In parole semplici:  
	è come dire: “**faccio una serie di $\delta$**, e ogni volta prendo lo **stato che ho ottenuto prima**, e lo uso come **input per la prossima transizione**”.


##### 🧠 **Conclusione**  
La computazione dell’automa a partire dalla configurazione iniziale $(q_0, x)$ è:
$$\delta^*(q_0, x)$$
E questo stato finale ci dice l’esito dell’elaborazione.  
Se questo stato è uno degli **stati finali**, allora la parola è **accettata**.

>[!bug] Osservazione: La funzione di transizione NON È DEFINITA quando sul nastro viene letto blank ($\square$).
>Nel senso che, come abbiamo detto prima, quando arrivi al blank devi fermarti E QUINDI per farlo non abbiamo nessuna transizione dal blank in poi.

Conseguentemente all'osservazione, possiamo dire che tutte le computazioni di un ASFD terminano e che
- se lo stato in cui si trova $\in Q_{F}$, la parola è ACCETTATA
	- detto in termini ricorsivi "se $q = 𝜹^{*}(q_{0}, x)$ è uno stato finale"

- se lo stato in cui si trova $\notin Q_{F}$, la parola viene RIGETTATA
	- detto in termini ricorsivi "quando $q = 𝜹^{*}(q_{0}, x)$ non è uno stato finale"

>[!lemma] Il linguaggio accettato da un ASFD $A = \langle \Sigma, Q, q_0, Q_F, \delta \rangle$ è l'insieme delle parole accettate da A, ossia $$L(A) = \{x \in \Sigma^{*} : (q_{0}, \ x) \vdash^{*} (q, \ \square) \ \ \ \text{con q} \in Q_{F}\}$$o equivalentemente $$L(A) = \{x \in \Sigma^{*} : \delta^{*}(q_{0}, \ x) \in Q_{F}\}$$
>in poche parole una serie di transizioni se portano a uno stato $Q_f$ con il rispettivo $\square$ allora il linguaggio è accettato da quel modello A
> $A$ legge l'intera parola $x$, e:
> - se termina in uno stato finale → accetta $x$
> - se termina in uno stato non finale → rifiuta $x$


Sottolineiamo che, poiché tutte le computazioni di un ASFD <u>terminano sempre</u> allora
>[!lemma] L(A) È IL LINGUAGGIO DECISO DA A
> **Differenza tra accettato e deciso**:  
> Un linguaggio è _accettato_ se l'automa riconosce tutte le parole del linguaggio (ma _potrebbe non terminare_ su quelle fuori dal linguaggio).  
> Un linguaggio è _deciso_ se l'automa **termina sempre** e dice **sì o no** per ogni parola.  
> Poiché un ASFD **termina sempre**, ogni linguaggio accettato da un ASFD è anche **deciso** da esso.
##### Esempio
![[Pasted image 20250417151543.png]]
## Macchina di Turing vs Automa a stati finiti
Abbiamo detto prima che un ASFD è una MT con dei deficit.

Tuttavia, le descrizioni dei due modelli differiscono in due aspetti
1. Un ASFD è descritto mediante una funzione di transizione $\delta$; mentre una MdT è descritta mediante un insieme di quintuple
	- SOLUZIONE: l'abbiamo già vista prima, fai in modo che la quintupla riscriva letteralmente il carattere letto e si sposti a destra
![[Pasted image 20250417152032.png]]
2. In un ASFD ci possono essere transizioni che partono da uno stato finale, in una MT questa cosa non è possibile
	- SOLUZIONE
		- fai in modo che gli unici stati finali della MT rimangano $q_{A}$ e $q_{R}$
		- aggiungi a P, per ogni stato finale $q$ dell'automa, le quintuple $$〈q,\square ,\square ,q_A, F〉$$
		- aggiungi a P, per ogni stato <u>NON</u> finale $q$ dell'automa, le quintuple $$\langle q, \square, \square, q_{R}, F \rangle$$
		**IN PRATICA**
		Tutti gli stati finali $q$ del ASFD diventano stati normalissimi per la MT, però quando li usi dici "ah aspetta, questo è uno stato finale, allora PREMATURAMENTE aggiungo la quintupla $\langle q, \square, \square,q_A,F \rangle$ nel caso in cui subito dopo volesse terminare" (nota come, nel caso in cui non terminasse, non andrei nella quintupla $\langle q, \square, \square, q_{A}, F \rangle$ ma ne sceglierei un'altra)
		Stessa cosa vale per i gli stati NON FINALI.

#### in definitiva possiamo dire che:
![[Pasted image 20250417152916.png]]
### Cosa resta da dimostrare
![[Pasted image 20250417154630.png]]

##### In questa lezione vedremo solo il PASSO 1)

>[!lemma] TEOREMA G.14
 Per ogni ASFD $A = \langle Σ, Q, q_0 , Q_F, 𝛿 \ \rangle$ esiste una grammatica $G_A= \langle 𝑉_T, 𝑉_N , P, S \rangle$  tale che $$L(A) = L(GA)$$
> ##### ✏️ Cosa significa?
Ogni **automa a stati finiti** può essere tradotto in una **grammatica regolare** equivalente.


![[Pasted image 20250417155228.png]]
>N.B.: Dal punto due abbiamo che ogni stato ho un simbolo non terminale corrispondente A

>[!tip]- spiegazione degli ultimi 3 punti
>![[Pasted image 20250417155521.png]]

### Iniziamo la dimostrazione vera e propria
$$x \in L(A) \Leftarrow\Rightarrow x \in L(G_A)$$

che dividiamo in 2 parti
la prima:
$$x \in L(A) \Rightarrow x \in L(G_A)$$
e poi la seconda:
$$x \in L(G_{A}) \Rightarrow x \in L(A)$$
#### PARTE 1
Stiamo dimostrando che:
$$x \in L(A) \Rightarrow x \in L(G_A)$$cioè:
> se una parola è **accettata** dall’automa, allora può essere **derivata** dalla grammatica regolare costruita.

##### ✏️ Passaggi
1. Sia $x = x_{0} \ x_{1} \ ... \ x_{n}$ una qualunque parola che appartiene al linguaggio accettato da A
	
2. Se $x \in L(A)$, allora possiamo scrivere che $$\delta^{*}(q_{0}, \ x) = q_{j} \in Q$$ossia che se l'automa parte da $q_{0}$ e legge tutta la parola, arriverà in uno stato finale $q_j$ 
	
3. Allora esiste una sequenza di stati $$q_{i_{1}}, \ q_{i_{2}}, \ ..., \ q_{i_{n}} \in Q$$tale che
	- $\delta(q_{0}, \ x_{0}) = q_{i_{1}}$
	- $\delta(q_{i_{1}}, \ x_{1}) = q_{i_{2}}$
	- ...
	- $\delta(q_{i_{n-1}}, \ x_{n-1}) = q_{i_{n}}$
	- $\delta(q_{i_{n}}, \ x_{n}) = q_{j} \in Q$
	
	Questa è la sequenza di stati visitati dall'automa mentre legge la parola, quindi ogni transizione è collegata e arriviamo al nostro $q_{j}$

##### 🔸Ora, colleghiamoci alla grammatica
Ricordiamo che nella grammatica avevamo costruito le produzioni così: $$A_i \rightarrow a A_h \quad \text{se } \delta(q_i, a) = q_h$$oppure $$A_i \rightarrow a \quad \text{se } \delta(q_i, a) = q_h \in Q_F$$
in poche parole se siamo alla fine non mettiamo più parole che appartengono ai $V_N$ 

Questo vuol dire che possiamo riscrivere la sequenza di transizioni in questo modo
- $A_0 \rightarrow x_0 A_{i_1}$  
- $A_{i_1} \rightarrow x_1 A_{i_2}$  
- $\ldots$  
- $A_{i_{n-1}} \rightarrow x_{n-1} A_{i_n}$
- $A_{i_{n}}\rightarrow x_{n}$ 

##### 🧠 Conclusione:
La grammatica ha quindi generato, tramite derivazione, la parola: $$
A_0 \Rightarrow x_0 A_{i_1} \Rightarrow x_0 x_1 A_{i_2} \Rightarrow \ldots \Rightarrow x_0 x_1 \ldots x_{n-1} A_{i_n} \Rightarrow x_0 x_1 \ldots x_n
$$CHE È ESATTAMENTE LA PAROLA CHE APPARTIENE A $L(A)$.

>[!lemma] Quindi $x\in L(G_{A})$

#### PARTE 2
Ora stiamo dimostrando $$x \in L(G_{A}) \Rightarrow x \in L(A)$$cioè:
> Se una parola può essere **generata dalla grammatica regolare $G_A$​**, allora è anche **accettata dall'automa $A$**.

##### ✏️ Passaggi della dimostrazione:
1. Supponiamo che $x = x_0 x_1 \ldots x_n \in L(G_A)$,  
	cioè: la grammatica ha derivato $x$, partendo da $A_0$: $$A_0 \Rightarrow^* x$$
2. Allora esistono non terminali $A_{i_1}, A_{i_2}, \ldots, A_{i_n} \in V_N$ tali che:
	- $A_0 \rightarrow x_0 A_{i_1}$
	- $A_{i_1} \rightarrow x_1 A_{i_2}$
	- $\ldots$
	- $A_{i_{n-1}} \rightarrow x_{n-1} A_{i_n}$
	- $A_{i_n} \rightarrow x_n$
	
	👉 Quindi la grammatica ha fatto esattamente la derivazione: $$A_0 \Rightarrow x_0 A_{i_1} \Rightarrow x_0 x_1 A_{i_2} \Rightarrow \ldots \Rightarrow x_0 x_1 \ldots x_n$$
3. Ma per come è costruita $G_A$, ogni produzione corrisponde a una transizione dell’automa:
	- $\delta(q_0, x_0) = q_{i_1}$
	- $\delta(q_{i_1}, x_1) = q_{i_2}$
	- $\ldots$
	- $\delta(q_{i_{n-1}}, x_{n-1}) = q_{i_n}$
	- $\delta(q_{i_n}, x_n) = q_f \in Q_F$
	
	📌 Quindi: partendo da $q_0$, l’automa legge tutta la parola e arriva in uno stato finale $q_f$, E QUINDI ACCETTA

>[!lemma] Quindi $x \in L(A)$

### ✅ Teorema completato:
Abbiamo dimostrato **entrambe le direzioni**:
- $x \in L(A) \Rightarrow x \in L(G_A)$
- $x \in L(G_A) \Rightarrow x \in L(A)$

quindi:
>[!lemma] $L(A) = L(G_{A})$

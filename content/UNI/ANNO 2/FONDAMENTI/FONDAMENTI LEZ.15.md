Questa lezione continua la precedente [[FONDAMENTI LEZ.14]]
Vogliamo dimostrare che se un linguaggio L è generato da una grammatica(di tipo 0)
allora esiste una macchina di Turing che accetta L ovvero:
$$L_{0} \subseteq A$$
Vogliamo quindi dimostrare che l'insieme dei Linguaggi accettabili coincide con quelli dell'insieme dei linguaggi generabili da grammatiche di tipo 0
# Teorema G.5
Per ogni grammatica G esiste una macchina di Turing che accetta L(G).

Ossia:
$\forall$ grammatica $G$   
	$\exists \ T$ : $L(G)$ è il linguaggio accettato da $T$
		Avendo $G = <V_{N}, V_{T}, P_{G}, S>$
	$\forall \ x \ \exists \ V_{T}^{*} \ [o_{T}(x) = q_{A} \iff L(G)]$
### Andiamo a definire una dimostrazione ma che è sbagliata

Sia $G$ la grammatica definita come $$G = <V_{N}, V_{T}, P_{G}, S>$$
Progettiamo una macchina di Turing [[FONDAMENTI LEZ.5|NON DETERMINISTICA]] a 2 nastri
- su N1 scriviamo l'input $x \in V_{T}^{*}$
- su N2 è il nastro di lavoro (su cui scriviamo le parole generate da $G$)
Scegliamo una macchina non deterministica perché così posso simulare TUTTE le computazioni "insieme".

Cosa facciamo?
- scriviamo sul secondo nastro $S$ e iniziamo a scrivere tutte le produzioni
	1) Se ad un certo punto la **parola scritta sul nastro 2 è uguale all'input (nastro 1)**, <font color="#245bdb">accetta</font>
	2) se abbiamo uno di questi due casi
		- la parola sul nastro due contiene tutti terminali MA è diversa dall'input
		- la parola sul secondo nastro ha qualche carattere NON terminale MA non possiamo più applicare produzioni 
		allora <font color="#ff0000">rigetta</font>
La dimostrazione è sbagliata perché, pur cercando di riconoscere `x`, non garantisce che in caso positivo (`x ∈ L(G)`) venga mai accettato in tempo finito.  
Una macchina riconoscitrice deve:
- accettare in tempo finito **se `x ∈ L(G)`**
- può **non terminare mai** se `x ∉ L(G)`  
    (**non è obbligata a rigettare esplicitamente**)
### Per capire ancora meglio andiamo a fare un esempio
- Grammatica: $G = <V_{N}, V_{T}, P_{G}, S>$
	- $V_{N} = \{S\}$
	- $V_{T} = \{a,b\}$
	- Produzioni
		- `S -> aSa |  bSb | a | b | ε`
	
- Input: `ababa`

📌Quindi l'obiettivo è prendere l'input `ababa` e vedere se la grammatica produce la stessa parola e quindi accetta il linguaggio

allora avremmo una macchina non deterministica $NT(x)$ con la seguente computazione:
![[Pasted image 20250406121647.png]]
i nodi sono le produzioni su $N2$ mentre gli archi indicano che la produzione è stata applicata
in questo caso accetta e quindi funziona

>[!question] Perché funziona?
>Perché dopo ogni produzione avrò sempre MASSIMO una $S$, quindi ogni volta la macchina dovrà eseguire un numero di produzioni **COSTANTE** (visto che tutte le produzioni partono da $S$, e sono 5, allora per ogni parola (nodo) verranno applicate 5 produzioni).

>[!question] Ma funziona sempre?
>NO e riprendiamo ciò che abbiamo detto prima.
>
>Immagina di avere queste produzioni
> - `S -> ABS | ε`
>- `B -> Cb`
>- `AC -> cA`
>- `BC -> Cc`
>- `C -> ε`
>
>Se $x$ è tanto grande, verrà generata una parola molto grande che sarà del tipo $$S \ \rightarrow \ ABS \ \Rightarrow_{G} \ ABABS \ \Rightarrow_{G} \ ABABABS  \ \Rightarrow_{G}^{*} \ (AB)^{n}S$$e poi dovrò applicare la produzione `B -> Cb`.
>Fin qui tutto tranquillo.
>
>Però ora chiediti, **quante volte devo applicare la produzione**? *DIPENDE DALLA LUNGHEZZA DELLA PAROLA*.
>
>QUINDI ***NON È COSTANTE*** COME NEL CASO DI PRIMA.
>![[Pasted image 20250406122026.png]]


Per risolvere questi problemi dobbiamo modificare la macchina.

## DIMOSTRAZIONE CORRETTA PERFETTA ASSURDA!
Progettiamo una macchina di Turing NON DETERMINISTICA  $NT_{G}$ a **3 nastri**
- su N1 scriviamo l'input $x \in V_{T}^{*}$
- su N2 è il nastro di lavoro (su cui scriviamo le parole generate da $G$)
- su N3 scrivo un intero (inizializzato a 1)

>[!question] a che ci serve il nastro N3?
>il nastro N3  ci serve per rappresentare la posizione della parola su cui applicare una produzione, ad esempio:
> - parte da un nodo
> - guarda `i`
> - applica la produzione in posizione `i` generando una nuova parola (nodo nel livello successivo)
> - ora inizio a applicare le produzioni in posizione `i` sulla nuova parola
> - e continua finché non si ferma
> 	- per $q_{A}$
> 	- per $q_{R}$
> 	- perché ha finito le quintuple(raggiunge la fine di i)
> 
> SE ARRIVA IN $q_{A}$
> - vuol dire che ha confrontato la parola generata con l'input e sono uguali.
> 
> SE NON ARRIVA IN $q_{A}$ (le parole sono diverse)
> - incrementa `i`
> - **rimane nella parola corrente** (quindi nello **stesso nodo** dell’albero)
> - e prova ad applicare le produzioni da **una posizione successiva**
> 
>[!danger] QUANDO CAMBIO RAMO, `i` viene riportato a `1`.
>
>in sostanza faccio le produzioni perché voglio ricondurmi alla parola giusto, quindi vado in posizione 1 della parola iniziale, mi accorgo che non posso fare produzioni quindi vado in posizione 2 e così via finché non arrivo alla i finale e posso determinare se ho raggiunto una parola accettabile o no
>esempio grafico:
>![[Pasted image 20250406123325.png]]

Il grado di non determinismo è costante e la computazione non prova le produzioni a casaccio ma con una logica ben definita(si basa sulle i posizioni)
il grado di non determinismo della macchina rimane costante
### Approfondimento sui rami
Quanti rami ho?
Il **numero di produzioni** + la produzione in cui non esegue nulla ma **incrementa**, quindi $$|P_{G}| + 1$$
Quindi il valore è **costante** e **NON DIPENDE DALL'INPUT**.
### La macchina funziona correttamente
infatti $NT_{G}$ accetta una parola $x$ $\iff$ esiste una sequenza di produzioni che, partendo da $S$, genera $x$.
Cioè, la macchina simula correttamente ogni sequenza di produzioni come: $$S \ \Rightarrow_{G} \ x_{1} \ \Rightarrow_{G} \ x_{2} \ ... \Rightarrow_{G} \ x$$
Quindi: $$NTG(x) \ accetta  \iff   x \in L(G)$$
E da qui concludi che: $$L(NTG​)=L(G)$$
Per quanto riguarda il caso in cui x ∉ L(G)
la macchina entra in un loop infinito e quindi eseguire computazioni non terminali
ciò va comunque bene perché a noi ci basta che essa accetti se x ∈ L(G) in un tempo *finito*
$NT_G$ tenta **tutte le possibili sequenze di produzioni**, nella speranza di trovare **una derivazione che generi $x$**.  
Ma se $x$ **non appartiene a $L(G)$**, nessuna derivazione porterà mai a $x$, e quindi:
	$x \notin L(G) \quad \Rightarrow \quad NT_G(x)$ non rigetta (potrebbe non terminare)

## precisazione su una possibile scorciatoia
- ✔️ stiamo lavorando con **grammatiche di tipo 0**
- 🚫 **non possiamo usare euristiche** (tipo la lunghezza della parola) per decidere se un ramo porterà a `q_A` oppure no
- 😵 Quindi **il problema del `q_R`** (cioè sapere se dobbiamo rigettare) **è davvero complicato con grammatiche di tipo 0**
- 🚫non possiamo dire tipo "stiamo incappando in una situazione dove abbiamo una parola lunga 2000 mentre x era 5" perché potrebbe esserci una produzione che la accorcia a 5
## Conclusione
![[Pasted image 20250406124551.png]]
# ESERCIZIO DA FARE
![[Pasted image 20250406124607.png]]
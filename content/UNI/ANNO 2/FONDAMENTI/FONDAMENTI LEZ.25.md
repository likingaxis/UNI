## Classi complemento
Oltre ad aver definito le classi computazionali classiche ci sono anche quelle complemento:
![[Pasted image 20250508160948.png]]
Non cambia nulla se stiamo parlando di linguaggi L o $L^c$ perché il teorema 6.11 ci dice che sostanzialmente i costi sono gli stessi
>[!tip] Teorema 6.11 recap
>![[Pasted image 20250508161359.png]]
>che viene dimostrato:
>- Si prende una macchina T che decide L tale che, per ogni x, $dtime(T,x) ∈ O(f(|x|))$
>	- questa cosa vale anche per dspace
>	- sostanzialmente una macchina che decide una x nel linguaggio L in tempo al più la lunghezza dell'input
>
>successivamente si crea una macchina T' che complementa gli stati finali della macchina e ci si rende conto che lo fanno nello stesso tempo o spazio
>![[Pasted image 20250508162102.png]]

### Dal teorema 6.11 possiamo derivare delle definizioni
##### Corollario 6.3
>[!tip] Corollario 6.3
>- P = coP
>- coPSPACE = PSPACE

Questo è definito per le classi deterministiche


>[!question] possiamo dire lo stesso per le non?
>- possiamo utilizzare la stessa tecnica utilizzata nella dimostrazione del Teorema 6.11 nel caso non deterministico?
>- Possiamo complementare gli stati di accettazione e di rigetto di una macchina NT che accetta un linguaggio L al fine di accettare il complemento di L?

Ricordiamo che:
- le classi non deterministiche sono definite come classi di linguaggi accettati da macchine non deterministiche entro quantità limitate di istruzioni o celle di nastro
abbiamo inoltre detto che:
- malgrado abbiamo macchine di Turing non deterministiche che decidono un linguaggio in un certo tempo
	- presentano comunque una asimmetria
Questo perché nelle macchine **deterministiche** a differenza di quelle non hanno accettazione e rigetto **simmetrici**: basta invertire lo stato finale.
- questo ci ha permesso di dimostrare il 6.11
- la prof ci fa vedere comunque che succede se lo facciamo con quelle non deterministiche
e ci accorgiamo che **la dimostrazione non può funzionare allo stesso modo**, proprio a causa dell’asimmetria(spoilerz)
### applichiamo la stessa tecnica
- costruiamo una nuova macchina NT’ invertendo gli stati di accettazione e di rigetto di NT
- e vediamo se NT’ accetta (oppure no) il complemento del linguaggio accettato da NT
Cominciamo scegliendo un linguaggio L ⊆ {0,1}* accettato da una macchina di Turing non deterministica NT
ricordiamo che il linguaggio complementato $L^c$ si crea facendo
- $L^c = \{0,1\}^*- L$ ossia, per ogni x ∈ {0,1}* 
	- se x ∈ L allora x ∉ $L^c$ 
	- se x ∉ L allora x ∈ $L^c$
in poche parole il contrario
##### Come si comporta una macchina $NT^C$?
![[Pasted image 20250508164718.png]]
quindi nel concreto possiamo avere macchine non deterministiche complementari

#### Ora proviamo ad applicare la vera e propria dimostrazione del teorema 6.11 per le non deterministiche

- Scegliamo un linguaggio $L⊆{0,1}^∗$che è accettato da una macchina di Turing **non deterministica**, chiamiamola **NT**.
poi -> 
- Proviamo a fare come nel Teorema 6.11:
    > Costruire una nuova macchina **NT′** invertendo gli **stati di accettazione e rigetto** della NT  
    > (cioè, provare a costruire una macchina che accetta il **complemento** di L)

per sgamare eventuali errori sul seguente teorema, creiamo una macchina $NT_1$ che
![[Pasted image 20250508170212.png]]
in poche parole questa macchina per ogni possibile input avrà comunque uno stato di rigetto

In pratica: abbiamo "iniettato" una computazione finta che **fallisce sempre**,  
anche se NT accettava x tramite un’altra computazione.
nella foto sotto vediamo che ora NT rigetta sempre con le nuove quintuple
![[Pasted image 20250508170423.png]]

Possiamo inoltre notare anche che 
- NT₁ accetta **tutto ciò che accettava NT** (cioè il linguaggio L)
- **Ma in più** ha una computazione che porta a rigetto
![[Pasted image 20250508171030.png]]
oltre a non accettare rigetta anche
- se tutte le computazioni di NT rigettano
- anche le computazioni di $NT_1$ rigettano+ quella speciale che rigetta sempre
questo avviene quando x ∉ L
![[Pasted image 20250508171241.png]]

Adesso che abbiamo definito $NT_1$ correttamente possiamo applicare le stesse cose del teorema 6.11
- proviamo a creare la macchina non deterministica complementare
	- $NT_1^C$ 
	- invertendo gli stati di accettazione e di rigetto di NT1

Ora andremo a verificare se **NT₁ᶜ accetta il complemento di L**, cioè se davvero:
- accetta gli input **x ∈ Lᶜ**
- e **non accetta** quelli in L

Dividiamo in 2 casi:
Se $x \in L^C$ 
![[Pasted image 20250508171748.png]]
ma che succede invece se
Se $x \notin L^C$ ?
$NT_1^C$ non dovrebbe accettare
![[Pasted image 20250508171852.png]]
### Ricapitolando
visto che con le macchine non deterministiche abbiamo una asimmetria non possiamo dire che
![[Pasted image 20250508172216.png]]

### congetture di classi
- abbiamo detto che la maggior parte delle inclusioni tra classi di complessità sono deboli
	- non si dimostra che sono diverse
	- ma nemmeno uguali
il caso famoso riguarda soprattutto P e NP
![[Pasted image 20250508173815.png]]


Da qui nasce un teorema che definisce una relazione tra queste due congetture definite sopra
##### Teorema 6.23
>[!tip] Teorema 6.23
>![[Pasted image 20250508173935.png]]
>![[Pasted image 20250508174058.png]]


##### Teorema 6.24
>[!tip] Teorema 6.24
>![[Pasted image 20250508174147.png]]
>Cioè: se prendi un problema in coNP e lo riduci polinomialmente a un altro problema, il problema risultante resta in coNP.


### Come per tutte le classi di complessità, anche per la classe coNP possiamo definire linguaggi completi rispetto alla riducibilità polinomiale


![[Pasted image 20250508175029.png]]
### **Cosa abbiamo imparato dalla classe NP:**
- Quando supponiamo che **P ≠ NP**, allora i **linguaggi NP-completi** non possono appartenere a P.
- Questi linguaggi sono quindi i **“più difficili”** della classe NP.
- Inoltre, proprio per questa loro difficoltà, possono agire da **linguaggi separatori** tra P e NP (cioè: se uno di essi stesse in P, P = NP, altrimenti no).
### **Cosa vogliamo fare con coNP:**
- **Stessa logica, ma tra NP e coNP.**
- Vogliamo mostrare che i **linguaggi coNP-completi** sono i candidati a essere **linguaggi separatori** tra NP e coNP.
- Cioè, se supponiamo che **coNP ≠ NP**, allora:
    - **Un linguaggio coNP-completo non può stare in NP**
    - Anche qui, questi linguaggi sono i “più difficili” all’interno di coNP.
##### Teorema 6.25
>[!tip] Teorema 6.25
>Un linguaggio L è NP-completo se e soltanto se il suo complemento $L^c$ è coNP-completo
>per dimostrarlo facciamo una doppia <= => 
>![[Pasted image 20250508180423.png]]
>Ora dimostriamo l'altra parte
>![[Pasted image 20250508180440.png]]

##### Teorema 6.26
>[!tip] Teorema 6.26
>![[Pasted image 20250508180634.png]]
>![[Pasted image 20250508180647.png]]
>![[Pasted image 20250508180657.png]]


# 📘 Lezione 20 settembre – Definire operatori e precedenza in Prolog

## 1. Perché gli operatori?

In Prolog, sotto il cofano, anche le espressioni più semplici sono **termini**.  
Per esempio l’espressione aritmetica `1 + 2 * 3` non è “un calcolo”, ma un termine annidato, equivalente a:

`+(1, *(2,3))`

Chiaramente nessuno vuole scrivere sempre così. Per questo Prolog permette di dichiarare **operatori**, in modo da rendere più leggibile il codice e decidere **chi lega più forte** e **in che ordine** interpretare una sequenza di simboli.

---

## 2. Come si dichiara un operatore

Si usa il predicato:

`op(Precedenza, Tipo, Nome).`

- **Precedenza**: è un numero da 1 a 1200.  
    Più il numero è fottutamente **piccolo**, più l’operatore “lega forte” (cioè viene valutato prima).
    
- **Tipo**: indica se l’operatore è infisso, prefisso o postfisso, e come si comporta con altri operatori della stessa cazzo di precedenza.
    
- **Nome**: è l’atomo che diventa l’operatore (es. `and`, `or`, `++`).
    

Esempio semplice:

`:- op(500, yfx, plus).`

Dichiara `plus` come operatore **infix** (in mezzo) con precedenza 500.

---

## 3. Cosa significano x e y

Questa è la parte che spesso sembra misteriosa.  
Le lettere `x` e `y` dicono se **l’argomento può avere la stessa precedenza dell’operatore**:

- `x` → l’argomento deve avere precedenza **più alta** (numero più basso).
    
- `y` → l’argomento può avere precedenza **uguale o più alta**.
    

Questo serve a decidere se puoi scrivere catene senza parentesi, e in che direzione si associano.

---

## 4. Infix: associatività

Se definisci un operatore **infix** (tra due argomenti), hai tre possibilità:

- `yfx` → associativo a sinistra  
    Esempio: con `plus/2` dichiarato `yfx`, Prolog interpreta:
    
    `1 plus 2 plus 3   ⇒   plus(plus(1,2), 3)`
    
- `xfy` → associativo a destra  
    Utile per potenze:
    
    `2 pow 3 pow 2   ⇒   pow(2, pow(3,2))`
    
- `xfx` → non associativo  
    Vietate le catene:
    
    `a eq b eq c   ⇒   ERRORE senza parentesi`
    

---

## 5. Prefix e Postfix

Gli operatori possono stare anche **prima** o **dopo** dell’argomento:

- **Prefisso (fx/fy)**: esempio `not a`.
    
    - `fx`: l’argomento deve avere precedenza più alta.
        
    - `fy`: l’argomento può avere stessa precedenza → permette catene tipo `not not a`.
        
- **Postfisso (xf/yf)**: meno usati, ma possibili.
    
    - `xf`: l’argomento a sinistra deve avere precedenza più alta.
        
    - `yf`: può avere la stessa → puoi scrivere cose tipo `a !!` (se definito).
        

---

## 6. Precedenza nella pratica

Una regola utile da ricordare è: **numeri più piccoli = operatori più forti**.  
Quindi, se vuoi simulare un po’ di algebra di merda:

- `*` intorno a 400
    
- `+` intorno a 500
    
- comparazioni (<, =, …) intorno a 700
    
- logica (`and`, `or`) intorno a 800–900
    
- `:-` e `,` molto esterni (intorno a 1000–1200)
    

Esempio:

`:- op(300, fy, not). :- op(800, yfx, and). :- op(850, yfx, or).`

Così Prolog interpreta in modo naturale le cazzo di operazioni:

`not a and b or c   ⇒   or(and(not(a), b), c)`

---

## 7. Esempi concreti

### Somma left-associativa

`:- op(500, yfx, plus).`

Uso:

`?- 1 plus 2 plus 3. plus(plus(1,2), 3).`

### Potenza right-associativa

`:- op(400, xfy, pow).`

Uso:

`?- 2 pow 3 pow 2. pow(2, pow(3,2)).`

### Operatore prefisso

`:- op(300, fy, not).`

Uso:

`?- not not a. not(not(a)).`

---

## 8. Buone pratiche

- Non ridefinire operatori già esistenti (=, is, :- …).
    
- Usa gli operatori solo se rendono il codice più leggibile.
    
- Quando hai dubbi, **metti sempre le parentesi**: hanno precedenza massima.
    

---

## 9. Esercizi consigliati

1. Definisci `and` e `or` con precedenze tali che `not` leghi più di `and` e `and` più di `or`. Verifica il parse di `not a or b and not c`.
    
2. Definisci un operatore `**` right-associativo e prova `2 ** 3 ** 2`.
    
3. Definisci un operatore `eq` non associativo e verifica che `a eq b eq c` dia errore.
    

---

## 10. Riassunto finale

- In Prolog tutto è un termine.
    
- `op/3` ti permette di dichiarare operatori con precedenza e associatività.
    
- `x` e `y` regolano se gli argomenti possono avere stessa precedenza (influenza le catene).
    
- Numeri più bassi = legano più forte.
    
- Usare operatori è comodo, ma va fatto con giudizio.
# 📘 Lezione 21 settembre – `findall`, `bagof`, `setof`

## 1. Il problema di fondo

Di solito, Prolog ti dà **una soluzione di merda alla volta**.  
Esempio:

`colore(rosso). colore(verde). colore(blu).  ?- colore(X). X = rosso ; X = verde ; X = blu.`

Se vuoi **una lista con tutte le soluzioni** (`[rosso, verde, blu]`), hai bisogno di strumenti appositi: `findall`, `bagof` e `setof`.

---

## 2. `findall/3`

### Sintassi

`findall(Termine, Goal, Lista).`

- `Termine` → cosa raccogliere.
    
- `Goal` → la query da eseguire.
    
- `Lista` → la lista di tutte le istanze del cazzo trovate.
    

### Esempio semplice

`?- findall(X, colore(X), L). L = [rosso, verde, blu].`

### Se non ci sono soluzioni

`findall` restituisce sempre una lista, anche se vuota:

`?- findall(X, animale(X), L). L = [].`

📌 **Importante**: `findall` ignora variabili libere nel `Goal`. Quindi se ci sono variabili non vincolate, non separa i risultati per valori diversi → mette tutto insieme.

---

## 3. `bagof/3`

### Sintassi

`bagof(Termine, Goal, Lista).`

Simile a `findall`, ma **tratta le variabili libere come parametri**.  
Cosa significa? Che separa i risultati in base alle variabili non legate.

### Esempio

`padre(mario, gianni). padre(mario, luca). 
`padre(gianni, anna).  
`?- bagof(Figlio, padre(Padre, Figlio), L). 
`Padre = mario,  L = [gianni, luca] ; 
`Padre = gianni, L = [anna].`

Qui `Padre` è **variabile libera**: quindi `bagof` ti dà un risultato **per ogni valore di Padre**.

### Se vuoi ignorare una variabile libera

Puoi usare l’operatore `^` per “bloccare” una variabile:

`?- bagof(Figlio, Padre^padre(Padre, Figlio), L). 
`L = [gianni, luca, anna].`

---

## 4. `setof/3`

### Sintassi

`setof(Term, Goal, Lista).`

È identico a `bagof`, ma in più fa queste troiate:

- Ordina la lista in ordine crescente.
    
- Elimina i duplicati.
    

### Esempio

`colore(rosso). colore(verde). colore(rosso).  ?- setof(X, colore(X), L). L = [rosso, verde].`

---

## 5. Differenze riassunte

- **findall** → piglia tutto, sempre in una lista (anche vuota). Non distingue variabili libere.
    
- **bagof** → raggruppa i risultati per ogni combinazione di variabili libere.
    
- **setof** → come `bagof`, ma i risultati sono ordinati e senza duplicati.
    

---

## 6. Esempi comparativi

### Database

`padre(mario, gianni). padre(mario, luca). padre(gianni, anna). padre(gianni, luca).   % duplicato intenzionale`

### findall

`?- findall(F, padre(P, F), L). L = [gianni, luca, anna, luca].`

→ tutto in una lista unica, duplicati inclusi.

### bagof

`?- bagof(F, padre(P, F), L). P = gianni, L = [anna, luca] ; P = mario,  L = [gianni, luca].`

→ risultati separati per `P`.

### setof

`?- setof(F, padre(P, F), L). P = gianni, L = [anna, luca] ; P = mario,  L = [gianni, luca].`

→ come `bagof`, ma liste ordinate e senza duplicati.

---

## 7. Esercizi pratici

1. Usa `findall` per raccogliere tutti i colori in una lista.
    
2. Usa `bagof` per ottenere i figli di ciascun padre separatamente.
    
3. Usa `setof` per ottenere tutti i padri distinti ordinati alfabeticamente.
    
4. Crea un predicato `figli(Padre, ListaFigli)` che usa `bagof`.
    

---

## 8. Riassunto

- `findall/3`: raccoglie tutto in una lista (anche vuota).
    
- `bagof/3`: separa i risultati in base alle variabili libere.
    
- `setof/3`: come `bagof`, ma ordina e rimuove duplicati.
    
- `^` serve a bloccare una variabile quando non vuoi che venga considerata “libera”.
# 📘 Lezione 22 settembre – Ripasso generale di Prolog (teoria + esempi minimi)

---

## 1. Basi del Prolog

- **Fatti** → verità assolute:
    

`padre(mario, gianni).`

- **Regole** → “se… allora…”:
    

`nonno(X,Y) :- padre(X,Z), padre(Z,Y).`

- **Query** → domande:
    

`?- padre(mario, gianni).   % true ?- padre(mario, X).        % X = gianni`

👉 **Unificazione**: Prolog prova a rendere due termini uguali sostituendo variabili.  
👉 **Backtracking**: Prolog cerca più soluzioni esplorando alternative.

---

## 2. Liste e ricorsione

- Sintassi: `[a,b,c]` oppure `[H|T]`.
    
- Predicati built-in:
    

`member(X,L).      % vero se X è in L append(L1,L2,L3). 
`% L3 = L1+L2 length(L,N).      % N = lunghezza di L reverse(L,R).     % R = L al contrario`

- Ricorsione tipica:
    

`my_length([],0). my_length([_|T],N) :- my_length(T,N1), N is N1+1.`

---

## 3. Strutture e alberi

- **Termine complesso** = `funtore(arg1,...,argN)`.
    
- **Funtore** = nome, **Arity** = numero di argomenti.
    

Esempio:

`mangia(cavallo, biada).   % funtore = mangia, arità = 2`

- Ricorsione su alberi:
    

`stessa_struttura(nil,nil). stessa_struttura(nodo(_,SX1,DX1), nodo(_,SX2,DX2)) :-     stessa_struttura(SX1,SX2),     stessa_struttura(DX1,DX2).`

---

## 4. Cut e Fail

- `fail` → fallisce sempre → forza backtracking.
    

`stampa_colore :- colore(X), write(X), nl, fail.`

- `cut (!)` → blocca backtracking.
    

`massimo(X,Y,X) :- X >= Y, !. massimo(_,Y,Y).`

- `not` simulato:
    

`not(P) :- P, !, fail. not(_).`

---

## 5. Assert, Retract, Univ

- Modifica dinamica della KB:
    

`:- dynamic padre/2. ?- assert(padre(gianni, anna)). ?- retract(padre(gianni, anna)).`

- =.. (univ): converte tra termine e lista.
    

`?- mangia(cavallo,biada) =.. L. L = [mangia,cavallo,biada].  ?- T =.. [ama,romeo,giulietta]. T = ama(romeo,giulietta).`

---

## 6. DCG (Definite Clause Grammars)

- Usate per riconoscere/parlare frasi → `-->`.
    

`frase(mangia(S,O)) --> [il], nome(S), [mangia], [la], nome(O).  nome(cavallo) --> [cavallo]. nome(biada)   --> [biada].`

Uso:

`?- frase(X,[il,cavallo,mangia,la,biada],[]). X = mangia(cavallo, biada).`

---

## 7. Operatori

- Dichiarazione:
    

`:- op(500, yfx, plus).`

- **Precedenza**: 1–1200 (numero più piccolo = più forte).
    
- **x/y** → se l’argomento può avere stessa precedenza.
    
    - `yfx` → associativo a sinistra.
        
    - `xfy` → associativo a destra.
        
    - `xfx` → non associativo.
        

Esempio potenza:

`:- op(400, xfy, pow). ?- 2 pow 3 pow 2. pow(2, pow(3,2)).`

---

## 8. Raccolta soluzioni: findall, bagof, setof

- `findall(T,Goal,L)` → raccoglie tutte le soluzioni (anche se 0 → `[]`).
    
- `bagof(T,Goal,L)` → separa per variabili libere.
    
- `setof(T,Goal,L)` → come `bagof`, ma lista ordinata senza duplicati.
    

Esempio:

`padre(mario, gianni). padre(mario, luca). padre(gianni, anna).  ?- findall(F,padre(P,F),L). L = [gianni,luca,anna].  ?- bagof(F,padre(P,F),L). P = gianni, L = [anna] ; P = mario,  L = [gianni,luca].  ?- setof(F,padre(P,F),L). P = gianni, L = [anna] ; P = mario,  L = [gianni,luca].`

---

## 9. Schema pratico da esame

👉 Quando leggi un esercizio, chiediti:

- Devo **navigare liste/alberi**? → ricorsione + `append/member`.
    
- Devo **stampare o forzare più soluzioni**? → `fail`.
    
- Devo **scegliere un’unica regola**? → `cut`.
    
- Devo **aggiungere/rimuovere fatti**? → `assert/retract`.
    
- Devo **riconoscere frasi**? → DCG.
    
- Devo **raccogliere tutte le soluzioni**? → `findall/bagof/setof`.
    
- Devo **scrivere elegante**? → magari definire operatori con `op/3`.
    

---

## 10. Esercizi di ripasso veloce

1. Definisci `conta_occorrenze(X,L,N)` con ricorsione.
    
2. Usa `not/1` per definire `diverso(X,Y)`.
    
3. Scrivi una DCG che traduce `[il,ragno,mangia,rosmarino]` in `mangia(ragno,rosmarino)`.
    
4. Con `bagof`, trova i figli di ogni padre in una KB familiare.
    
5. Definisci `**` come operatore infix right-associativo per potenze.
    

---

# ✅ Riassunto finale

In 8 giorni abbiamo visto:

- Fatti, regole, query, unificazione e backtracking.
    
- Liste e ricorsione.
    
- Strutture e alberi.
    
- Cut, fail e `not`.
    
- Assert, retract e =...
    
- DCG per parsing.
    
- Operatori personalizzati.
    
- Raccolta soluzioni con findall/bagof/setof.
    

Con questo zoccolo teorico puoi affrontare gli esercizi d’esame. Da domani si passa ai **casi pratici** (Language Model, rete alimentare, campo di battaglia).

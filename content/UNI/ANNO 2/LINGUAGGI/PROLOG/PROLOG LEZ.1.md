Perfetto 💪 iniziamo con la **lezione del 14 settembre**: basi di Prolog, regole, fatti, query e unificazione.  
Ti scrivo in modo chiaro, con spiegazioni + esempi pratici che puoi copiare in un file `.pl`.

---

# 📘 Lezione 14 settembre – Basi di Prolog

## 1. Cos’è Prolog

- Prolog è un linguaggio **dichiarativo**: tu descrivi i **fatti** e le **regole** del problema, e Prolog trova le soluzioni tramite **unificazione** e **backtracking**.
    
- Non dici “come fare le cose” passo per passo (stile Python o C), ma **cosa è vero** nel tuo mondo.
    

---

## 2. Fatti

Un **fatto** rappresenta una verità del mondo che stai modellando.  
Esempio (famiglia):

`padre(mario, gianni). 
`padre(gianni, luca). 
`padre(luca, anna).`

Qui stai dicendo:

- Mario è padre di Gianni.
    
- Gianni è padre di Luca.
    
- Luca è padre di Anna.
    

---

## 3. Regole

Una **regola** permette di definire relazioni complesse a partire dai fatti.  
La forma è:

`testa :- corpo.`

Significa: **“testa è vera se corpo è vero”**.

Esempio: definire il predicato `nonno(X,Y)`:

`nonno(X,Y) :- padre(X,Z), padre(Z,Y).`

Leggilo così:

> “X è nonno di Y se X è padre di Z e Z è padre di Y”.

---

## 4. Query

Le **query** (interrogazioni) si scrivono nel prompt Prolog con `?-`.  
Esempi:

`?- padre(mario, gianni). true.  
`?- padre(mario, X). X = gianni.`

Oppure:

`?- nonno(mario, anna). true.`

Qui Prolog ha usato i fatti e la regola per rispondere.

---

## 5. Unificazione

L’unificazione è l’algoritmo con cui Prolog prova a **rendere uguali due termini**.

- Funziona con sostituzioni di variabili.
    
- È alla base della risoluzione dei predicati.
    

Esempi:

`?- X = mario.
`X = mario.  
`?- padre(mario, X) = padre(mario, gianni). 
`X = gianni.  
`?- padre(mario, X) = padre(gianni, luca). 
`false.`

---

## 6. Backtracking

Se ci sono più soluzioni, Prolog esplora tutte le possibilità.

Esempio:

`colore(rosso). 
`colore(verde). 
`colore(blu).  
`?- colore(X). 
`X = rosso ; 
`X = verde ; 
`X = blu.`

Prolog restituisce **tutte le soluzioni possibili**, una alla volta.

---

## 7. Esercizi pratici

👉 Crea un file `famiglia.pl` con:

`padre(mario, gianni). padre(gianni, luca). padre(luca, anna).  nonno(X,Y) :- padre(X,Z), padre(Z,Y).`

Poi prova queste query:

1. `?- padre(mario, gianni).`
    
2. `?- padre(mario, X).`
    
3. `?- nonno(mario, anna).`
    
4. `?- nonno(gianni, anna).`
    

---

## 8. Riassunto veloce

- **Fatti** = cose vere.
    
- **Regole** = definizioni logiche.
    
- **Query** = domande a Prolog.
    
- **Unificazione** = rende uguali due termini con sostituzioni.
    
- **Backtracking** = esplora tutte le soluzioni possibili.
    
    
    
    # 📘 Lezione 15 settembre – Liste e ricorsione

## 1. Liste in Prolog

Le liste sono strutture fondamentali, scritte tra **[ ]**.  
Esempi:

`[]                % lista vuota 
`[1,2,3]           % lista di numeri 
`[a,b,c]           % lista di atomi 
`[1, pippo, X]     % lista mista con variabile`

Si possono anche scrivere come **testa | coda**:

`[H|T]`

- `H` = primo elemento (head).
    
- `T` = resto della lista (tail).
    

Esempi:

`?- [H|T] = [1,2,3]. 
`H = 1, T = [2,3].  
`?- [H|T] = [a]. 
`H = a, T = [].`

---

## 2. Predicati built-in per le liste

I principali che il prof ti lascia usare:

- `member(X,L)` → vero se `X` appartiene a `L`.
    
- `append(L1,L2,L3)` → unisce due liste e le mette in L3.
    
- `length(L,N)` → vero se `N` è la lunghezza della lista `L`.
    
- `reverse(L,R)` → vero se `R` è la lista `L` al contrario.
    

Esempi:

`?- member(b, [a,b,c]). true.  
`?- append([1,2], [3,4], X). X = [1,2,3,4].  
`?- length([a,b,c], N). N = 3.  
`?- reverse([1,2,3], R). R = [3,2,1].`

---

## 3. Ricorsione sulle liste

Molti predicati si implementano **ricorsivamente**:

- Caso base → lista vuota `[]`.
    
- Caso ricorsivo → lista `[H|T]`.
    

### Esempio: definire `my_length/2`

`my_length([], 0).                     % Caso base my_length([_|T], N) :-                % Caso ricorsivo     my_length(T, N1),     N is N1 + 1.`

In Prolog `_` è la **variabile anonima**, cioè: “qui c’è qualcosa, ma non mi interessa”.
Prova:

`?- my_length([a,b,c], N). N = 3.`

---

### Esempio: definire `my_member/2`

`my_member(X, [X|_]).                  % Caso 1: X è la testa my_member(X, [_|T]) :-                % Caso 2: cerca nella coda     my_member(X, T).`

Prova:

`?- my_member(2, [1,2,3]). true.  
`?- my_member(4, [1,2,3]). false.`

---

### Esempio: definire `my_append/3`

`my_append([], L, L).                  % Caso base my_append([H|T], L2, [H|R]) :-        % Caso ricorsivo     my_append(T, L2, R).`

Prova:

`?- my_append([1,2], [3,4], X). 
`X = [1,2,3,4].`

---

## 4. Esercizi pratici

👉 Prova a scrivere questi predicati da solo:

>[!tip]- 1. `somma_lista(Lista, Somma)` → somma tutti i numeri in una lista.
> 
> ```prolog
> somma_lista([],0).
> somma_lista([H|T],S) :-
>     somma_lista(T,S1),  S is H+S1.
> ```

>[!tip]- 2. `conta_occorrenze(X, Lista, N)` → conta quante volte X appare.
> ```prolog
> conta_occorrenze(X,[],0).
> conta_occorrenze(X,[X|T],N):-
>     conta_occorrenze(X,T,N1), N is N1+1.
> conta_occorrenze(X,[H|T],N):-
>     conta_occorrenze(X,T,N). 
> ```

>[!tip]- 3. `maggiore_di(Lista, N, Filtrata)` → restituisce solo gli elementi > N.
> 
> ```prolog
> maggiore_di([], N, []).
> maggiore_di([X|T],N,R):-
>     X>N,
>      maggiore_di(T,N,L), 
>        append([X],L,R).
>     
> maggiore_di([X|T],N,R):-
>     X=<N,
>      maggiore_di(T,N,R).
> ```
> 

_(Sono gli scheletri che userai più avanti per gli esercizi sugli esami.)_

---

## 5. Riassunto veloce

- Le liste sono `[ ]` o `[H|T]`.
    
- `member/2`, `append/3`, `length/2`, `reverse/2` → strumenti fondamentali.
    
- Quasi tutto si fa con ricorsione:
    
    - Caso base: lista vuota.
        
    - Caso ricorsivo: `[H|T]`.

# 📘 Lezione 16 settembre – Strutture e termini complessi

## 1. Che cos’è un termine in Prolog

In Prolog tutto è un **termine**.  
Esistono diversi tipi di termini:

1. **Numeri** → es. `3`, `4.5`.
    
2. **Atomi** → simboli che iniziano con lettera minuscola o scritti tra apici: `rosso`, `pippo`, `'Ciao'`.
    
3. **Variabili** → iniziano con lettera maiuscola o `_`: `X`, `Persona`.
    
4. **Liste** → es. `[a,b,c]`, che in realtà sono una notazione speciale.
    
5. **Strutture (o termini complessi)** → hanno un **nome** e degli **argomenti**:
    
    `nome(arg1, arg2, ..., argN)`
    

Esempi di strutture:

`mangia(cavallo, biada). ama(romeo, giulietta). colore(auto, rosso).`

---

## 2. Funtore e arità

Quando parliamo di strutture, dobbiamo distinguere due concetti fondamentali:

- **Funtore** → è il **nome** della struttura.
    
    - In `mangia(cavallo, biada)` il funtore è `mangia`.
        
    - In `ama(romeo, giulietta)` il funtore è `ama`.
        
- **Arity (arità)** → è il **numero di argomenti** della struttura.
    
    - `mangia(cavallo, biada)` ha arità 2.
        
    - `colore(auto, rosso, vecchia)` ha arità 3.
        
    - `padre(mario)` ha arità 1.
        

In Prolog si scrive spesso “funtore/aritá” per identificare un predicato:

- `mangia/2` → significa “il predicato mangia con 2 argomenti”.
    
- `padre/1` → significa “il predicato padre con 1 argomento”.
    

---

## 3. Unificazione tra strutture

Prolog può **unificare** due strutture **solo se hanno lo stesso funtore e la stessa arità**.  
Se i nomi o il numero di argomenti non coincidono, fallisce.

Esempi:

`?- mangia(X, biada) = mangia(cavallo, Y). X = cavallo, Y = biada.`

Qui entrambe le strutture hanno:

- funtore = `mangia`
    
- arità = 2
    

Quindi Prolog le fa combaciare unificando `X = cavallo` e `Y = biada`.

---

Altro esempio:

`?- mangia(cavallo, biada) = mangia(ragno, rosmarino). false.`

Qui il funtore è lo stesso (`mangia`), l’arità è la stessa (`2`),  
ma gli argomenti non si possono far coincidere → quindi fallisce.

---

Altro caso:

`?- mangia(cavallo, biada) = ama(romeo, giulietta). false.`

Qui addirittura il **funtore cambia** (`mangia` vs `ama`), quindi non c’è speranza di unificazione.

---

## 4. Predicato `functor/3`

Prolog ha un predicato built-in che permette di “analizzare” una struttura:

`functor(Term, Funtore, Arity).`

Esempi:

`?- functor(mangia(cavallo, biada), F, A). F = mangia, A = 2.  
`?- functor(ama(romeo, giulietta), F, A). F = ama, A = 2.`

Quindi puoi controllare se due termini hanno lo stesso funtore e arità:

`stessa_firma(T1, T2) :-     
`functor(T1, F, A),     
`functor(T2, F, A).`

---

## 5. Strutture come alberi

Le strutture possono essere viste come **alberi**:

- il **funtore** è la radice,
    
- gli **argomenti** sono i sottoalberi.
    

Esempio:  
`mangia(cavallo, biada)` → albero con radice `mangia` e due figli `cavallo` e `biada`.

Questa idea è utile per esercizi tipo “due alberi hanno la stessa forma?”.

### Esempio: stessa struttura

`stessa_struttura(nil, nil). 
`stessa_struttura(nodo(_,SX1,DX1),nodo(_,SX2,DX2)) :-     
`stessa_struttura(SX1, SX2),     
`stessa_struttura(DX1, DX2).`

Uso:

`?- stessa_struttura(nodo(1,nil,nil), nodo(a,nil,nil)). true.  
`?-stessa_struttura(nodo(1,nil,nil),nodo(a,nil,nodo(b,nil,nil))). false.`

---

## 6. Esercizi pratici

>[!tip]- 1. Definisci `stessa_arita(T1,T2)` → vero se due termini hanno lo stesso numero di argomenti.
> ``` prolog
> stessa_arita(T1,T2):-
>     functor(T1,_,A),functor(T2,_,A2),
>     A=A2.
> ```
> 

    
>[!tip]- 2. Definisci `stesso_funtore(T1,T2)` → vero se due termini hanno lo stesso nome.
> ```prolog
> stesso_funtore(T1,T2):-
>     functor(T1,F,_),functor(T2,F1,_),
>     F=F1.
> ```
    
>[!tip]- 3. Definisci `foglia/1` per un albero binario del tipo `nodo(Val, nil, nil)`.
> 
> ```prolog
> foglia(nodo(_,nil,nil)).
> ```
> 
    
	
>[!tip]- 1. Definisci `conta_nodi(T, N)` che conta i nodi di un albero binario.
> ```prolog
> conta_nodi(nil,0).
> conta_nodi(nodo(_,nil,nil),1).
> conta_nodi(nodo(_,SX,DX),N):-
>     conta_nodi(SX,N1),
> 	conta_nodi(DX,N2),
>     N is N1+N2+1.
> 
> ```
---

## 7. Riassunto

- Un **termine complesso** è `funtore(arg1,...,argN)`.
    
- **Funtore** = nome del predicato.
    
- **Arity** = numero di argomenti.
    
- Due termini si unificano solo se hanno stesso funtore e arità.
    
- Con `functor/3` puoi estrarre funtore e arità da un termine.
    
- Le strutture si possono vedere come **alberi**, e si trattano con ricorsione.
    

---

👉 Domani (17 settembre) vediamo **fail e cut**: due strumenti per gestire il **backtracking** di Prolog e simulare il `not`.





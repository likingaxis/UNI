# 📑 Linea guida Prolog – Esercizi e Comandi

## 1. Predicati built-in per il compito
- `append(L1,L2,L3)` → unisce due liste: `L3 = L1 + L2`.  
- `atom(A)` → vero se `A` è un atomo (es. `a`, `pippo`).  
- `number(A)` → vero se `A` è un numero.  
- `member(Elem,L)` → vero se `Elem` appartiene alla lista `L`.  
- `list(L)` → vero se `L` è una lista.  
- `reverse(L,Lrev)` → vero se `Lrev` è la lista `L` al contrario.  
- `length(L,N)` → vero se `N` è la lunghezza di `L`.  

---

## 2. Esercizi sui codificatori
### 2.1. Codifica 1 – Invertire le parole
```prolog
codifica1(L,L1):-
    string_codes(L,T),
    dividiparole(T,R),
    invertiparole(R,C),
    unisciparole(C,S),
    string_codes(L1,S).
```

### 2.2. Codifica 2 – Scambiare primo/ultimo carattere
```prolog
codifica2(L,L1):-
    string_codes(L,T),
    dividiparole(T,R),
    invertiparole(R,C),
    passaparole(C,D),
    unisciparole(D,S),
    string_codes(L1,S).
```

### 2.3. Codifica 3 – Invertire prima/ultima parola
```prolog
codifica3(L,L1):-
    string_codes(L,T),
    dividiparole(T,R),
    invertiparole(R,C),
    passaparole(C,D),
    invertilettere(D,A),
    unisciparole(A,S),
    string_codes(L1,S).
```

---

## 3. Esame – Decodifica messaggio
- Predicato principale: `decodifica_messaggio/2`  
- Predicati ausiliari: `dividiparole`, `prendiparole`, `lunghezza_messaggio`, `conta32`, `maxlen`, `predicatoPrincipe`  

---

## 4. Esame – Codice grafo
### 4.1. Parsing frasi con DCG
- Pattern:  
  - `X si nutre di Y`  
  - `X mangia Y`  
  - `il cibo del X e la Y`

### 4.2. Costruzione grafo
- Predicato principale: `grafo/1`  
- Inserimento frasi: `asserisciFrasi/1`  

---

## 5. Esercizi vari
### 5.1. Operatori logici
```prolog
:- op(700, fy, not).
not(P):- P,!,fail.
not(_).
```

### 5.2. Operatori personalizzati
```prolog
:- op(700, yfx, ha).
:- op(500, yfx, di).
:- op(300, fx, il).
:- op(300, fx, la).

mario ha la macchina di dario.
giovanni ha il cestino di mario.
```

### 5.3. Massimi
```prolog
max(A,B,A):- number(A), number(B), A > B.
max(A,B,B):- number(A), number(B), B > A.

maxlist([A],A).
maxlist([A|T],A):- maxlist(T,B), A >= B.
maxlist([A|T],B):- maxlist(T,B), B > A.
```

### 5.4. Implementazione manuale di reverse e append
```prolog
reversed([],[]).
reversed([H|T],X):- reversed(T,Y), append2(Y,[H],X).

append2([],Z,Z).
append2([H|T],Y,[H|Z]):- append2(T,Y,Z).
```

---

## 6. Grafi
### 6.1. Path
```prolog
edge(a,b). edge(b,c). edge(c,d). edge(d,e).
path(X,Z):- edge(X,Z).
path(X,Y):- edge(X,Z), path(Z,Y).
```

### 6.2. DFS (profondità)
- `solve/2` – versione base  
- `solve2/2` – evita cicli  
- `solve3/3` – profondità limitata  

### 6.3. BFS (ampiezza)
- `visitabfs/2`  
- `solve4/2` con `breadthfirst`  


### DECODIFICATORI
% Student exercise profile
:- set_prolog_flag(occurs_check, error).        % disallow cyclic terms
:- set_prolog_stack(global, limit(8 000 000)).  % limit term space (8Mb)
:- set_prolog_stack(local,  limit(2 000 000)).  % limit env

%X=elemento da cercare, N=posizione in cui si trova X nella lista, L=lista in cui cercare X,
%L1=gli elementi di L a sinistra di X (X escluso), L2=gli elementi di L a destra di X (X escluso)
elemAt(X,N,[X|R],[],R,N).
elemAt(X,N,[K|R],[K|R1],R2,Count):- %Count deve essere inizializzato a 0
    Count2 is Count+1,
    elemAt(X,N,R,R1,R2,Count2).

% per ognuno dei predicati worker, la Stringa deve contenere uno spazio a fine parola, ad es: Stringa=["mario rossi "]
decodificatore_1_worker(Stringa,StringaAggiustata):-
    string_codes(Stringa,X),
    decodificatore_1(X,[],StringaAggiustata).

decodificatore_2_worker(Stringa,StringaAggiustata):-
    string_codes(Stringa,X),
    decodificatore_2(X,[],StringaAggiustata).

decodificatore_3_worker(Stringa,StringaAggiustata):-
    string_codes(Stringa,X),
    decodificatore_3(X,[],StringaAggiustata).
decodificatore_1([],Acc,Stringa_nuova):- 
    string_codes(Stringa_nuova,Acc), !.

decodificatore_1(Chars,Acc,Stringa_nuova):-
    elemAt(32,_,Chars,L,D,0),
    aggiusta_stringa_1(L,NewL),
    append(NewL,[32],NewerL),
    append(Acc,NewerL,Acc2),
    decodificatore_1(D,Acc2,Stringa_nuova).

aggiusta_stringa_1(Chars,CharsAggiustati):-
    reverse(Chars,CharsAggiustati).

decodificatore_2([],Acc,Stringa_nuova):-
    string_codes(Stringa_nuova,Acc), !.

decodificatore_2(Chars,Acc,Stringa_nuova):-
    elemAt(32,_,Chars,L,D,0),
    aggiusta_stringa_2(L,NewL),
    append(NewL,[32],NewerL),
    append(Acc,NewerL,Acc2),
    decodificatore_2(D,Acc2,Stringa_nuova).

aggiusta_stringa_2(Chars,CharsAggiustati):-
    reverse(Chars,CharsNuovi),
    swapfl(CharsNuovi, CharsAggiustati).

%Acc è una lista di liste di numeri
decodificatore_3([],Acc,Stringa_nuova):-
    swapfl(Acc,NewAcc),
    estrai_caratteri(NewAcc,[],Chars), %chars è un unica lista di numeri
    string_codes(Stringa_nuova,Chars).
%chars è una lista di interi
decodificatore_3(Chars,Acc,Stringa_nuova):-
    elemAt(32,_,Chars,L,D,0),
    aggiusta_stringa_2(L,NewL),
    append(NewL,[32],NewerL),
    append(Acc,[NewerL],Acc2), %così facendo Acc sarà una lista di liste
    decodificatore_3(D,Acc2,Stringa_nuova).

estrai_caratteri([],Acc,Acc).
%H è una lista di numeri
estrai_caratteri([H|T],Acc,Chars):-
    append(Acc,H,NewAcc),
    estrai_caratteri(T,NewAcc,Chars).
    

swapfl([First|Middle1], List2) :- %inverte il primo ed ultimo elemento della lista
    append(Middle, [Last], Middle1),
    append([Last|Middle], [First], List2).

    
    
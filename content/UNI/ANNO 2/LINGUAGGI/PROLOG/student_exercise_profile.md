# Student Exercise Profile

```prolog
% Impostazioni di configurazione Prolog
:- set_prolog_flag(occurs_check, error).        % disallow cyclic terms
:- set_prolog_stack(global, limit(8 000 000)).  % limit term space (8Mb)
:- set_prolog_stack(local,  limit(2 000 000)).  % limit env
```

## Predicato `elemAt/6`

```prolog
% elemAt(X, N, L, L1, L2, Count)
% X = elemento da cercare
% N = posizione in cui si trova X nella lista
% L = lista in cui cercare X
% L1 = gli elementi di L a sinistra di X (X escluso)
% L2 = gli elementi di L a destra di X (X escluso)

elemAt(X, N, [X|R], [], R, N).
elemAt(X, N, [K|R], [K|R1], R2, Count) :-
    Count2 is Count + 1,
    elemAt(X, N, R, R1, R2, Count2).
```

## Worker: `decodificatore_1_worker/2`

```prolog
% La Stringa deve contenere uno spazio a fine parola, es: ["mario rossi "]
decodificatore_1_worker(Stringa, StringaAggiustata) :-
    string_codes(Stringa, X),
    decodificatore_1(X, [], StringaAggiustata).
```

### `decodificatore_1/3` e `aggiusta_stringa_1/2`

```prolog
decodificatore_1([], Acc, Stringa_nuova) :- 
    string_codes(Stringa_nuova, Acc), !.

decodificatore_1(Chars, Acc, Stringa_nuova) :-
    elemAt(32, _, Chars, L, D, 0),
    aggiusta_stringa_1(L, NewL),
    append(NewL, [32], NewerL),
    append(Acc, NewerL, Acc2),
    decodificatore_1(D, Acc2, Stringa_nuova).

aggiusta_stringa_1(Chars, CharsAggiustati) :-
    reverse(Chars, CharsAggiustati).
```

## Worker: `decodificatore_2_worker/2`

```prolog
decodificatore_2_worker(Stringa, StringaAggiustata) :-
    string_codes(Stringa, X),
    decodificatore_2(X, [], StringaAggiustata).
```

### `decodificatore_2/3` e `aggiusta_stringa_2/2`

```prolog
decodificatore_2([], Acc, Stringa_nuova) :-
    string_codes(Stringa_nuova, Acc), !.

decodificatore_2(Chars, Acc, Stringa_nuova) :-
    elemAt(32, _, Chars, L, D, 0),
    aggiusta_stringa_2(L, NewL),
    append(NewL, [32], NewerL),
    append(Acc, NewerL, Acc2),
    decodificatore_2(D, Acc2, Stringa_nuova).

aggiusta_stringa_2(Chars, CharsAggiustati) :-
    reverse(Chars, CharsNuovi),
    swapfl(CharsNuovi, CharsAggiustati).
```

## Worker: `decodificatore_3_worker/2`

```prolog
decodificatore_3_worker(Stringa, StringaAggiustata) :-
    string_codes(Stringa, X),
    decodificatore_3(X, [], StringaAggiustata).
```

### `decodificatore_3/3`, `estrai_caratteri/3` e `swapfl/2`

```prolog
% Acc è una lista di liste di numeri
decodificatore_3([], Acc, Stringa_nuova) :-
    swapfl(Acc, NewAcc),
    estrai_caratteri(NewAcc, [], Chars), % chars è una singola lista di numeri
    string_codes(Stringa_nuova, Chars).

decodificatore_3(Chars, Acc, Stringa_nuova) :-
    elemAt(32, _, Chars, L, D, 0),
    aggiusta_stringa_2(L, NewL),
    append(NewL, [32], NewerL),
    append(Acc, [NewerL], Acc2), % Acc diventa lista di liste
    decodificatore_3(D, Acc2, Stringa_nuova).

% Estrazione dei caratteri da lista di liste
estrai_caratteri([], Acc, Acc).
estrai_caratteri([H|T], Acc, Chars) :-
    append(Acc, H, NewAcc),
    estrai_caratteri(T, NewAcc, Chars).

% swapfl/2: inverte il primo ed ultimo elemento della lista
swapfl([First|Middle1], List2) :-
    append(Middle, [Last], Middle1),
    append([Last|Middle], [First], List2).
```

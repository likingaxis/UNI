# 📘 Lezione 17 settembre – `fail`, `cut` e il `not`

## 1. Backtracking in Prolog (ripasso veloce)

- Quando fai una query, Prolog cerca soluzioni.
    
- Se trova una soluzione, la propone.
    
- Se chiedi altre (`;`), Prolog **torna indietro (backtracking)** e cerca altre strade.
    

Esempio:

`colore(rosso). colore(verde). colore(blu).  
`?- colore(X). X = rosso ; X = verde ; X = blu.`

---

## 2. Il predicato `fail`

- `fail/0` è un predicato che **fallisce sempre**.
    
- Serve per forzare Prolog a cercare altre soluzioni.
    

Esempio:

`stampa_colore :-     
`colore(X),     write(X), nl,     fail.     % forza backtracking`

Uso:

`?- stampa_colore. rosso verde blu false.`

📌 Qui `fail` obbliga Prolog a continuare a cercare altri `colore(X)`.  
Quando non ne trova più → `false`.  
👉 `fail` viene spesso usato per “fare tutte le soluzioni” (es. stampa, conteggio).
- `write(X)`  
→ stampa a video il valore di `X`.  
→ Se `X = rosso`, stampa `rosso`.
- `nl`  
→ va a capo (“new line”).

---

## 3. Il predicato `cut (!)`

- `!/0` è chiamato **cut** (taglio).
    
- Serve per **bloccare il backtracking** oltre un certo punto.
    

Esempio:

`massimo(X,Y,X) :- X >= Y, !. 
`massimo(X,Y,Y).`

Cosa succede:

- Se `X >= Y`, allora la prima regola è vera e il `!` impedisce a Prolog di provare la seconda regola.
    
- Se `X < Y`, la prima regola fallisce e Prolog passa alla seconda.
    

Uso:

`?- massimo(5,3,R). R = 5.  ?- massimo(2,7,R). R = 7.`

Senza cut, Prolog proverebbe comunque entrambe le regole e magari darebbe più soluzioni inutili.

---

## 4. Il `not` in Prolog

Prolog non ha un `not` nativo (logica classica ≠ logica di Prolog).  
Però si può **simulare** con `cut` e `fail`:

`not(P) :- P, !, fail.   % se P è vero → fallisci not(_).                 % se P è falso → questa regola va in porto`
```
not(P):- 
    P, !, fail. 
not(_).
```

Esempi:

`?- not(rosso = verde). true.  ?- not(rosso = rosso). false.`

📌 Attenzione: questo `not` è il cosiddetto **negation as failure**:  
“qualcosa è falso se non si può dimostrare che è vero”.

---

## 5. Cut rosso vs cut verde

In teoria si distinguono due tipi di cut:

- **Cut rosso** → cambia il significato logico del programma (forza una scelta, può eliminare soluzioni corrette).
    
- **Cut verde** → serve solo a rendere più efficiente il programma (non cambia il significato).
    

Esempio cut verde (ottimizzazione):

`pari(X) :- X mod 2 =:= 0, !. pari(_).`

Qui il cut evita di controllare altre regole inutili.

---

## 6. Esercizi pratici

>[!tip]- 1. Definisci `massimo/3` con cut (già visto).
> ``` prolog
> massimo(X,Y,X):-
>     X>=Y, !.
> massimo(_,Y,Y).
> ```

    
>[!tip]- 2. Definisci `assoluto(X,Y)` che calcola il valore assoluto usando cut.
>     
> ```prolog
>     assoluto(X,X) :- X >= 0, !. 
>     assoluto(X,Y) :- Y is -X.
> ```
> 
    

>[!tip]- 3. Implementa `not/1` con cut e fail.
> ```prolog
> not(P):- 
>     P, !, fail. 
> not(_).
> ```
> 

---

## 7. Riassunto

- **`fail`** → fallisce sempre, utile per forzare il backtracking.
    
- **`cut`** → blocca il backtracking, serve per ottimizzare o per forzare scelte.
    
- **`not`** → si implementa con cut + fail (`negation as failure`).
    
- Usare cut e fail richiede attenzione: possono cambiare la logica del programma.
# 📘 Lezione 18 settembre – `assert`, `retract` e `univ`

## 1. La base di conoscenza in Prolog

Quando scrivi un programma Prolog, definisci una **base di conoscenza (KB)** con:

- **Fatti** → cose sempre vere.
    
- **Regole** → relazioni dedotte dai fatti.
    

Ma Prolog permette anche di **aggiungere o rimuovere** fatti e regole **durante l’esecuzione**.

---

## 2. `assert/1` – aggiungere fatti o regole

- `assert(X)` aggiunge il fatto/regola `X` alla base di conoscenza.
    
- `asserta(X)` lo aggiunge in testa, `assertz(X)` in coda (di solito non importa).
    

Esempio:

`?- assert(padre(pippo, pluto)). true.  ?- padre(pippo, Y). Y = pluto.`

📌 Dopo la query, la base di conoscenza ha un fatto in più.

---

## 3. `retract/1` – rimuovere fatti o regole

- `retract(X)` rimuove la prima clausola che unifica con `X`.
    
- Se ci sono più fatti uguali, puoi richiamare `;` per rimuoverne altri.
    

Esempio:

`?- assert(padre(topolino, minnie)). true.  ?- retract(padre(topolino, minnie)). true.  ?- padre(topolino, minnie). false.`

---

## 4. Uso insieme di `assert` e `retract`

Puoi aggiornare la KB “al volo”.  
Esempio: contatore che si incrementa:

`:- dynamic contatore/1. contatore(0).  incrementa :-     retract(contatore(N)),     N1 is N + 1,     assert(contatore(N1)).`

Uso:

`?- incrementa. true.  ?- incrementa. true.  ?- contatore(X). X = 2.`

📌 `:- dynamic nome/Arity.` serve a dire a Prolog che quel predicato può essere modificato.

---

## 5. L’operatore =.. (univ)

=.. permette di convertire un termine in una **lista** con il funtore e gli argomenti.

Sintassi:

Term =.. Lista

- Da termine a lista:
    
    `?- mangia(cavallo, biada) =.. L. L = [mangia, cavallo, biada].`
    
- Da lista a termine:
    
    `?- T =.. [ama, romeo, giulietta]. T = ama(romeo, giulietta).`
    

📌 È utile quando vuoi “manipolare” i predicati come dati.

---

## 6. `listing/1` (solo per curiosità)

`listing/1` stampa tutte le definizioni di un predicato.  
Esempio:

`?- listing(padre/2). padre(mario, gianni). padre(gianni, luca). true.`

Non è fondamentale per l’esame, ma utile per il debug.

---

## 7. Esercizi pratici

1. Aggiungi un fatto dinamico con `assert` e verifica che sia interrogabile.
    
2. Rimuovi un fatto con `retract`.
    
3. Scrivi un predicato `aggiungi_amico(X,Y)` che fa `assert(amico(X,Y))`.
    
4. Scrivi un predicato `toglie_amico(X,Y)` che fa `retract(amico(X,Y))`.
    
5. Usa =.. per trasformare `somma(2,3,5)` in `[somma,2,3,5]`.
    
6. Usa = .. per costruire dinamicamente un fatto tipo `studente(pippo,30)` a partire da una lista.
    

---

## 8. Riassunto

- **`assert/1`** → aggiunge fatti o regole alla KB.
    
- **`retract/1`** → rimuove fatti o regole.
    
- = .. univ → converte un termine ↔ lista `[funtore, arg1, arg2,…]`.
    
- **`listing/1`** → stampa i predicati (solo di supporto).

# 📘 Lezione 19 settembre – Definite Clause Grammars (DCG)

## 1. Perché servono le DCG

- Senza DCG, analizzare frasi significa lavorare manualmente con liste di simboli: `[il,cavallo,mangia,la,biada]`.
    
- Con DCG puoi scrivere regole grammaticali più **leggibili** e lasciare a Prolog il lavoro di gestire le liste.
    
- Sono molto usate per parsing, linguaggio naturale, compilatori, trasformazioni di testo.
    
 
---

## 2. Sintassi base

Una regola DCG si scrive con `-->` invece di `:-`.  
Esempio:

`frase --> soggetto, predicato.  
`soggetto --> [cavallo]. 
`soggetto --> [ragno].  
`predicato --> [mangia, biada]. 
`predicato --> [mangia, rosmarino].`

Uso:

`?- frase([cavallo,mangia,biada], []). true.  ?- frase([ragno,mangia,rosmarino], []). true.`

📌 Una regola `p --> q,r.` equivale a:

`p(L0,L2) :- q(L0,L1), r(L1,L2).`

Quindi le DCG sono solo **zucchero sintattico** per gestire liste di simboli.

---

## 3. Esempio: grammatica semplice

Costruiamo una grammatica che riconosce frasi del tipo _“il cavallo mangia la biada”_.

`frase --> articolo, nome, verbo, articolo, nome.  
`articolo --> [il]. 
`articolo --> [la].  
`nome --> [cavallo]. 
`nome --> [biada]. 
`nome --> [ragno]. 
`nome --> [rosmarino]. 
`verbo --> [mangia].`

Uso:

`?- frase([il,cavallo,mangia,la,biada], []). true.  
`?- frase([il,ragno,mangia,rosmarino], []). true.`

---

## 4. DCG con variabili (estrazione di significato)

Possiamo “estrarre” la struttura logica da una frase.

`frase(mangia(Soggetto, Oggetto)) -->      articolo, nome(Soggetto), verbo, articolo, nome(Oggetto).  
`articolo --> [il]. articolo --> [la].  
`nome(cavallo) --> [cavallo]. 
`nome(biada)   --> [biada]. 
`nome(ragno)   --> [ragno]. 
`nome(rosmarino) --> [rosmarino].  
`verbo --> [mangia].`

Uso:

`?- frase(X, [il,cavallo,mangia,la,biada], []). 
`X = mangia(cavallo, biada).  
`?- frase(X, [il,ragno,mangia,rosmarino], []). 
`X = mangia(ragno, rosmarino).`

📌 Qui DCG non solo controlla la frase, ma costruisce direttamente il fatto logico.

---

## 5. DCG con ricorsione

Le DCG gestiscono anche frasi composte.  
Esempio: più nomi di fila → lista:

`nomi([N|Ns]) --> nome(N), nomi(Ns). nomi([])     --> [].  nome(cavallo)   --> [cavallo]. nome(biada)     --> [biada].`

Uso:

`?- nomi(L, [cavallo,biada,cavallo], []). L = [cavallo, biada, cavallo].`

---

## 6. Dove servono per l’esame

- Esercizio **rete alimentare (09/07)**: frasi tipo _“Il cavallo si nutre di biada”_ → `mangia(cavallo,biada)`.
    
- Con DCG puoi definire più regole per catturare tutte le varianti (mangia, si nutre di, il cibo è…).
    

Esempio:

`frase(mangia(Soggetto, Oggetto)) -->      [il], nome(Soggetto), [mangia], [la], nome(Oggetto).  frase(mangia(Soggetto, Oggetto)) -->      [il], nome(Soggetto), [si, nutre, di], nome(Oggetto).`

---

## 7. Esercizi pratici

1. Scrivi una DCG che riconosce frasi tipo:
    
    - “il cane ama il gatto” → `ama(cane,gatto)`
        
    - “il topo odia il formaggio” → `odia(topo,formaggio)`
        
2. Scrivi una DCG che riconosce una lista di numeri `[1,2,3]` e la traduce in `somma(6)`.
    
3. Estendi la DCG dell’esercizio alimentare per riconoscere almeno **3 modi diversi** di esprimere la stessa relazione.
    

---

## 8. Riassunto

- DCG = notazione più leggibile per analizzare stringhe/lista di simboli.
    
- Sintassi: `-->`.
    
- Dietro le quinte: `p(L0,L2) :- q(L0,L1), r(L1,L2).`
    
- Con le variabili puoi trasformare frasi in **strutture logiche**.

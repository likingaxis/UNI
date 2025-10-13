comandi utilizzabili per il compito:
append(L1,L2,L3) → unisce due liste: L3 = L1 + L2. atom(A) → vero se A è un atomo (es. a, pippo). number(A) → vero se A è un numero. member(Elem,L) → vero se Elem appartiene alla lista L. list(L) → vero se L è una lista. reverse(L,Lrev) → vero se Lrev è la lista L al contrario. length(L,N) → vero se N è la lunghezza di L.

### Esame codificatori
```prolog
%esame sui codificatori 3 codifiche diverse
%codifica 1 chiede di invertire le parole
%codifica 2 chiede di prendere codifica 1 e invertire il primo e l'ultimo carattere di ogni parola
%codifica 3 chiede di prendere codifica 2 e invertire prima e ultima parola



%dividiparole semplicemente seziona la stringa in sottostringhe tagliando il carattere 32 = spazio in codice ascii
dividiparole([],[]).


dividiparole([32|T],L):-!,  %questo in particolare serve a escludere parole vuote
    dividiparole(T,L).

dividiparole(L,[Word|Rest]):-
    prendiparole(L,Word,RestoLista),
    dividiparole(RestoLista,Rest).

%prendiparole è ausiliario a dividiparole,
% essenzialmente prende la stringa intera e restituisce come secondo parametro la parola troncata da 32
prendiparole([],[],[]).

prendiparole([32|T],[],T):-!.

prendiparole([T|L],[T|L2],Rest):-
    prendiparole(L,L2,Rest).
    

%invertiparole molto semplicemente ogni parola della lista di sottoliste (parole)
invertiparole([],[]).

invertiparole([H|T],[H1|T1]):-
              reverse(H,H1),
              invertiparole(T,T1).



%unisciparole ricrea la lista iniziale decapsulando le sottoliste e inserendo 32 tra una e l'altra 
unisciparole([],[]).
unisciparole([W],W).

unisciparole([W|Res],L):-
    unisciparole(Res,L1),
    append(W,[32|L1],L).
    
    
%la prima codifica richiesta
codifica1(L,L1):-
    string_codes(L,T),
    dividiparole(T,R),
    invertiparole(R,C),
    unisciparole(C,S),
    string_codes(L1,S).


%tutto cio che è scritto qui sopra serve per codifica1, sotto ci saranno parti aggiuntive per le altre codifiche

%PARTI AGGIUNTIVE PER CODIFICA2:

%invertilettere inverte il primo e l'ultimo elemento della lista passata
invertilettere([_],[_]).
invertilettere([X,Y],[Y,X]).
invertilettere([H|T],[H1|T1]):-
    append(X,[H1],T),
    append(X,[H],T1).
   
%passaparole utilizzato per passare le singole parole a invertilettere
passaparole([],[]).
passaparole([H|T],[H1|L]):-
    passaparole(T,L),
    invertilettere(H,H1).

%CODIFICA2: si comporta come richiesto con l'aggiunta dei predicati
codifica2(L,L1):-
    string_codes(L,T),
    dividiparole(T,R),
    invertiparole(R,C),
    passaparole(C,D),
    unisciparole(D,S),
    string_codes(L1,S).




%CODIFICA3: sfrutta inverti lettere per invertire le parole
codifica3(L,L1):-
    string_codes(L,T),
    dividiparole(T,R),
    invertiparole(R,C),
    passaparole(C,D),
    invertilettere(D,A),
    unisciparole(A,S),
    string_codes(L1,S).



```
### codificatori esame 2
```prolog

decodifica_messaggio(Messaggio,Decodifica):-
    codifica1(Messaggio,B),
    predicatoPrincipe(B,Messaggio2,0),
    string_codes(Decodifica,Messaggio2).


dividiparole([],[]).
dividiparole([32|T],L):-!,
    dividiparole(T,L).
dividiparole(T,[Word|Rest]):-
    prendiparole(T,Word,Restolista),
    dividiparole(Restolista,Rest).

prendiparole([],[],[]).
prendiparole([32|Resto],[],Resto):-!.
prendiparole([H|T],[H|T1],Resto):-
    prendiparole(T,T1,Resto).


codifica1(A,B):-
    string_codes(A,C),
    dividiparole(C,B).



lunghezza_messaggio([],0).
lunghezza_messaggio([_|T],N):-
    lunghezza_messaggio(T,N1),
    N is N1 + 1.


conta32([],0):-!.
conta32([32|T],N):-
    conta32(T,N1),
    N is N1+1,!.
conta32([_|T],N):-
    conta32(T,N),!.




maxlen([],0).
maxlen([P|Ps],M):-
    length(P,L),
    maxlen(Ps,M1),
    M is max(L,M1).


% caso base: se nessuna parola ha una lettera a posizione N, stop
predicatoPrincipe(Messaggio,[],N):-
    maxlen(Messaggio,M),
    N >= M.

% passo ricorsivo
predicatoPrincipe(Messaggio,C,N):-
    % qui so che almeno una parola ha una lettera
    passaparole(Messaggio,H,N),
    N1 is N+1,
    predicatoPrincipe(Messaggio,T,N1),
    append(H,T,C).


    
passaparole([],[],_).
passaparole([Parola|Resto],[H|T],Number):-
    codificatore(Parola,H,Number),
    passaparole(Resto,T,Number).
    
codificatore([],32,_).
codificatore([H|_],H,0).
codificatore([_|T],Letter,Number):-
    Number1 is Number-1,
    codificatore(T,Letter,Number1).

```

### Esame codice grafo
```prolog
/* query example:

codifica1("Il cavallo si nutre di biada

Il cibo del pony e la ciccia

Il pony si nutre di ciccia

Il maile mangia la cicoria

Il ragno si nutre di rosmarino",L).

*/

  
  

:- dynamic mangia/2.

%dividiparole semplicemente seziona la stringa in sottostringhe tagliando il carattere 32 = spazio in codice ascii

dividiparole([],[]).

  
  

dividiparole([32|T],L):-!,  %questo in particolare serve a escludere parole vuote

    dividiparole(T,L).

  

dividiparole(L,[Word|Rest]):-

    prendiparole(L,Word,RestoLista),

    dividiparole(RestoLista,Rest).

  

%prendiparole è ausiliario a dividiparole,

% essenzialmente prende la stringa intera e restituisce come secondo parametro la parola troncata da 32

prendiparole([],[],[]).

  

prendiparole([32|T],[],T):-!.

  

prendiparole([T|L],[T|L2],Rest):-

    prendiparole(L,L2,Rest).

  

convertiparole([],[]).

convertiparole([H|T],[H1|T1]):-

    atom_codes(H2,H),

    downcase_atom(H2,H1),

    convertiparole(T,T1).

  
  

recuperaFrasi([],[]).

recuperaFrasi([H|T],[H1|T1]):-

    string_codes(H,H1),

    recuperaFrasi(T,T1).

  

richiamaDividi([],[]).

richiamaDividi([H|T],[H1|T1]):-

    dividiparole(H,H1),

    richiamaDividi(T,T1).

  

richiamaConverti([],[]).

richiamaConverti([H|T],[H1|T1]):-

    richiamaConverti(T,T1),

    convertiparole(H,H1).

%la prima codifica richiesta

codifica1(L,L1):-

    string_lines(L,A),

    recuperaFrasi(A,B),

    richiamaDividi(B,C),

    richiamaConverti(C,L1),

    grafo(L1).

  

% --- predicato principale ---

estrai_mangia(FraseList, mangia(S,O)) :-

    once(phrase(frase(mangia(S,O)), FraseList)).

  

% --- Regole principali della grammatica ---

frase(F) --> pattern_nutre(F).

frase(F) --> pattern_mangia(F).

frase(F) --> pattern_cibo(F).

  

skip_word --> [_].       % salta una parola qualsiasi

skip_words --> skip_word, skip_words.

skip_words --> [].

  

% --- pattern "X si nutre di Y" ---

pattern_nutre(mangia(S,O)) -->

    skip_words, [S,si,nutre,di,O], skip_words.

  

pattern_mangia(mangia(S,O)) -->

    skip_words, [S,mangia,la,O]|[S,mangia,il,O]|[S,mangia,lo,O]|[S,mangia,gli,O]|[S,mangia,i,O]|[S,mangia,le,O], skip_words.

  

pattern_cibo(mangia(S,O)) -->

    skip_words, [il,cibo,del,S,e,la,O]|[il,cibo,del,S,e,il,O]|[il,cibo,del,S,e,lo,O]|[il,cibo,del,S,e,gli,O]|[il,cibo,del,S,e,le,O]|[il,cibo,del,S,e,i,O], skip_words.

  
  

grafo(L):-

    retractall(mangia(_,_)),

    write('Inizio inserimento frasi nel database...'), nl,

    asserisciFrasi(L).

  

asserisciFrasi([]).

asserisciFrasi([H|T]):-

    ( estrai_mangia(H,C) ->  % se la frase viene parsata correttamente

        assertz(C)

    ;

        true                % altrimenti ignora la frase e continua

    ),

    asserisciFrasi(T).
```
### Codici a caso
num(Number)--> [Number] , {number(Number)}.

f(Ris)--> num(Val1), oper(OP), num(Val2), {P=.. [OP,Val1,Val2], Ris is P}.

oper(+)--> [più].
oper(-)--> [meno].
oper(/)--> [diviso].
oper(*)--> [per].

%query di esempio: f(Ris,[4, per, 8],R).

% DEFINIZIONE DELL'OPERATORE NOT
% espressione della frase "Mary ama tutti gli animali, ma non i serpenti"
% con il predicato likes


:-op(700,fy,not).



not(P):-
    P,!,fail.
not(_).


animal(camaleonte).
animal(pincopallino).
animal(serpente).
snake(serpente).


likes(mary, X):-
    animal(X),
    not snake(X).

%esercizio su ridefinzione operatori per rispondere alla sintassi normale di una frase


:-op(700, yfx, ha).
:-op(500, yfx, di).
:-op(300, fx, il).
:-op(300,fx, la).

mario ha la macchina di dario.
giovanni ha il cestino di mario.
% max= massimo tra due numeri

max(A,B,A):-
    number(A),
    number(B),
    A>B.

max(A,B,B):-
    number(A),
    number(B),
    B>A.

% maxlist= massimo all interno di una lista, 
% ATTENZIONE: in caso di non funzionamento inserire il predicato number come sopra.

maxlist([A],A).

maxlist([A|T],A):-
    maxlist(T,B),
    A>=B.

maxlist([A|T],B):-
    maxlist(T,B),
    B>A.
    
% implementazione fatta a mano di reverse:
% ATTENZIONE: in questo esempio utiliziamo append2 fatto da me
% è possibile utilizzarla con "append" che è built-in

reversed([],[]).

reversed([H|T],X):-
    reversed(T,Y),
    append2(Y,[H],X).


%  implementazione fatta a mano di append

append2([],Z,Z).

append2([H|T],Y,[H|Z]):-
    append2(T,Y,Z).




%  implementazione fatta a mano di append

append2([],Z,Z).

append2([H|T],Y,[H|Z]):-
    append2(T,Y,Z).

edge(a,b).
edge(b,c).
edge(c,d).
edge(d,e).
edge(f,e).
edge(a,e).

path(X,Z):- edge(X,Z).

path(X,Y):-
    edge(X,Z),
    path(Z,Y).
    




%un modo per rappresentare tutte le transizioni di stato
% ATTENZIONE, il modo in cui rappresnetiamo le transizioni
% dipende dal grafo che stiamo rappresentando
% quindi non esiste un modo univoco
s([[A|RA],B,C],[RA,[A|B],C]).
s([[A|RA],B,C],[RA,B,[A|C]]).

s([B,[A|RA],C],[[A|B],RA,C]).
s([B,[A|RA],C],[B,RA,[A|C]]).

s([B,C,[A|RA]],[[A|B],C,RA]).
s([B,C,[A|RA]],[B,[A|C],RA]).


%predicato per trovare l'obbiettivo che cerchiamo
goal(Situation):-
	member([a,b,c], Situation).

%DFS
solve(N,[N]):-
    goal(N).

solve(N,[N|Sol1]):-
    s(N,N1),
    solve(N1,Sol1).

/*
 L’idea che sta alla base di questo tipo di ricerca è la seguente:
Per trovare il percorso che rappresenta la soluzione, Sol, dato un nodo N, ed almeno un nodo obiettivo:
Se N è la l’obiettivo, allora Sol = [N], altrimenti
Se esiste un nodo connesso a N, detto N1, tale che esista una soluzione Sol1 da N1 ad un nodo obiettivo, allora Sol = [N | Sol1]
*/





%un modo per rappresentare tutte le transizioni di stato
% ATTENZIONE, il modo in cui rappresnetiamo le transizioni
% dipende dal grafo che stiamo rappresentando
% quindi non esiste un modo univoco
s([[A|RA],B,C],[RA,[A|B],C]).
s([[A|RA],B,C],[RA,B,[A|C]]).

s([B,[A|RA],C],[[A|B],RA,C]).
s([B,[A|RA],C],[B,RA,[A|C]]).

s([B,C,[A|RA]],[[A|B],C,RA]).
s([B,C,[A|RA]],[B,[A|C],RA]).


%predicato per trovare l'obbiettivo che cerchiamo
goal(Situation):-
	member([a,b,c], Situation).

% DFS VERSIONE 2:
% QUESTA VERSIONE FA SI CHE SI RICORDI IL PERCORSO SVOLTO FIN ORA 
% PER NON TORNARE SU CONFIGURAZIONI GIà VISITATE ED EVITARE UN LOOP
% (attenzione: quando parliamo di configurazioni già visitate parilamo di nodi di un grafo).




solve2( Node, Solution)  :-
  		depthfirst2( [], Node, Solution).

depthfirst2( Path, Node, [Node | Path] )  :-
   	goal( Node).

depthfirst2( Path, Node, Sol) :-
  		s( Node, Node1),
  		not(member( Node1, Path)), 
	 	depthfirst2( [Node | Path], Node1, Sol).

/*
 L’idea che sta alla base di questo tipo di ricerca è la seguente:
Per trovare il percorso che rappresenta la soluzione, Sol, dato un nodo N, ed almeno un nodo obiettivo:
Se N è la l’obiettivo, allora Sol = [N], altrimenti
Se esiste un nodo connesso a N, detto N1, tale che esista una soluzione Sol1 da N1 ad un nodo obiettivo, allora Sol = [N | Sol1]
*/
%visitaBFS grafo 


arco(a,b).
arco(a,c).
arco(a,d).
arco(b,z).
arco(b,x).
arco(c,y).
arco(c,z).
arco(z,s).
arco(s,u).

connessione(X,Y):-
    arco(X,Y).

setog(H,C):-
    setof(Y,connessione(H,Y),C),
    write(C),nl.
setog(_,[]).
    

frontiera([],[]).

frontiera([X],L):-
    setog(X,L).

frontiera([H|T], L):-
    setog(H,C),
    append(C,Z,L),
    frontiera(T,Z).

visitabfs([],[]).



visitabfs(X,L):-
    frontiera(X,C),
    append(C,Y,L),
    visitabfs(C,Y).
    
%visitaBFS grafo 


arco(a,b).
arco(a,c).
arco(a,d).
arco(b,z).
arco(b,x).
arco(c,y).
arco(c,z).
arco(z,s).
arco(s,u).

connessione(X,Y):-
    arco(X,Y).

setog(H,C):-
    setof(Y,connessione(H,Y),C),
    write(C),nl.
setog(_,[]).
    

frontiera([],[]).

frontiera([X],L):-
    setog(X,L).

frontiera([H|T], L):-
    setog(H,C),
    append(C,Z,L),
    frontiera(T,Z).

visitabfs([],[]).



visitabfs(X,L):-
    frontiera(X,C),
    append(C,Y,L),
    visitabfs(C,Y).
    /*
 VISITA BFS DEL GRAFO:
 VERSIONE ADATTATA CON DEI PREDICATI CHE FORMANO DEI FATTI
 
 query tipica: solve4(nodo(start,b),Situation).
*/

nodo(start,a).
nodo(a,b).
nodo(a,c).
nodo(a,d).
nodo(a,e).
nodo(a,f).
nodo(b,c).
nodo(b,f).
nodo(b,e).
nodo(f,c).
nodo(e,c).
nodo(f,h).
nodo(h,m).
nodo(m,n).
nodo(n,y).
nodo(d,k).
nodo(k,y).
nodo(y,z).
nodo(z,x).


goal(nodo(_,x)).


solve4( Start, Solution)  :-
  	breadthfirst( [ [Start] ] , Solution).

breadthfirst( [ [Node | Path] | _] , [Node | Path] )  :-
  	goal(Node).

breadthfirst( [Path | Paths] , Solution)  :-
  	extend( Path, NewPaths),
  	append( Paths, NewPaths, Paths1),
  	breadthfirst( Paths1, Solution).

extend( [nodo(X,Y) | Path], NewPaths)  :-
  	bagof( [nodo(Y,Z), nodo(X,Y) | Path],
         (  nodo(Y,Z), not(member( nodo(Y,Z), [nodo(X,Y) | Path] )) ),
         NewPaths),
  !.

extend( _, [] ).


/*
 L’idea che sta alla base di questo tipo di ricerca è la seguente:
Data una lista di possibili percorsi:
Se la testa della prima lista è un obiettivo, allora quel percorso è la soluzione
Altrimenti rimuovi il primo percorso dalla lista dei candidati, 
genera tutti i percorsi che fanno uno step in più del percorso appena
eliminato e inseriscili in coda alla lista dei percorsi candidati e analizza
il percorso che ora si trova in testa alla lista dei possibili percorsi
*/





%un modo per rappresentare tutte le transizioni di stato
% ATTENZIONE, il modo in cui rappresnetiamo le transizioni
% dipende dal grafo che stiamo rappresentando
% quindi non esiste un modo univoco
s([[A|RA],B,C],[RA,[A|B],C]).
s([[A|RA],B,C],[RA,B,[A|C]]).

s([B,[A|RA],C],[[A|B],RA,C]).
s([B,[A|RA],C],[B,RA,[A|C]]).

s([B,C,[A|RA]],[[A|B],C,RA]).
s([B,C,[A|RA]],[B,[A|C],RA]).


%predicato per trovare l'obbiettivo che cerchiamo
goal(Situation):-
	member([a,b,c], Situation).

% DFS VERSIONE 3:
% QUESTA VERSIONE LIMITà LA PROFONDITà, OVVERO IL NUMERO DI NODI VISITATI




solve3( Node, Solution, Max)  :-
  		depthfirst3( Node, Solution, Max).

depthfirst3( Node, [Node], _)  :-
   	goal( Node).

depthfirst3( Node, [Node | Sol], Maxdepth)  :-
   	Maxdepth > 0,
   	s( Node, Node1),
   	Max1 is Maxdepth - 1,
   	depthfirst3( Node1, Sol, Max1).

/*
 L’idea che sta alla base di questo tipo di ricerca è la seguente:
Per trovare il percorso che rappresenta la soluzione, Sol, dato un nodo N, ed almeno un nodo obiettivo:
Se N è la l’obiettivo, allora Sol = [N], altrimenti
Se esiste un nodo connesso a N, detto N1, tale che esista una soluzione Sol1 da N1 ad un nodo obiettivo, allora Sol = [N | Sol1]
*/


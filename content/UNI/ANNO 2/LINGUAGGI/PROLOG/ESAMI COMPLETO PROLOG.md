
### ESAME 1

Stanno girando sui social media dei messaggi apparentemente senza senso. Sembrano infatti delle sequenze di lettere casuali. Sono evidentemente dei messaggi in codice. Sfruttando la potenza del prolog, si vuole costruire **il codificatore ed il decodificatore** che realizzino queste codifiche:

1. La prima versione di messaggio codificato in è il messaggio originale in cui tutte le parole sono invertite e il loro ordine è mantenuto
    
2. La seconda versione di messaggio codificato è la prima versione di codifica in cui poi ciascuna parola inverte la prima e l’ultima lettera
    
3. La terza versione di codifica è la seconda versione in cui la prima e l’ultima parola sono scambiate
    

---

Si ricorda che esiste il built-in **string_codes(STRING, LIST_OF_CHARS)**

#### SOLUZIONE 1
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



### ESAME 2
Il mondo sta cambiando ed esistono delle specie di animali e di piante più esposte all’inquinamento umano. Onde capire se l’inquinamento umano torna nelle nostre tavole, si vuole costruire una rete i cui nodi sono le specie e la relazione è la relazione di chi mangia chi.

Data la rete, se un animale o pianta è inquinata, il mangiante ad una certa distanza **n** è inquinato **0.87^n**.

Per costruire questa rete, si vuole utilizzare Wikipedia nella quale la relazione è espressa in maniera testuale con frasi del tipo:

- Il cavallo si nutre di biada.
    
- Il cibo del cavallo è la biada.
    
- Il cavallo mangia la biada.
    
- Il ragno si nutre di rosmarino.
    

Si vogliono portare tutte queste frasi alla forma canonica:

- `mangia(cavallo, biada)`
    
- `mangia(ragno, rosmarino)`
    

per costruire la rete di relazione di mangiare delle specie.

Trovare un sistema generale per risolvere la sfida.

#### SOLUZIONE 2

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


### ESAME 3

Si vuole costruire un analizzatore di messaggi nascosti all’interno di sequenze di lettere apparentemente senza senso. Un messaggio di n parole è scritto nella seguente maniera:

- Si metta un indice i = 0
    
- Per ogni parola in sequenza nella frase, si metta parola[i] nella stringa se esiste, spazio se non esiste e si incrementi i di 1
    
- Se esiste almeno una parola in cui parola[i] esiste, si torni al passo precedente
    

Si scriva un predicato prolog:

`lunghezza_messaggio(Messaggio,N)`

che sia vero se N è la lunghezza del Messaggio in numero di parole. Come da bravi decodificatori, si è individuato che in ogni messaggio c’è la preposizione “per”.

Si scriva poi:

`decodifica_messaggio(Messaggio,MessaggioDecodificato)`

che sia vero se MessaggioDecodificato è il messaggio celato dentro Messaggio. Si tenga a mente il predicato precedente.

Decodificare questo messaggio:

`“igspdmicpfla teialea t ann nrmt sgeeoa i na dr oe”`
### SOLUZIONE 3
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


### ESAME 4
Si vis pacem, para bellum”

Vogliamo aiutare l’esercito romano ad essere preparato in caso di attacco per evitargli rischi inutili.  
Abbiamo scoperto che i Daci hanno dei dardi potentissimi ma prevedibili se utilizzati nel campo di battaglia. Infatti, dividendo il campo di battaglia in una griglia di n×n quadrati, si sa che il dardo può colpire il bersaglio su traiettorie orizzontali, verticali o diagonali fino ad una distanza di m quadrati indipendentemente dalla direzione. Conosciamo anche l’arsenale dei Daci e dispongono solo di k di questi dardi micidiali. I dardi possono essere utilizzati solo con la luce del giorno.

I Daci controllano tutta la metà destra del campo di battaglia e siccome i romani hanno delle buone torri di avvistamento mobili, riescono a vedere di notte dove vengono posizionati i dardi micidiali. Possono dunque posizionare agevolmente le loro coorti in posizioni nelle quali possono stare tranquilli per, eventualmente, sferrare il contrattacco.

Dal momento che possiedono un calcolatore a corde che funziona in Prolog, gli serve un programma Prolog che sia in grado di emettere rapidamente la posizione che devono tenere le v coorti romane.

---

Se vi pare più semplice, considerate n=10, k=4, m=6 e v=5. Sarebbe gradita una soluzione parametrica.


### SOLUZIONE 4
% Student exercise profile
:- set_prolog_flag(occurs_check, error).        % disallow cyclic terms
:- set_prolog_stack(global, limit(8 000 000)).  % limit term space (8Mb)
:- set_prolog_stack(local,  limit(2 000 000)).  % limit environment space

%vero se la torre è fuori dalla traiettoria verticale
check_verticale(dardo(XD,YD,M),torre(XD,YT)):-
    DstY is YD-M,
    YT < DstY,!. %sta abastanza sopra
check_verticale(dardo(XD,YD,M),torre(XD,YT)):-
    DstY is YD+M,
    YT > DstY,!. %sta abastanza sotto
check_verticale(dardo(XD,_,_),torre(XT,_)):-
     XD\=XT.

%vero se la torre è fuori dalla traiettoria orizzontale
check_orizzontale(dardo(XD,YD,M),torre(XT,YD)):-
    DstX is XD-M,
    XT < DstX,!.
check_orizzontale(dardo(XD,YD,M),torre(XT,YD)):-
    DstX is XD+M,
    XT > DstX,!.
check_orizzontale(dardo(_,YD,_),torre(_,YT)):-
    YD\=YT.

%vero se la torre NON è fuori dalla traiettoria diagonale
check_diagonale(dardo(XD,YD,M),torre(XT,YT)):-
	Safe is abs(XD-XT),
    Safe =:= abs(YD-YT),
    Safe<M. 

torri([],_).
%vedi se torre è safe per ogni elem. di dardi, poi richiama con TT
torri([Torre|Altre], Dardi) :-
    forall(member(Dardo, Dardi), %forall è vero se la variabile è vera per tutte le condizioni (2° parametro)
           (check_verticale(Dardo, Torre),
            check_orizzontale(Dardo, Torre),
               not(check_diagonale(Dardo,Torre)))),
    torri(Altre, Dardi).

### ESAME 5

Si vuole costruire un analizzatore di messaggi nascosti all’interno di sequenze di lettere apparentemente senza senso.  
Un messaggio di n parole è scritto nella seguente maniera:
- Si metta un indice i = 0  
- Per ogni parola in sequenza nella frase, si metta parola[i] nella stringa se esiste, spazio se non esiste e si incrementi di 1  
- Se esiste almeno una parola in cui parola[i] esiste, si torni al passo precedente  
Si scriva un predicato prolog:
lunghezza_messaggio(Messaggio,N)
che sia vero se N è la lunghezza del Messaggio in numero di parole.  

Come da bravi decodificatori, si è individuato che in ogni messaggio c’è la preposizione “per”.

Si scriva poi:
decodifica_messaggio(Messaggio,MessaggioDecodificato)
che sia vero se MessaggioDecodificato è il messaggio celato dentro Messaggio.  
Si tenga a mente il predicato precedente.
 Decodificare questo messaggio:
"igspdmicpf lateiala ea tan n nrmt sgee oai na dr oe"

### SOLUZIONE 5
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


### ESAME 6

 Il Gestore di Servizi di Trasporto Pullman (40’)
Si vuole realizzare un servizio di erogazione di biglietti per tratte coperte da pullman.  
Il costo di ogni biglietto è proporzionale alle tratte che devono essere svolte per giungere dalla stazione di partenza alla destinazione.
Ogni tratta, già disponibile in un database, è rappresentata da una lunghezza in kilometri, da un codice di tipologia tratta (e.g. nazionale blu, nazionale grigio, regionale blu, regionale grigio), dalla classe dei mezzi disponibili (normale, comfort, deluxe) e dalle stazioni ai due estremi.  
Ogni codice di tipologia tratta ha un costo per chilometro, ed le classi comfort e deluxe hanno un coefficiente moltiplicativo di costo rispetto alla classe di viaggio normale (unico se trattasi di tutto il sistema).
Un utente può specificare partenza e destinazione e ricevere delle proposte di biglietto per tutte le possibili combinazioni disponibili di tratte (e di tipologie su di esse), tipi di pullman, calcolate automaticamente dal sistema.  
Per ogni biglietto è necessario rappresentare le seguenti informazioni: la partenza, la destinazione, la sequenza delle tratte ed il tipo di mezzo ad esse associate, ed il prezzo del biglietto.
Per lo svolgimento del compito, ignoriamo gli aspetti delle tabelle orarie (assumiamo che vi siano continuamente dei pullman in partenza da ogni stazione ad intervalli molto brevi).

Coefficienti moltiplicativi
- Fatt. moltip. comfort: *1,3*  
- Fatt. moltip. deluxe: *1,7*  
Costo chilometri per categoria
- naz-grigio: *15 cent*  
- naz-blu: *10 cent*  
- reg-grigio: *10 cent*  
- reg-blu: *8 cent*  

 Tabella delle tratte

| Tratta          | dist. | tipo-tratta         | classe           |
| --------------- | ----- | ------------------- | ---------------- |
| Roma-Firenze    | 200km | naz-blu, naz-grigio | tutti            |
| Roma-Pisa       | 220km | naz-blu             | normale, comfort |
| Firenze-Pisa    | 50km  | reg-blu             | comfort, deluxe  |
| Firenze-Bologna | 60km  | reg-blu, naz-blu    | tutti            |
| Roma-Ancona     | 200km | reg-blu, reg-grigio | normale          |
| Roma-Pescara    | 150km | reg-blu, reg-grigio | normale          |
| Roma-Napoli     | 170km | naz-blu             | normale          |
| Napoli-Foggia   | 80km  | reg-blu, reg-grigio | normale, comfort |
| Foggia-Pescara  | 100km | reg-blu             | normale          |
### SOLUZIONE 6
% Student exercise profile
:- set_prolog_flag(occurs_check, error).        % disallow cyclic terms
:- set_prolog_stack(global, limit(8 000 000)).  % limit term space (8Mb)
:- set_prolog_stack(local,  limit(2 000 000)).  % limit environment space

%tratta, distanza, tipo tratta
tratta(roma-firenze, 200, naz-blu).
tratta(roma-firenze, 200, naz-grigio).
tratta(roma-pisa, 220, naz-blu).
tratta(firenze-pisa, 50, reg-blu).
tratta(firenze-bologna, 60, reg-blu).
tratta(firenze-bologna, 60, naz-blu).
tratta(roma-ancona,200,reg-blu).
tratta(roma-ancona,200,reg-grigio).
tratta(roma-pescara,150,reg-blu).
tratta(roma-pescara,150,reg-grigio).
tratta(roma-napoli, 170, naz-blu).
tratta(napoli-foggia, 80, reg-blu).
tratta(napoli-foggia, 80, reg-grigio).
tratta(foggia-pescara, 100, reg-blu).

tipo_tratta(naz-grigio, 15).
tipo_tratta(naz-blu, 10).
tipo_tratta(reg-grigio, 10).
tipo_tratta(reg-blu, 8).

%in input: partenza e destinazione
%output: percorso con tutte le tappe per arrivare a destinazione spendendo il meno possibile

connessi(A, B, Distanza, Tipo) :-
    tratta(A-B, Distanza, Tipo).

connessi(A, B, Distanza, Tipo) :-
    tratta(B-A, Distanza, Tipo).

percorso_economico(Partenza, Destinaz, Tappe, CostoMinimo) :-
    %prendi TUTTI i percorsi da una tappa all'altra, ed ordinali per costo
    setof(Costo-Tappe, percorso_con_costo(Partenza, Destinaz, [Partenza], Tappe, 0, Costo), Percorsi),
    Percorsi = [CostoMinimo-Tappe | _].  % Il primo è il più economico, grazie a setof/3

percorso_con_costo(Città, Città, Acc, Tappe, Costo, Costo):-
    reverse(Acc, Tappe). %perchè Visitate è in ordine inverso alle tappe fatte
    
percorso_con_costo(Corrente, Destinazione, Visitate, Tappe, CostoParziale, CostoTotale) :-
    connessi(Corrente, Prossima, _, Tipo),
    \+ member(Prossima, Visitate),  % Evita cicli
    tipo_tratta(Tipo, Prezzo),
    NuovoCosto is CostoParziale + Prezzo, %vediamo il prezzo della tratta trovata e lo aggiungiamo al costo attuale
    percorso_con_costo(Prossima, Destinazione, [Prossima|Visitate], Tappe, NuovoCosto, CostoTotale).

### ESAME 7
matrice di caratteri, la consegna non è nota
### SOLUZIONE 7
% Student exercise profile
:- set_prolog_flag(occurs_check, error).        % disallow cyclic terms
:- set_prolog_stack(global, limit(8 000 000)).  % limit term space (8Mb)
:- set_prolog_stack(local,  limit(2 000 000)).  % limit environment space
:- discontiguous quadrato/5.
%X=elemento da cercare, N=posizione in cui ci troviamo nella lista, L=lista ordinata,
%L1=gli elementi di L a sinistra di X, L2=gli elementi di L a destra di X
elemAt(X,N,L,R1,R2):- elemAt(X,N,L,R1,R2,0).
elemAt(X,N,[X|R],[],R,N).
elemAt(X,N,[K|R],[K|R1],R2,Count):-
    Count2 is Count+1,
    elemAt(X,N,R,R1,R2,Count2). 

linea(_,_,[]):- fail. %non è necessario perchè tanto prolog se ne occuperà da solo ma vabbè

linea(A,Len,[H|_]):-
    controlla_seq(A,Len,H),!.
linea(A,Len,[_|T]):-
    linea(A,Len,T).

controlla_seq(A, L, Lista) :-controlla_seq_aux(A, L, Lista, 0).

controlla_seq_aux(_, L, _, L).% Caso di successo: contatore ha raggiunto L
controlla_seq_aux(_, _, [], _):- fail.% Se la lista è finita e non abbiamo raggiunto L, fallisce
controlla_seq_aux(A, L, [A|T], C) :-% Se l'elemento corrente è A, incrementiamo il contatore
    C1 is C + 1,
    controlla_seq_aux(A, L, T, C1).
controlla_seq_aux(A, L, [_|T], _) :-% Se l'elemento corrente non è A, resettiamo il contatore
    controlla_seq_aux(A, L, T, 0).

quadrato(_,_,_,0,_):- !. %trovato, C=0 (Il cut non funziona?)

quadrato(_,_,[],_,_):-fail.

%versione giusta: trova A nella sua posizione,vedi se c'è la sequenza da quella posizione, ripeti per le altre Len liste
%C uguale a Len all'inizio
quadrato(A,Len,L):-
    quadrato(A,Len,L,Len).
%1^ iterazione, trovo A per la prima volta
quadrato(A,Len,[H|T],C):-
    elemAt(A,N,H,_,R),
    controlla_seq(A,Len,[A|R]),
    C2 is C-1, %trovata, abbiamo altri C2 lati da cercare
    quadrato(A,Len,T,C2,N).
%non ho trovato A a questa iteraz. di tipo 1
quadrato(A,Len,[_|T],_):-
    quadrato(A,Len,T,Len).

%2^ iteraz., ho trovato A una volta, ora devo ricercarlo nelle prossime C liste in posiz. N
quadrato(A,Len,[H|T],C,N):-
    elemAt(A,N,H,_,R),
    controlla_seq(A,Len,[A|R]),
    C2 is C-1,
    quadrato(A,Len,T,C2,N).

%non abbiamo trovato il quadrato, od un lato è meno lungo del previsto, ri-inizia dalla 1^ iteraz.
quadrato(A,Len,[_|T],_,_):-
    quadrato(A,Len,T,Len).

### LISTA COMANDI SAFE DA USARE
- `append(L1,L2,L3)` → unisce due liste (`L3 = L1 + L2`).
- `member(Elem,L)` → vero se `Elem` appartiene a `L`.
- `reverse(L,Lrev)` → vero se `Lrev` è la lista `L` al contrario.
- `length(L,N)` → vero se `N` è la lunghezza di `L`.
- `is_list(L)` (o `list(L)` in alcuni dialetti) → vero se `L` è una lista.
### 🔹 Gestione atomi, stringhe e numeri
- `atom(A)` → vero se `A` è un atomo.
- `number(A)` → vero se `A` è un numero.
- `string_codes(String,List)` → converte tra stringa e lista di codici carattere.
- `atom_codes(Atom,List)` → converte tra atomo e lista di codici carattere.
- `downcase_atom(A,Lower)` → converte un atomo in minuscolo.
- `abs(N)` → restituisce il valore assoluto.
### 🔹 Gestione della conoscenza dinamica
- `assertz(Fatto)` → aggiunge un fatto alla base di conoscenza.
- `retractall(Head)` → rimuove tutti i fatti che unificano con `Head`.
- `dynamic/1` → dichiara un predicato dinamico (per poter fare assert/retract).
### 🔹 Controllo e meta-predicati
- `once(Goal)` → prova `Goal` una sola volta.
- `forall(Cond,Az)` → vero se per tutti i `Cond` è vera `Az`.
- `not(Goal)` oppure `\+(Goal)` → negazione come fallimento.
- `!/0` (cut) → impedisce backtracking oltre il punto in cui si trova.
### 🔹 I/O
- `write(Term)` → scrive un termine su output.
- `nl` → va a capo.
### 🔹 Gestione ambiente Prolog
- `set_prolog_flag(Flag,Value)` → imposta un parametro del motore Prolog (es. memoria, controlli).
### 🔹 Raccolta di soluzioni
- `setof(X,Goal,Set)` → raccoglie in `Set` tutti gli `X` che soddisfano `Goal`, senza duplicati e ordinati.
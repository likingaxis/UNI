# Modello Relazionale
Venne introdotto per favorire l'indipendenza dei dati 
Questo modello si basa su un concetto matematico di relazione, ogni relazione è di tipo naturale con una rappresentazione su tabelle
### Concetto di relazione
$D_1...D_n$ sono insiemi di domini 
ad esempio 
- stringhe 
- date 
- interi 
- tutti i numeri dal 18 al 21...
Il prodotto cartesiano è definito come tutte le n-uple (d1,...dn)
tali che ciascun elemento $d1\in D1$, $d2 \in D2$ ... $dn \in Dn$
per cui una relazione su una serie di questi domini è un sottoinsieme dei vari prodotti cartesiani
![[Pasted image 20250317180250.png]]
?=sottoinsieme
#### Proprietà dell'insieme
una relazione è un insieme; quindi: 
1. non c'è ordinamento fra le n-uple; 
2. le n-uple sono distinte
3. ciascuna n-upla è ordinata: l’ i-esimo valore proviene dall’ i-esimo dominio
## Esempio pratico
![[Pasted image 20250317180309.png]]

## Precisazione sulla funzione
una relazione è una collezione di n-uple dove una n-upla è una associazione tra un attributo e un dominio corrispondente
## Esempio pratico 2
Rappresentazione di una relazione tramite tabella

| Nome  | Cognome | Matricola | Voto medio |
| ----- | ------- | --------- | ---------- |
| Mario | Rossi   | 1         | 24         |
| Luigi | Bianchi | 2         | 28         |
| Rosa  | Rossa   | 3         | 26         |

Se 𝑡 è una tupla su 𝑿 e A è un attributo, con A ∈ X allora $t[A]$ indica il valore di t su A.
Esempio: se t è la prima tupla allora…
$t[Cognome] -> \ ’ Rossi’$
ci darà 

| Nome  | Cognome   | Matricola | Voto medio |
| ----- | --------- | --------- | ---------- |
| Mario | ==Rossi== | 1         | 24         |
| Luigi | Bianchi   | 2         | 28         |
| Rosa  | Rossa     | 3         | 26         |
## Regole su tabelle e relazioni
Una tabella rappresenta una relazione se
- i valori di ogni colonna sono fra loro omogenei
-  le righe sono diverse fra loro
- le intestazioni delle colonne sono diverse tra loro
 In una tabella che rappresenta una relazione
- l’ordinamento tra le righe è irrilevante
- l’ordinamento tra le colonne è irrilevante
## Esempi e Disempi
![[Pasted image 20250317180346.png]]
## Riferimenti
i riferimenti su relazioni diverse (tabelle) avvengono tramite valori che hanno lo scopo di creare dei riferimenti
## studenti

| Matricola | Cognome | Nome  | Data di nascita |
| --------- | ------- | ----- | --------------- |
| 6554      | Rossi   | Mario | 05/12/1978      |
| 8765      | Neri    | Paolo | 03/11/1976      |
| 9283      | Verdi   | Luisa | 12/11/1979      |
| 3456      | Rossi   | Maria | 01/02/1978      |

## esami

| Studente | Voto | Corso |
| -------- | ---- | ----- |
| 3456     | 30   | 04    |
| 3456     | 24   | 02    |
| 9283     | 28   | 01    |
| 6554     | 26   | 01    |

## corsi

| Codice | Titolo  | Docente |
| ------ | ------- | ------- |
| 01     | Analisi | Mario   |
| 02     | Chimica | Bruni   |
| 04     | Chimica | Verdi   |
DELLE TABELLE COSì AVRANNO UNA RELAZIONE COSì -> 

![[Pasted image 20250317180404.png]]

## Vantaggi ecc(riscrivi meglio dopo)
- indipendenza dalle strutture fisiche (si potrebbe avere anche con puntatori di alto livello) che possono cambiare dinamicamente
- si rappresenta solo ciò che è rilevante dal punto di vista dell’applicazione
- l’utente finale vede gli stessi dati dei programmatori
- i dati sono portabili più facilmente da un sistema ad un altro
- i puntatori sono direzionali
### Definizioni varie
### Schema di relazione
viene detto con il nome R con un insieme di attributi come A1...An
R(A1...An)
Schema di base di dati
insieme di schemi di relazione
R=(R1(X1)...Rk(Xk))
ESEMPIO
- Schema di relazione
STUDENTI(Matricola, Cognome, Nome, Data di Nascita)
- Schema di basi di dati
STUDENTI(Matricola, Cognome, Nome, Data di Nascita)
ESAMI(Matricola, Voto, Corso)
CORSO(Codice, Titolo, Docente)
![[Pasted image 20250317181730.png]]

Qui abbiamo uno schema R(X) che rappresenta la singola tabella mentre invece r di ennuple su X indica i veri e propri dati al suo interno
per quanto riguarda l'istanza su uno schema R delle base di dati indica l'insieme delle varie tabelle
![[Pasted image 20250317180427.png]]
Istanza celestino invece schema la cosa verde
## Strutture nidificate
Voglio rappresentare uno scontrino di questo tipo, possiamo vedere che sono nidificate perché abbiamo una tabella in un'altra
![[Pasted image 20250317180444.png]]
Per farlo creo delle tabelle di questo tipo con delle relazioni
![[Pasted image 20250317180458.png]]
## Struttura rigida conseguenze
spesso possiamo avere informazioni incomplete dovute alla rigidezza del DBMS
#### Vari esempi
![[Pasted image 20250317180517.png]]
Se l'informazione è incompleta non conviene mettere ad esempio 0
nelle base di dati viene usato NULL per indicare un valore non presente o mancante

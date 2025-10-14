# I cookie mantenere stato utente/server
L'interazione HTTP GET/risposta era senza stato 
ciò comporta a dei non problemi
- a nessuno importa di tenere traccia dello stato durante lo scambio
- tutte le richieste sono indipendenti quindi non serve
- se si generano errori si rifà la richiesta 
![[Pasted image 20250318185425.png|300]]
>[!question]- che succede se la connessione di rete o il client si blocca al tempo t'?
>verrà modificato solo fino a x'' creando delle problematiche di lock della variabile
### Utilizzo dei cookie 
I siti web e i browser client usano i cookie per mantenere lo stato delle varie transazioni
ogni cookie rappresenta un identificativo per il client dell'utente ad esempio
#### Per gestire i cookie servono 4 componenti

1️⃣ **Riga di intestazione nella risposta HTTP**
- Quando un utente visita un sito per la prima volta, il server invia un’intestazione HTTP che imposta un cookie sul browser dell’utente.
2️⃣ **Riga di intestazione nella richiesta HTTP**
- Nelle richieste successive, il browser include il cookie nell’header HTTP per identificare l’utente.
3️⃣ **File cookie sul sistema dell’utente**
- Il browser salva il cookie localmente nel computer dell'utente, permettendo di usarlo per richieste future.
4️⃣ **Database sul sito**
- Il server memorizza le informazioni relative a ciascun **sessionID** in un database
##### Esempio grafico su come funziona il sistema dei cookie
![[Pasted image 20250318190550.png|500]]
i cookie vengono usati per 
- autorizzazioni
- carrelli degli acquisti
- raccomandazioni per pubblicità

Di default il protocollo HTTP è stateless come fanno client e server a mantenere salvati gli stati?
ci sono due metodi:
1️⃣ **Presso gli endpoint del protocollo**
- Il **trasmettitore** e il **ricevitore** (client e server) devono **conservare lo stato** tra più transazioni.
- Ad esempio, un sito di e-commerce salva nel database gli articoli del carrello dell’utente.
2️⃣ **Nei messaggi HTTP (usando i cookie)**
- I cookie vengono **trasmessi con ogni richiesta HTTP**, permettendo al server di riconoscere l’utente.
- Es. Un cookie di sessione può contenere un **session ID**, che il server usa per associare la richiesta all’utente corretto.

SIMPATICA GIF DI UN ESEMPIO :)
![[ciao/content/UNI/ANNO 2/RETI/fotret/ezgif.com-animated-gif-maker.gif|500]]

##### GDPR
Serie di regole europee per garantire la privacy riservatezza dei dati ecc...
### Web cache
È un intermediario tra il server d'origine e i client per soddisfare le richieste senza coinvolgerlo
Il browser ha una sua web cache locale che se ha già salvato la richiesta HTTP la rimanda direttamente altrimenti comunica con il server
![[Pasted image 20250318192553.png|400]]
##### Web cache di tipo proxy
Il proxy funziona come da client perché fa delle richieste al server d'origine e le salva
poi quando un client comunica con il proxy esso funge da server
Vantaggi
riduzione del traffico tempi di risposta più rapidi e evita la queue
### Esempi di miglioramento di una infrastruttura di rete
![[ciao/content/UNI/ANNO 2/RETI/fotret/ezgif.com-animated-gif-maker (1).gif]]
Nel primo esempio abbiamo una velocità di trasferimento troppo lenta e una infrastruttura che presenta delle problematiche che causano un enorme ritardo
###### Opzione 1
miglioro la velocità di collegamento riducendo così il ritardo
- problema: costa troppo
#### Opzione 2
metto una cache locale per ridurre il ritardo
- funziona evviva che bello
### Get condizionale
Non fare la get(inviare) se nei metadati c'è la stessa data di modifica
![[Pasted image 20250318194725.png|300]]
### HTTP 1.1
Viene introdotta la GET multipla in pipeline su una singola connessione TCP
>[!bug] problemi
>- usa First Come First Served che causa problematiche
>	- se ho un blocco piccolo dopo blocchi grandi esso verrà inviato molto dopo (HOL)
>	- recupero delle perdite di informazioni blocca tutto

### HTTP/2
Per risolvere i problemi di prima viene usato un sistema a priorità
- invio push al client di oggetti aggiuntivi senza richieste per avvantaggiare il tutto
- Dividere gli oggetti in frame così da ridurre HOL
- riduce overhead 
- funziona meglio il controllo della congestione TCP
##### Esempio di mitigazione con HTTP/2
Esempio di richiesta da un client di 1 oggetto grande e 3 più piccoli
essi vengono divisi in frame per fare una trasmissione interlacciata ovvero trasmessi alternando i vari oggetti
![[Pasted image 20250318200004.png]]
#### perché passare da HTTP/2 a HTTP/3
HTTP/2 cerca di inviare su una singola connessione TCP
- ciò causa problemi per eventuali recuperi delle informazioni che bloccano tutta la trasmissione degli oggetti
- non c'è grande sicurezza su una TCP semplice
#### HTTP/3 viene in nostro aiuto
migliora
- sicurezza
- errori
- utilizza direttamente **UDP** come protocollo di trasporto, migliorandolo con il protocollo **QUIC** per gestire 
	- sicurezza
	- controllo di errore
	- congestione

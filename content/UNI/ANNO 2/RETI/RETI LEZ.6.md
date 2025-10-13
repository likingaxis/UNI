### Posta elettronica
Ci sono tre componenti principali
- user agent
	- il programma che consente di comporre email leggerle ecc... tipo outlook
- mail server
	- server di posta che gestisce la casella di posta dell'utente
	- il server di posta prende i messaggi nella coda di uscita e prova a mandarli al server di posta del destinatario
	- sotto ho fatto un esempio
- simple mail transfer protocol: SMTP
	- protocollo che consente il trasferimento di messaggi tra server di posta
![[Pasted image 20250321175516.png|400]]
## Esempio di posta elettronica
- io paolo@sbors.it invio al mio server di posta sbors.it la mail con SMTP
- successivamente il server di posta usa SMTP per inviare la lettera al server di posta del destinatario che lo riceverà con SMTP 
- ma come fa il tizio ad accedere alla sua casella di posta? 
	- con il protocollo IMAP che spieghiamo tra poco
#### A che serve avere un server? non basta inviare alla persona e basta?
Serve un server perché e bene avere un servizio esterno che gestisce le cose mettiamo che Samuele ha il pc spento poi può prelevare le cose dal server
### SMTP RFC (5321)
- RFC indica i documenti definiti dagli enti in modo universale che abbiamo citato alla scorsa lezione 
- Questo protocollo serve per instradare i pacchetti con un sistema client-server
- i pacchetti sono messaggi di posta elettronica
Questo protocollo si serve del protocollo TCP per trasmettere i pacchetti 
Per fare il trasferimento ci sono 3 step:
- handshaking TCP per stabilire la connessione
- handshaking smtp per presentare le due parti client server con i vari codici di stato
- il trasferimento dei messaggi veri e propri 
- poi la chiusura
![[Pasted image 20250321180434.png|300]]
### Esempio stupido con Alice e Bob
![[Pasted image 20250321181228.png|600]]
#### Esempio dettagliato
server di posta crepes.fr invia al server di posta hamburger.edu possiamo vedere tutti gli step
![[Pasted image 20250321181449.png]]
spiegazione 
Qui possiamo vedere come il . venga usato per indicare la fine del messaggio 
MAIL FROM E RCPT vengono usate per indicare il mittente e il destinatario
DATA avverte che stanno per arrivare i dati
#### SMTP VS HTTP
smtp: è di tipo client push(invia i dati senza che essi vengano richiesti)
http: è di tipo client pull(il client richiede esplicitamente dei dati)
- entrambi hanno una interazione comando/risposta in ascii e usano codici di stato
- http: ciascun oggetto è incapsulato nel suo messaggio di risposta
- smtp: più oggetti vengono trasmessi in un unico messaggio
smtp usa connessioni persistenti e durature fino al quit a differenza di http

per indicare la terminazione del messaggio:
- http: usa CRLF (`\r\n`) per separare le righe degli header e una riga vuota CRLF (`\r\n\r\n`) per segnalare la fine degli header e l'inizio del corpo del messaggio.

- smtp: usa CRLF (`\r\n`) per terminare ogni riga. La fine del messaggio è indicata da `\r\n.\r\n`, cioè una riga con solo un punto (`.`) dopo un CRLF

##### Formato dei messaggi di posta elettronica
![[Pasted image 20250321183134.png]]
#### ACCEDERE ALLA MAIL DI POSTA CON IMAP
![[Pasted image 20250321183245.png|500]]
protocollo che permette di scaricare i messaggi sul server di posta elettronica
- consente di recuperare cancellare e archiviare i messaggi memorizzati nel server
IMAP sta per Internet Mail Access Protocol
### La web mail funziona con http
accedo tramite browser e basta come Gmail Hotmail ecc...
utilizzano una interfaccia web

## DNS
Gli host su internet sono definiti da indirizzi IP da 32 o 128 bit
anche gli host hanno diversi identificatori non solo indirizzi IP, quest'ultimi sono difficili da digitare
### Soluzione vecchia e pasticciona cogliona
un tempo si usava un file con indirizzi IP che corrispondevano a nomi
![[Pasted image 20250321185128.png|400]]
il problema di questo file è che deve crescere costantemente
questo file era registrato da NIC un ente che aveva il compito di tenere conto dei vari indirizzi IP 
#### Soluzione
Per ovviare questo problema di host.txt venne introdotto il DNS
che sta per Domain Name System
un database distribuito(ma anche il protocollo che consente la comunicazione con essi) che ha una applicazione che traduce il nome in un indirizzo IP
il DNS è nella periferia della rete e funziona nel livello applicativo
esso ha un modello di servizi:
1) traduce da host name a indirizzo IP
2) fa l'host aliasing dove si può avere un nome friendly alias tipo se cerchi google.it va su google.com
3) mail server aliasing permette a più indirizzi email diversi di **confluire sulla stessa casella** tipo pippo@azienda.it franco@azienda.it
4) load distribution distribuzione del carico di rete, supponiamo di avere netflix.com esso corrisponde a un indirizzo IP di una macchina, il DNS può sapere che esso è associato a piu host con indirizzi IP, quindi può darne piu di uno a ruota per evitare sovraccarichi
>[!question]- perché non centralizzare il DNS
>- ci sarebbe solo un punto vulnerabile
>- maggiore volume di traffico
>- manutenzione difficile
>infatti il DNS e DISTRIBUITO
>differenza tra centralizzato e distribuito?
>- centralizzato: Tutto (dati, logica, risorse) si trova su **un solo server** o in un singolo nodo centrale.
>- distribuito: distribuito su più server che collaborano tra loro

quasi tutte le interazioni su internet passano per il DNS
il DNS deve essere affidabile e sicuro

#### Gerarchia nel dettaglio  del DNS
![[Pasted image 20250321190924.png]]
C'è una divisione dei livelli dei server del DNS
- la root dove ci sono i server che indirizzano ai server DNS più specifici
- TLP dove abbiamo i domini più usati e sono infatti strettamente collegati alla radice
- poi ci sono gli autoritativi tipo uniroma2.it
	- i server autoritativi sono quelli che sanno l'indirizzo IP effettivo
>[!tip] Ricordiamo il DNS è distribuito gerarchico e decentralizzato 

### Esempio con amazon.com
- **Il client interroga un root server DNS**
- **Il client interroga un TLD server per .com**
- **Il client interroga il server autorevole per amazon.com**
## DNS locale
A questa gerarchia bisogna aggiungere un DNS server locale 
un server terzo a cui noi chiediamo la conversione dell'indirizzo e la fa per nostro conto se non è presente nella sua cache
Ogni DNS locale è in ogni ISP(Internet Service Provider)
- non appartiene alla gerarchia dei DNS
### Interrogazione DNS come funziona?
ci sono di due tipi
###### di tipo iterativo
![[Pasted image 20250321192921.png]]
- il DNS server locale deve interrogare tutti i vari server se non ha nella cache l'ip convertito
###### di tipo ricorsivo
![[Pasted image 20250321192958.png]]
- in questo caso si "risolvono" tra di loro
## Caching del DNS
Anche il DNS ha una cache che ha un time to live delle conversioni
- questa cache tiene conto della mappatura basandosi sulla determinata query e restituisce il risultato 
il DNS è un servizio best effort che non assicura sempre una conversione corretta
#### Come è fatto un record DNS
il database usa un formato RR(risorse record) con
$$(name, value, type, ttl)$$
dove rispettivamente abbiamo:
- name: Il dominio o sottodominio a cui il record si riferisce
- value: L'informazione associata (es. IP, altro hostname, mail server)
- type: Il tipo di record DNS
- TTL: Il tempo di vita della cache DNS prima di una nuova risoluzione
##### Ci sono diversi tipi di Record in ogni DNS (autoritativi?)

| Tipo di Record | Descrizione                                          | Esempio a parole                                                        |
| -------------- | ---------------------------------------------------- | ----------------------------------------------------------------------- |
| A              | Mappa un hostname a un indirizzo IPv4                | Il dominio 'www.esempio.com' punta all'IP 192.168.1.1                   |
| NS             | Specifica il name server responsabile per un dominio | Il dominio 'esempio.com' è gestito dal name server 'ns1.esempio.com'    |
| CNAME          | Definisce un alias per un altro hostname             | Il dominio 'blog.esempio.com' è un alias di 'server1.esempio.com'       |
| MX             | Specifica il mail server per il dominio              | Il dominio 'esempio.com' gestisce le email attraverso 'mail.esempio.com |

#### Messaggi DNS
![[Pasted image 20250321210303.png|700]]

### Mettere un nostro sito nel sistema
![[Pasted image 20250321210406.png]]

#### Sicurezza nel DNS
- Deve essere sicuro da attacchi DDoS 
- attacco di spoofing: dove io rintraccio una richiesta e fornisco l'informazione fasulla avvelenando le cache
	- per ovviare abbiamo DNSSEC , garantisce che le risposte DNS siano autentiche e non alterate da terze parti.
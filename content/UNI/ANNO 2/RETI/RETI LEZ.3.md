### Internet e la sua sicurezza
internet di base è nato senza includere la sua sicurezza
### Analisi dei pacchetti 
 - una interfaccia di rete legge e registra tutti i pacchetti che l'attraversa
![[Pasted image 20250314183026.jpg|400]]
### identità falsa
- attraverso un IP spoofer che inietta pacchetti con indirizzi ip falsi
![[Pasted image 20250314183100.jpg|400]]
### Negazione del servizio
- attraverso attacchi Dos(Denial of Service)
	- rendono una rete, un host o altri elementi di infrastruttura non disponibili per gli utenti
	- si dividono in 3 categorie
		- 1) invio di pochi pacchetti ma che sono costruiti per far bloccare il servizio attraverso vulnerabilità
		- 2) bandwidth flooding invio in massa di pacchetti che impediscono il traffico legittimo
			- avviene in una situazione in cui il client invia un numero di bit al secondo maggiore di quelli che può ricevere il server
		- 3) connection flooding connessioni in massa TCP al servizio impedendogli di accettare le connessioni da parte di utenti legittimi 
foto del bandwidth flooding
![[Pasted image 20250314184506.jpg|300]]
foto del connection flooding
![[Pasted image 20250314184926.jpg|300]]
### Linee di difesa
- autenticazione: attraverso identità hardware ad esempio una carta SIM
- riservatezza: attraverso la cifratura
- integrità: le firme digitali prevengono/rilevano le manomissioni
- restrizioni di accesso:VPN con protezione da password
- firewalls: middlebox che fa da intermediario e che 
	- "off-by-default" filtra i pacchetti in entrata e limita i mittenti i destinatari e le applicazioni
	- rilevare/reagire agli attacchi DOS
### Livelli di protocollo e modelli di riferimento
Le reti sono complesse e composte da diverse componenti, per gestirle e collegarle al meglio si decise di dividere l'organizzazione della rete in più strati e livelli
##### Utilità della stratificazione
- la modulazione facilita la manutenzione e l'aggiornamento di un sistema
- una struttura impostata in modo esplicito consente l'identificazione dei vari componenti 
##### Svantaggi della stratificazione
- un livello sopra deve violare la separazione di questi livelli e deve scendere sotto per ottenere informazioni
- un livello superiore può duplicare un livello inferiore
	- come la correzione di errori che è presente in più livelli
### Pila di protocolli di internet
![[Pasted image 20250314192324.jpg]]
## Servizi, Stratificazione e Incapsulamento
![[Pasted image 20250314204807.png]]
Questa slide ci fa vedere come i livelli siano usati sia da sorgente che destinazione ovvero client e server
ad ogni livello abbiamo un aggiunta di quello che era il pacchetto nel livello precedente 
possiamo vedere la cosa come
Un pacco postale:
- Il **messaggio originale (M)** è l'oggetto che vuoi spedire.
- Il **livello di trasporto** aggiunge un'etichetta con il nome del destinatario.
- Il **livello di rete** aggiunge un indirizzo più dettagliato (via, città, codice postale).
- Il **livello di collegamento** impacchetta tutto in una busta.
- Il **livello fisico** lo trasporta tramite camion o aereo.
Qui ogni livello lo invia al sottostante aggiungendo un header ovvero informazioni aggiuntive che servono per la comunicazione del pacchetto
il datagramma è il nome del tipo di dato che si trova nel livello di rete, in tutti gli altri livelli si chiama in un altro modo

|**Livello OSI**|**Nome dell'unità di dati**|**Descrizione**|
|---|---|---|
|**Applicazione (7)**|**Messaggio**|Dati generati da un’applicazione (es. una richiesta HTTP, un’email, un file inviato su FTP).|
|**Trasporto (4)**|**Segmento (TCP) / Datagramma (UDP)**|TCP divide i dati in **segmenti** per garantire la consegna affidabile. UDP usa **datagrammi**, che sono più veloci ma non garantiscono la ricezione.|
|**Rete (3)**|**Datagramma IP**|Unità di dati del protocollo IP, che trasporta i segmenti da un host all'altro nella rete.|
|**Collegamento (2)**|**Frame**|Il datagramma IP viene incapsulato in un **frame** Ethernet o Wi-Fi per essere trasmesso tra dispositivi direttamente connessi.|
|**Fisico (1)**|**Bit**|Il frame viene trasformato in segnali elettrici, onde radio o impulsi ottici per viaggiare nel mezzo fisico.|
## I servizi 
Ogni livello ha i suoi servizi che fornisce al livello superiore in modo indipendente ogni livello di solito ha più protocolli per fornire diversi sistemi come TCP o UDP per quello di trasporto
### Da qui prendiamo il concetto di matrioska (incapsulamento)
![[Pasted image 20250314211620.png]]
![[Pasted image 20250314211654.png]]
si può tutto vedere come una matrioska e i vari livelli che aggiungono informazioni al pacchetto finale
## Visione end-to-end incapsulamento (senza intermediari)
![[Pasted image 20250314211942.png]]
### n-PDU cosa è e come vengono implementati i livelli
possiamo da questa immagine notare come il livello di rete faccia da intermediario tra hardware e software
![[Pasted image 20250314212354.png|400]]
l'unità di dati definita prima prende il nome generico in PDU(Protocol Data Unit)
ogni PDU ha come nome quello che era presente nella tabella precedente ed è composto da
- informazioni di controllo sono dati aggiuntivi (metadati) che aiutano il protocollo a gestire la comunicazione.
- payload il contenuto effettivo
# modello TCP/IP vs ISO/OSI
![[Pasted image 20250314212722.png]]
possiamo vedere come esista il modello ISO/OSI che presenta 2 livelli in più
- presentazione
	- aggiunge l'interpretazione di un determinato dato prima che venga dato ai livelli sottostanti(discorsi di crittografia dei dati ecc...)
- sessione
	- serve per sincronizzazione
internet non prevede questi strati vanno messi nelle applicazioni

### parentesi su Wireshark
![[Pasted image 20250314212904.png]]
Wireshark lavora al livello applicativo analizzando i vari pacchetti che arrivano in rete attraverso il packet capture del computer
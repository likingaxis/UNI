# parti fondamentali di internet
gli <font color="#c0504d">host</font> ospitano le applicazioni di rete, vengono anche chiamati end system si dividono in:
- client, chiedono servizi
- server, forniscono servizi
il <font color="#c0504d">browser</font> è lo user-agent che consente la comunicazione all'interno della rete
all'<font color="#f79646">interno</font> della rete non abbiamo gli host, essi sono parte esterna di esso come anche i client
all'interno della rete abbiamo i vari router e switch e ci consentono di <font color="#f79646">commutare</font> i vari pacchetti
>[!tip] per commutare si intende l'instradamento e la gestione dei vari pacchetti all'interno di una rete


![[Pasted image 20250303174455.png|500]]

per far comunicare tra loro i vari router switch host ecc... abbiamo bisogno di 
#### reti di collegamento
come rame fibra ecc... che hanno un loro tasso di trasmissione(pratico) e una loro ampiezza di banda(teorico)

Internet <font color="#c0504d">non è uniforme</font> bensì è una serie di reti composte a loro volta da 
 - dispositivi, router, collegamenti ecc...
#### Chi ci fornisce internet?
gli <font color="#f79646">ISP</font>(Internet Service Provider)
Internet è un insieme di ISP connessi tra loro
###### Concetto di <font color="#f79646">IoT</font>
internet delle cose, dove per "cose" si intendono tutti quegli oggetti che un tempo non erano connessi a internet ma ora lo sono

##### I dispositivi devono comunicare attraverso dei protocolli
i protocolli sono un insieme di regole che consentono e gestiscono l'invio e la ricezione di messaggi 
- http,streaming video, skype, tcp, ip, ethernet, wifi 4-5g ecc...
il protocollo di un messaggio indica esattamente
- il loro formato
- l'ordine di invio
- azioni intraprese in fase di trasmissione o ricezione di un messaggio o un evento
![[Pasted image 20250303180317.png|700]]

Standard che danno delle garanzie sulle varie compatibilità di internet
- RFC
- IETF
altri standard che lavorano su reti metropolitane oppure ethernet e Wi-Fi
protocolli Wi-Fi definiti da IEE come 802.11
### internet cosa è
internet è una infrastruttura globale di reti che fornisce un servizio di comunicazione alle varie applicazioni e dispositivi
Internet è un po come le poste, ci da la possibilità di avere più servizi di comunicazione
<font color="#f79646">l'interfaccia socket </font>ci serve per usare e definire una connessione a internet tra processi e applicazioni 
## le reti di accesso 
il primo router usato per uscire da una rete LAN a una WAN si chiama router edge
cosa importa? 
- velocità di trasmissione
una forma primitiva di rete di accesso internet è sicuramente quella con il modem 56k
poi ci fu una evoluzione con la DSL
![[Pasted image 20250303181839.png]]
Il provider darà un DSLAM un dispositivo che collega più linee da parte del provider
viene usato quindi un doppino per le basse frequenze le chiamate per le alte frequenze internet chiamato multiplexing a divisione di frequenza
noi abbiamo un collegamento dedicato con la centrale operativa
è normale ci sia differenza tra download e upload dovuto a un limite fisico
## Differenza tra i vari punti di accesso FTTx
![[Pasted image 20250303182107.png]]
## FTTH di tipo PON
sistemi non alimentati passivi
![[Pasted image 20250303182308.png]]
sono composti dai seguenti dispositivi OLT e ONT
- OLT: è da parte del provider e viene usato per fare da intermediario tra internet della centrale locale e i vari ONT 
- Viene usato uno splitter ottico per indirizzare i pacchetti ad ogni ONT, essendo passivo lo invia ad ogni ONT
- ONT: rappresentano un terminatore di fibra che viene condiviso nelle singole abitazioni
la potenza viene suddivisa quindi per ogni ONT
per l'upload viene usato il TDM Time division multiplexing per dividere il tempo di uso di upload dal ONT al OLT
FWA(Fixed Wireless Access)
wireless != mobile
![[Pasted image 20250303183134.png]]

# Reti locali wireless o Accesso wireless su scala geografica
<font color="#f79646">Locali</font> centinaia di metri di copertura
![[Pasted image 20250303183752.png|300]]
<font color="#f79646">Geografica</font> kilometri di copertura
![[Pasted image 20250303183817.png]]
# INVIO DEI PACCHETTI DI DATI
Il tutto viene suddiviso in sotto pacchetti con un tempo di trasmissione R e una lunghezza dei pacchetti L quindi abbiamo un ritardo di trasmissione dato da $\frac{L}{R}$
###### Mezzi vincolati e mezzi non vincolati
- <font color="#f79646">mezzi vincolati</font> sono obbligati a propagarsi su mezzi solidi
- <font color="#f79646">mezzi non vincolati</font> tipo wireless o radio
##### Tipi di cavi
- cavo ethernet
	- categoria 5-6
		- cambia la velocità e la distanza
- cavo coassiale
	- connettori di rami a banda larga
- cavo in fibra ottica
	- si attenua poco alle distanze e alle interferenze elettromagnetiche
##### segnali wireless
- canali radio
	- segnale elettromagnetico
	- broadcast quindi non si può parlare contemporaneamente
	- riflessione dell'onda ostruzione ecc...
- Bluetooth
	- brevi distanze con PAN Personal area network
- Wireless LAN
- microonde terrestri
	- punto punto
- satellitari
	- tipo star-link
	- 3 tipi di orbite
		- LEO
			- orbita bassa
		- MEO
			- orbita media
		- GEO
			- orbita geostazionaria ad alta distanza quindi rimane sempre nello stesso punto
![[Pasted image 20250303183458.png]]


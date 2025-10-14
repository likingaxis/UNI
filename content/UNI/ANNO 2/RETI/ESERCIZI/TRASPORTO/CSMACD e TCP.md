### ESERCIZIO 1
Facendo riferimento allo schema CSMA/CD, determinare che 
vincolo c'è tra lunghezza minima dei pacchetti e distanza massima 
tra due interfacce.

- il vincolo è
	- $T_{trasmissione} \geq 2*T_{propagazione}$ 
	- $T_{trasm}​=L/R$
		- Dimensione/velocità del collegamento
	- $T_{prop}​=d/v​$
		- distanza/velocità

### ESERCIZIO 2
![[Pasted image 20250710191022.png|300]]
- Capire che gli ACK sono cumulativi
- qui viene inviato un ACK corretto per il secondo segmento quindi si implica che anche il primo è stato inviato correttamente
- disegna le finestre di ricezione così
![[Pasted image 20250710191120.png|350]]
### ESERCIZIO 3
![[Pasted image 20250710191157.png]]
- Analizza i casi
	- **se si ha una crescita esponenziale**
		- Slow Start
	- **se si ha una piccola ricaduta**
		- Triplo ACK duplicato
		- fast recovery e poi congestion avoidance
	- **se si ha una caduta a 1**
		- timeout degli ACK
		- con cwnd=1
		- e poi va in slow start
### ESERCIZIO 5
Si consideri che una singola connessione TCP Reno utilizzi un collegamento da R = 
10 Mbps e si supponga che esso sia l'unico collegamento congestionato lungo il 
percorso tra il mittente e il destinatario.
Si assuma che:
• la connessione sia sempre in congestion avoidance (andamento a dente di sega)
• RTT = 150 ms
• tutti i segmenti abbiamo dimensione 1500 byte
• il mittente abbia sempre dati da trasmettere
• la finestra di ricezione sia molto più grande della finestra di congestione del mittente
Determinare:
• dimensione massima della finestra, espressa in segmenti
• throughput medio, espresso in Mbps
• tempo impiegato per raggiungere nuovamente la dimensione massima della finestra 
dopo il dimezzamento dovuto alla perdita di un pacchetto 

- serve sapere il tasso di trasmissione al TCP reno si calcola facendo
- $T_{trasmissione}=\frac{W*MSS}{RTT}$
	- $R\geq \frac{W*MSS}{RTT}$ 
	- da questa considerazione  sopra si può ritrovare W facendo la formula inversa
- Poi trovi il troughput medio 
	- $troughput \ medio = \frac{3}{4}*\frac{W_{max}*MSS}{RTT}$ 
- Per trovare il tempo impiegato per raggiungere la dimensione massima
	- $(W_{max}-\frac{W_{max}}{2} )*RTT$  

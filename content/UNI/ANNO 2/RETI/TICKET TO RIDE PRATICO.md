$$Ritardo_{e2e​}=T_{tx}​+T_{prop​}+T_{queue}​+T_{proc}​$$
$$T_{trasm}​=L/C​$$
$$T_{prop}​=d/v​$$
$$T_{queue​}=inizio \ trasmissione \ effettiva−tempo \ di \ arrivo \ al \ nodo$$

| Simbolo | Nome | Valore              |
| ------- | ---- | ------------------- |
| k       | kilo | 10³ = 1.000         |
| M       | mega | 10⁶ = 1.000.000     |
| G       | giga | 10⁹ = 1.000.000.000 |


$$Ritardo totale≈τ1​+τ2​+τ3​+\frac{D_{bit} file}{\min_i(C_i)}$$
- ritardi di propagazione+ Dim bit/bandapiùlenta
$$Ritardo_{e2e​}\ 1 \ tunnel= MIN\{R_C,R_S,R/LINK\}$$
- Collodibottiglia/client o server 
$$ Tempo \ utilizzo \ singolo \ link =R_S/R_C$$
- se per un collegamento passano più collegamenti, moltiplica per il numero di collegamenti
##### Correzione errori
`1101 1010 1001 0110`
- EDC con bit di parità
	- dividi in 4 gruppi
		- fai matrix
		- bit di parità x righe e colonne
		- e quello globale
- EDC con checksum
	- dividi in gruppi da 16
	- gruppo 1+gruppo 2
		- ris+gruppo 3
	- riporto lo elimini sommandolo ai meno signific
	- compl a 1

##### CSMA/CD
- il vincolo è
	- $T_{trasmissione} \geq 2*T_{propagazione}$ 
	- $T_{trasm}​=L/R$
		- Dimensione/velocità del collegamento
	- $T_{prop}​=d/v​$
		- distanza/velocità
#### TCP RENO
- serve sapere il tasso di trasmissione al TCP reno si calcola facendo
- $T_{trasmissione}=\frac{W*MSS}{RTT}$
	- $R\geq \frac{W*MSS}{RTT}$ 
	- da questa considerazione  sopra si può ritrovare W facendo la formula inversa
- Poi trovi il troughput medio 
	- $troughput \ medio = \frac{3}{4}*\frac{W_{max}*MSS}{RTT}$ 
- Per trovare il tempo impiegato per raggiungere la dimensione massima
	- $(W_{max}-\frac{W_{max}}{2} )*RTT$  

#### numero /x
$2^x-2\geq interfacce$ 

### Ritardo end-to-end
$$Ritardo_{e2e​}=T_{tx}​+T_{prop​}+T_{queue}​+T_{proc}​$$
- Ritardo di trasmissione
	- Tempo per **inviare tutti i bit** di un pacchetto sul canale.
	- $T_{trasm}​=L/C​$
	- Dimensione/velocità del collegamento

- Ritardo di propagazione
	- Tempo per il **primo bit** a viaggiare da mittente a destinatario.
	- $T_{prop}​=d/v​$
	- distanza/velocità

- Ritardo di elaborazione
	- Tempo che un nodo (es. router) impiega per **analizzare, controllare e instradare** il pacchetto.
	- fornito dal prof

- Ritardo di accodamento (se presente)
	- Tempo che un pacchetto aspetta **in coda nel router o nodo**, in attesa che il link si liberi.
	- $T_{queue​}=inizio \ trasmissione \ effettiva−tempo \ di \ arrivo \ al \ nodo$
### Router
se un router ha politica FIFO con store and forward semplicemente può salvare nel buffer tutti i pacchetti che vuole e li invia con logistica FIFO, ovviamente rispettando sempre il fatto che può inviare su un link un pacchetto per volta o anche ricevere

### Conversioni
Si usa il **prefisso decimale**:

| Simbolo | Nome | Valore              |
| ------- | ---- | ------------------- |
| k       | kilo | 10³ = 1.000         |
| M       | mega | 10⁶ = 1.000.000     |
| G       | giga | 10⁹ = 1.000.000.000 |

### stimare il ritardo con tanti pacchetti

$$Ritardo totale≈τ1​+τ2​+τ3​+\frac{D}{\min_i(C_i)}$$
dove rispettivamente abbiamo

| Termine                               | Significato                                                                                |
| ------------------------------------- | ------------------------------------------------------------------------------------------ |
| $\tau_1 + \tau_2 + \tau_3τ1​+τ2​+τ3​$ | Somma dei **ritardi di propagazione** su ogni tratto                                       |
| $\frac{D}{\min(C_i)}​$                | Tempo necessario a **trasmettere tutto il file D bit**, limitato dalla **banda più lenta** |
Insomma quando si hanno tanti pacchetti si può fare sta roba
#### Troughput end-end con un singolo tunnel
$$ MIN\{R_C,R_S,R/LINK\}$$ 
![[Pasted image 20250713123038.png|300]]
#### Calcolare il tempo di utilizzo di un collegamento
$$ R_S/R_C$$ se $R_S\leq R_C$ o viceversa per il collegamento di $R_S$ fare $R_S/R_S$ 
al num metti il collo di bottiglia 
se per un collegamento passano più collegamenti, moltiplica per il numero di collegamenti

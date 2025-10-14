## 🧪 **Obiettivo generale**

> Imparare a usare `ping` in modo avanzato per:

- Verificare la raggiungibilità di un host
    
- Calcolare l’**RTT** (Round Trip Time)
    
- Studiare pacchetti ICMP e opzioni di invio
    
- Capire l'effetto del **TTL**, del **timeout** e della **dimensione del pacchetto**
## ✅ **Esercizio 1 – ping base + Wireshark**

- Si esegue `ping www.google.it`, si interrompe con `CTRL+C`.
- Viene inviato ogni secondo un pacchetto ICMP **Echo Request**.
	- serve per capire se un host è raggiungibile 
- Ogni risposta è un **Echo Reply**, che include:
    - Numero sequenza (`icmp_seq`)
    - Tempo di ritorno (`time`)
    - TTL (dal pacchetto IP)  
- In **Wireshark** si filtra con `icmp` per vedere i pacchetti.

## ✅ **Esercizio 2 – Opzione `-c` (count)**

- `ping -c 1 www.google.it`
- Invia n pacchetti in questo caso 1.

## ✅ **Esercizio 3 – Opzione `-w` (deadline)**
- `ping -w 3 www.google.it`
- Esegue ping per **al massimo 3 secondi**, indipendentemente dal numero di pacchetti.
- Ping invia un pacchetto ogni secondo → si ricevono 3 pacchetti prima dello stop.
## ✅ **Esercizio 4 – Opzione `-i` (intervallo)**
- `ping -i 1.495 -w 3 www.google.it`
- Cambia l’intervallo tra un pacchetto e il successivo.
- Serve a simulare **invii più frequenti o più lenti**.
- Se combinato con `-w`, può causare **perdita di pacchetti** perché non si lascia tempo sufficiente alla risposta.
cambia la frequenza
## ✅ **Esercizio 5 – Combinazione `-i -c -w`**
- `ping -i 1.495 -c 3 -w 3 www.google.it`
- Invia 3 pacchetti ma scade a 3 secondi → **non fa in tempo a ricevere l’ultimo ACK**.
- Mostra che il timeout è importante anche se i pacchetti sono stati inviati correttamente.
## ✅ **Esercizio 6 – Opzione `-W` (timeout risposta)**

- `ping -W 1 -c 1 www.google.it`: aspetta **1 secondo** per la risposta.
- `ping -W 0.01 -c 1 www.google.it`: timeout troppo basso → **perdita pacchetto**.
- Mostra come un RTT alto può portare a **false perdite** se il timeout è troppo breve.
## ✅ **Esercizio 7 – Opzione `-s` (dimensione dati ICMP)**
- `ping -s 10 www.google.it`
- Cambia la dimensione del payload ICMP (non del pacchetto IP totale).
- Sotto i 16 byte, **ping non può calcolare l’RTT** perché manca il timestamp.
- Utile per testare **quanto i dati influenzano la risposta**.
## ✅ **Esercizio 8 – Opzione `-t` (TTL - Time To Live)**
- `ping -t 11`: limita il TTL → pacchetto viene **fermato da un router intermedio**.
- Il router invia un messaggio ICMP "Time Exceeded".
- `ping -t 12`: pacchetto **raggiunge la destinazione**.
- Serve a determinare quanti **hop** ci sono tra sorgente e destinazione (come fa `traceroute`).
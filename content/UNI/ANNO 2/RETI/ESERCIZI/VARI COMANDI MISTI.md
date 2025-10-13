# COMANDI LIVELLO DI TRASPORTO
## ss -s statistiche sulle socket
- mostra quali socket sono all'attivo per determinati protocolli
![[Pasted image 20250706161153.png]]
## ss-u -ua
- u specifica socket UDP
- ua specifica anche le socket che non hanno connessioni all'attivo
![[Pasted image 20250706161524.png]]
## altri comandi di ss
 - - n toglie le traduzioni automatiche delle porte
	quindi indirizzo:http  ora si vedrà come indirizzo:80
- - p informazioni sul processo
- - E socket distrutte

## dig
effettua richiesta un server DNS
![[Pasted image 20250706162626.png]]
## Wireshark
analizza i pacchetti inviati e ricevuti nella rete
- ha dei filtri che consentono di vedere determinati pacchetti
## ip addr
mostra indirizzi IP delle varie interfacce di rete del dispositivo

# COMANDI LIVELLO DI RETE
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

# COMANDI LIVELLO DI COLLEGAMENTO
## COMANDI IP
### 🔹 `ip link`
**Gestisce le interfacce di rete**
- 🔍 **Mostra interfacce**  
    `ip link` (o `ip link show`)  
    → Elenca tutte le interfacce di rete
- 📊 **Mostra statistiche**  
    `ip -s link show dev eth0`  
    → Statistiche RX/TX (byte, pacchetti, errori, ecc.)
- ⛔ **Disattiva interfaccia**  
    `sudo ip link set eth0 down`
- ✅ **Riattiva interfaccia**  
    `sudo ip link set eth0 up`
### 🔹 `ip address`

**Mostra o gestisce indirizzi IP associati alle interfacce**
- 🔍 **Mostra indirizzi IP**  
    `ip address` (o `ip addr show`)  
    → Elenca indirizzi IPv4/IPv6 di tutte le interfacce
- 🔎 **Filtri utili**
    - `ip address show up` → Solo interfacce attive
    - `ip address show dev eth0` → Solo `eth0`
    - `ip address show scope global` → Solo globali
    - `ip address show to 172.0.0.0/8` → Solo questo range
### 🔹 `ip route`
**Gestisce la tabella di routing (instradamento)**
- 🔍 **Mostra tabella di routing**  
    `ip route`  
    → Mostra le rotte (es. default, reti locali)
- 📁 **Salva e ripristina la tabella di routing**
    `ip route save > route.txt sudo ip route flush table main sudo ip route restore < route.txt`
- 🔎 **Filtri utili**
    - `ip route show dev eth0` → Solo rotte per `eth0`
    - `ip route show via 172.0.0.0/8` → Next hop nel range
    - `ip route show to root 0/0` → Tutte le rotte (default + locali)
- 📦 **Trova la rotta per una destinazione**  
    `ip route get 8.8.8.8`  
    → Mostra via quale interfaccia/gateway va un pacchetto
### 🔹 `ip neighbour`
**Gestisce la tabella ARP (associazioni IP-MAC)**
- 🔍 **Mostra tabella ARP**  
    `ip neigh` (o `ip neigh show`)  
    → Mostra IP, MAC e stato (es. `REACHABLE`)
- 🔎 **Filtri utili**
    - `ip neigh show dev eth0` → Solo `eth0`
    - `ip neigh show to 172.0.0.0/8`
    - `ip neigh show nud reachable` → Solo MAC raggiungibili
- 🔎 **Consulta una specifica entry ARP**  
    `ip neigh get 172.21.240.1 dev eth0`  
    → Mostra il MAC per un IP noto
- 🧹 **Svuota la tabella ARP**
    - Tutto: `sudo ip neigh flush dev eth0`
    - Solo voci "vecchie": `sudo ip neigh flush nud stale dev eth0`
## Comandi per il networking virtuale 
### 🔸 1. **Network Namespace (netns)**
Uno **stack di rete isolato**: ogni host virtuale avrà il suo.
- ➕ **Creazione**:
    `sudo ip netns add hostA`
- 🔍 **Lista dei namespace**:
    `ip netns list`
- ❌ **Eliminazione**:
    `sudo ip netns del hostA`
- 🖥️ **Avviare una shell in un namespace**:
    `sudo ip netns exec hostA /bin/bash`
- ▶️ **Eseguire comandi in un namespace**:
    `sudo ip netns exec hostA <comando>`
### 🔸 2. **Interfacce Virtuali (veth)**

Simulano un cavo Ethernet tra due dispositivi/namespace.
- ➕ **Creazione di una coppia veth**:
    `sudo ip link add vethA type veth peer name vethA-switch1`
    
- ❌ **Eliminazione di un veth**:
    `sudo ip link del vethA`
    
- 🔁 **Spostare una veth in un namespace**:
    `sudo ip link set vethA netns hostA`
### 🔸 3. **Bridge di rete (switch virtuale)**

Simula uno switch Ethernet.
- ➕ **Creazione del bridge**:
    `sudo ip link add name switch1 type bridge`
    
- 🔗 **Collegare le veth al bridge**:

    `sudo ip link set vethA-switch1 master switch1`
    
- ✅ **Attivare bridge e interfacce**:

    `sudo ip link set switch1 up sudo ip link set vethA-switch1 up`
### 🔸 4. **Configurazione rete nel namespace**

- 🖥️ **Rinominare vethA in `eth0` nel netns hostA**:
    `ip netns exec hostA ip link set vethA name eth0`
    
- 🌐 **Assegnare indirizzo IP e attivare interfacce**:

    `ip netns exec hostA ip addr add 10.0.1.10/24 br+ dev eth0 ip netns exec hostA ip link set eth0 up ip netns exec hostA ip link set lo up`
### 🔸 5. **Router virtuali**

- ➕ **Creazione namespace del router**:

    `sudo ip netns add router2`
    
- 🌐 **Assegnare IP e attivare interfacce del router**:

    `ip netns exec router2 ip addr add 10.0.2.1/24 dev vethR2S2 ip netns exec router2 ip link set vethR2S2 up ip netns exec router2 ip link set lo up`
    
- 🔁 **IP forwarding nel router**:

    `ip netns exec router2 sysctl -w net.ipv4.ip_forward=1`
    
- 📍 **Aggiungere rotte statiche nel router**:

    `ip netns exec router2 ip route add 10.0.1.0/24 via 10.0.4.1 ip netns exec router2 ip route add 10.0.3.0/24 via 10.0.4.6`

### 🔸 6. **Instradamento degli host**

- ➡️ **Aggiunta della rotta di default**:

    `ip route replace default via 10.0.1.1`

### TRACEROUTE
### 📌 COSA FA `traceroute`
- Mostra il **percorso (hop per hop)** che i pacchetti fanno da te verso una destinazione (es. `www.google.it`)
- Ogni riga = un router attraversato
- Viene usato il **TTL (Time To Live)** per forzare la risposta dei router intermedi

## 🔧 **COMANDI PRINCIPALI**

### 🔹 1. **Installazione (se serve)**

`sudo apt install inetutils-traceroute`
### 🔹 2. **Uso base**

`traceroute www.google.it`
- Mostra fino a 64 hop
- Per ogni hop: 3 tentativi (RTT - round trip time)
- `*` = nessuna risposta (può essere firewall o perdita)
### 🔹 3. **Protocollo alternativo: ICMP**
`traceroute -M icmp www.google.it`
- Usa pacchetti **ICMP Echo Request** (come `ping`)
- Permette di confrontare i percorsi ICMP vs UDP
- **Percorsi diversi** ⇒ routing diverso per tipo di pacchetto
### 🔹 4. **Limitare numero massimo di hop**
`traceroute -m 2 www.google.it`
- Mostra solo i primi 2 hop
- Utile per debug dei primi passaggi di rete
- Se non arriva a destinazione, lo vedi dal codice di uscita:
    `echo "$?"  # 0 = successo, 1 = fallito`
### 🔹 5. **Ping con TTL personalizzato**

`ping -t 13 -c 1 142.250.180.131`

- Limita TTL a 13
- Se TTL è troppo basso, ricevi errore `Time to live exceeded`
- Verifica con:
    bash
    CopiaModifica
    `echo "$?"  # 0 = ricevuto, 1 = fallito`
### 🕵️‍♂️ **Con Wireshark**
- Cattura i pacchetti durante il `traceroute`
- Vedrai:
    - UDP con TTL crescente (1, 2, 3…)
    - ICMP “TTL Exceeded” dai router intermedi
    - ICMP “Port Unreachable” dal server finale (perché la porta è casuale, tipo 33434)
## ROUTING
## 🧠 TEMA: **Tabella di instradamento e invio pacchetti**
### 🔹 1. COMANDO `ip route`
Visualizza la **tabella di instradamento**, cioè l’elenco delle reti raggiungibili e come raggiungerle.

Esempio:
`$ ip route default via 172.20.0.1 dev eth0 172.20.0.0/20 dev eth0 src 172.20.4.226 172.30.0.0/20 dev eth1 src 172.30.1.5 172.50.0.0/20 via 172.30.0.1 dev eth1 172.50.8.0/24 via 172.20.0.10 dev eth0`

📌 **Tipi di rotta:**

- **Diretta (scope link)** → la rete è sulla stessa interfaccia
    
- **Indiretta (via …)** → serve un router
    
- **Default route** → usata se nessuna altra corrisponde
    

📌 **Regola importante:**  
👉 Viene scelta la **rotta con il prefisso più lungo** (longest prefix match).
### 🔹 2. COMANDO `ip route get <IP>`

Mostra **la rotta selezionata per un indirizzo specifico**, es:

`ip route get 172.20.5.10`

- Mostra interfaccia (`dev`)
    
- Indirizzo sorgente (`src`)
    
- Router (`via`, se presente)
    

---

### 🔹 3. CASI PRATICI (semplificati)

#### 🅰️ `172.20.5.10`

- Appartiene alla rete `172.20.0.0/20`
    
- Rotta diretta → `dev eth0`, `src 172.20.4.226`
    
- Invio diretto senza router
    

#### 🅱️ `172.20.26.10`

- **Non** appartiene a `172.20.0.0/20`
    
- Usata la **default route** → via `172.20.0.1` su `eth0`
    
- Rotta indiretta (passa da router)
    

#### 🅾️ `172.50.0.7`

- Appartiene a `172.50.0.0/20`
    
- Rotta via `172.30.0.1` → `dev eth1`, `src 172.30.1.5`
    
- Rotta indiretta (passa da router)
    

---

### 🔹 4. INDIRIZZI A LIVELLO IP E MAC

Quando un host manda un pacchetto:

#### ✅ Livello **IP** (rete):

- **sorgente**: scelto da `src` nella rotta
    
- **destinazione**: IP finale, **non cambia** durante l'instradamento
    

#### ✅ Livello **MAC** (collegamento):

- **sorgente**: MAC dell’interfaccia usata (`ip link`)
    
- **destinazione**:
    
    - se **rotta diretta** → MAC del destinatario
        
    - se **rotta indiretta** → MAC del **router (next hop)**
        

🛠️ Se MAC non noto → cercato in **tabella ARP** oppure inviando **richiesta ARP**
### 📌 RICORDA

- Router cambiano solo gli indirizzi **MAC**, **non** quelli **IP**
    
- La scelta del `src` dipende sempre dalla **rete associata all’interfaccia**
    
- Se più rotte corrispondono, vince quella con **prefisso più lungo**

## 🧠 ARGOMENTO: Virtual networking (parte 2), ARP, ping, traceroute

---

### 🧰 **1. Network namespace: shell dedicata**

- Per entrare in una shell nel namespace `hostA`:
    
    bash
    
    CopiaModifica
    
    `sudo ip netns exec hostA /bin/bash`
    
- Per farlo **con l’utente corrente** e prompt personalizzato:
    
    bash
    
    CopiaModifica
    
    `PS1='\u@$(ip netns identify $$):\W] ' sudo ip netns exec hostA sudo -u $USER /bin/bash --noprofile --norc`
    

---

### 🧭 **2. Routing base: Host A**

bash

CopiaModifica

`ip route`

- `10.0.1.0/24` → diretto via `eth0`
    
- `default via 10.0.1.1` → gateway per tutte le reti esterne
    

---

### 🧹 **3. Tabella ARP**

- Visualizza ARP:
    
    bash
    
    CopiaModifica
    
    `ip neigh`
    
- Svuota tabella:
    
    bash
    
    CopiaModifica
    
    `sudo ip neigh flush dev eth0`
    

---

## 🧪 ESEMPIO 1: **Ping da Host A a Host B** (stessa sottorete)

### 📦 Pacchetti scambiati:

1. **Richiesta ARP** per trovare MAC di `10.0.1.20`
    
2. **Risposta ARP** → IP `10.0.1.20` = MAC `42:3e:e5:36:27:f9`
    
3. **ICMP Echo Request**
    
4. **ICMP Echo Reply**
    

📌 IP: da `10.0.1.10` a `10.0.1.20`  
📌 MAC: da Host A → Host B

👉 **Instradamento diretto**

---

## 🧪 ESEMPIO 2: **Ping da Host A a Host F** (rete diversa)

### 📦 Pacchetti scambiati:

1. ARP per trovare MAC di `10.0.1.1` (il **router**)
    
2. Risposta ARP
    
3. ICMP Echo Request
    
4. ICMP Echo Reply
    

📌 IP: da `10.0.1.10` a `10.0.3.20`  
📌 MAC (primo tratto): da Host A a Router 1

👉 **Instradamento indiretto via router**

---

## 🛰️ Router 1: inoltro pacchetti

- Inoltra l’Echo request a `10.0.3.20` passando per `10.0.4.2`
    
- Verifica e aggiorna MAC via ARP
    
- ICMP **non cambia IP**, ma **cambia MAC** a ogni hop
    

---

## 🔎 Traceroute da Host A a Host F

bash

CopiaModifica

`traceroute 10.0.3.20`

Esempio output:

CopiaModifica

`1  10.0.1.1 2  10.0.4.2 3  10.0.4.6 4  10.0.3.20`

---

## 📡 arping – Test ARP manuali

### ✅ Richiesta ARP (manuale)

bash

CopiaModifica

`sudo arping -c 1 10.0.1.20`

### ✅ Probe ARP (controlla se un IP è già usato)

bash

CopiaModifica

`sudo arping -I eth0 -c 1 -S 0.0.0.0 10.0.1.10`

### ✅ Announcement ARP (annuncia IP con MAC aggiornato)

bash

CopiaModifica

`sudo arping -I eth0 -c 1 -A 10.0.1.10`

📌 Serve per **aggiornare la tabella ARP degli altri host** se qualcuno ha una voce vecchia.

---

## 🧪 Caso avanzato: sostituzione entry ARP

### Forzare entry nella tabella ARP:

bash

CopiaModifica

`ip neigh replace 10.0.1.10 lladdr 11:11:11:11:11:11 nud reachable dev eth0`

### Reset comportamento ARP:

bash

CopiaModifica

`sudo sysctl -w net.ipv4.conf.eth0.arp_accept=1`
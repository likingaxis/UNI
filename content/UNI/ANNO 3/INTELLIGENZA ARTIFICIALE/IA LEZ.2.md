- differenza tra un software tradizionale e un software AI
	- il software AI é un software che non lavora in isolamento, lavora in un ambiente che agisce in autonomia, lui riceve segnali dall'ambiente e ne risponde
		- è piu simile a un S.O rispetto a un software classico
		- l'agente non puo sapere prima le domande
		- l'agente puo avere degli effettori, coloro che consentono a lui di effettuare azioni fisiche
		- sensori, apparati in grado di vedere l'ambiente e riconoscerlo adeguatamente
		- Ciclo dell'agente
			- percepire una azione mediante i sensori
			- decido
			- agisco con una azione
			- si aggiorna
		- gli agenti hanno obiettivi e una percezione adeguata ma anche parziale del mondo esterno
			- il mondo esterno non è però una copia 1:1 bensi una copia senza tutte le informazioni, che vengono aggiunte in modo dinamico e astratto una volta che mi accorgo della loro necessità
### PERCEZIONI E AZIONI
- Percezione
- Sequenza
- l'azione è esclusivamente dopo una Percezione
### Agenti Razionali
- Un agente ha una razionalita
	- scopo o scopi del singolo agente
	- Un agente intelligente=Un agente razionale
	- gli agenti lavorano su un criterio approssimato che cerca l'ottimalita su diverse scelte
		- ci sono piu vie 
		- vado a approfondire la cosa se ogni scelta ha probabilità identiche
##### Valutazione della prestazione
- ho diverse metodologie per dare una valutazione a una prestazione attuabile
	- devono funzionare su ambienti diversi, non una sola partita ma tutte le istanze possibili
### Un agente razionale
- la razionalità relativa a
	- la misura di prestazioni che hanno successo
	- le conoscenze pregresse dell'ambiente
	- le percezioni presenti e passate
	- le capacita dell'agente
- per ogni percezione deve compiere l'azione che massimizza il valore atteso della misura delle prestazioni, sfruttando percezioni passate e la conoscenza passata
	- diff tra percez passate e conoscenza passata
- non deve sempre fare le cose giuste per essere razionale
	- se non sa deve apprendere da risorse dati ecc, comunque dall'ambiente esterno
### Agenti autonomi
- lavorano in autonomia
	- mentre decide deve essere autonomo, possiamo pero manipolarlo perche cmq e un collaboratore
# AMBIENTE E CODIFICA PEAS
un ambiente è caratterizzato da una dimensione di 4 cose
- Prestazioni
	- obiettivi
- Ambiente
	- descrizione 
- Attuatori
	- componenti da usare per fare azioni
- Sensori
	- componenti per percepire dall'ambiente
ESEMPIO DI AMBIENTE CHAT GPT
- vedi slide
### Problema P dell'agente
- un problema P per un agente parte sicuramente da una caratterizzazione adeguata dell'ambiente
### UN ambiente e il problema hanno diverse proprieta
- completamente o parzialmente osservabile
- agente singolo o multiplo
	- agente non indicava multiple ia?
- deterministico, stocazzo, non deterministico
	- il primo e se sono sicuro al 100% di cosa succede
	- stocazzo se ho una certa prob
	- non det se ho difficolta a determinare cosa deve avvenire
- episodico vs sequenziale
	- episodico quando decisioni sono prese singolarmente
	- sequenziale decisioni in sequenza
- statico o dinamico
	- definiti da un cambiamento ambientale o meno
	- statico quando l'agente va piu veloce dei cambiamenti quindi non cambia l'ambiente ecc
	- dinamico quando le scelte vanno di paripasso ai cambiamenti dell'ambiente
		- tipo taxi autonomo
	- semi dinamico, l'ambiente non cambia ma la valutazione dell'agente si
- discreto o continuo
	- discreti, ambienti di esame
		- modificano ogni tot tick o scansioni e transizioni temporali
		- continuo quando le variabile vengono descritte da numeri reali
### Osservabilità dell'ambiente
- completamente osservabile
- parzialmente osservabile
## Come automatizzare un ambiente
- attraverso uno strumento software che vuole:
	- generare stimoli per gli agenti
	- raccogliere le azioni in risposta
	- aggiornare il proprio stato
	- attivare altri processi implicati dal cambiamento effettuato
	- valutare le prestazioni degli agenti
### AGENTE
architettura+programma
funzione che prende percezioni e manda in output azioni
una funzione di un agente prende in input una percezione
manda in output una azione
ha una memoria che deve aggiornare
effettua una azione scegliendo la migliore
aggiorna la memoria a seguito di una azione
restituisco l'azione
****
![[Pasted image 20250710194121.png]]
1. per identificarle raccogli i vari dispositivi di rete tranne gli host e raccogli nello stesso insieme se non ci sono router
2. da H1 viene inviato un messaggio broadcast che raggiunge H2 e S1
	- da S1 viene rifatta la stessa cosa e arriva a S2
	- da S2 la stessa cosa e raggiunge H3 e R1
		- R1 è di terzo livello e non può continuare l'operazione
		- H3 risponde con il suo indirizzo MAC con ARP reply
			- e viene ripercorso il tutto fino a raggiungere H1
3. non può perché appartiene a un'altra sottorete e c'è un router di livello 3



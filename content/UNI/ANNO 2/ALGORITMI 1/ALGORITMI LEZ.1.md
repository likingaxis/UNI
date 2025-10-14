# INTRODUZIONE
[[Introduzione_2024.pdf|pdf della lezione 1]]
>[!info]- cos'è un algoritmo
>È l'essenza computazionale di un programma, il procedimento per giungere a una soluzione di un problema di calcolo

### Un algoritmo deve essere:
- stabile
- modulare
- mantenibile
- user-friendly
- sicuro
- corretto
### I CONCETTI FONDAMENTALI
- problema: la cosa da risolvere
- istanza: oggetto in causa con conseguente problema
- dimensione dell'istanza: dimensione dell'oggetto
- modello di calcolo: elemento di utilizzo per risolvere il problema
- algoritmo: strategia da applicare con le cose che abbiamo
- correttezza dell'algoritmo: deve funzionare per qualsiasi istanza
## ESERCIZI
#### ESERCIZIO MONETA FALSA
>[!bug] vedi esercizio degli algoritmi delle monete di paperone alla slide 1 del prof a pagina 27 

#### ESERCIZIO SULLE FRITTELLE
>[!bug]  ![[Pasted image 20241008175847.jpg|200]]
>Si devono cuocere n frittelle. Si ha a disposizione una padella che
riesce a contenere due frittelle alla volta. Ogni frittella va cotta su
tutte e due i lati e ogni lato richiede un minuto.
Progettare un algoritmo che frigge le frittelle nel minor tempo
possibile. Si argomenti, se possibile, sulla ottimalità dell’algoritmo
proposto.

### SOLUZIONE
- Problema: cuocere n frittelle da entrambi i lati
- Istanza: n frittelle ognuna si deve cuocere ad ogni lato e ci vuole 1 minuto
- dimensione dell'istanza: n
- modello di calcolo: una padella che puo' contenere 2 frittelle per volta
- algoritmo: dividiamo per 2 le frittelle, così facendo dimezziamo la superficie e il tempo
```
ALG1(x)
x=n
If x dispari
Divide x-1 in gruppi x1,xn-1 e y=1
For i=1 to n do
	Tempo=cuoci(xi,xi+1)/2
Return Tempo+y

If x pari
Dividi x in sotto gruppi x1...xn 
For i=1 to n do
	Tempo=cuoci(xi,xi+1)/2
return Tempo
```

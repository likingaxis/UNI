## LISTA ESERCIZI
1. vettore può essere soluzione di base ammissibile?
2. vertice della regione ammissibile del problema con x1 e x2 strettamente positivi
3. può esistere una soluzione ottima con x3 in base?
	- cosa succede se ho due variabili nel vincolo che voglio del duale?
4. può esistere una soluzione ottima con x1 e x2 strettamente positivi
5. algoritmo del simplesso a 2 fasi
6. simplesso
7. simplesso primale-duale a partire da una soluzione duale y
8. verificare se le soluzioni del punto a sono ottime
	- applicare le condizioni di complementarietà primale-duale per verificare se la soluzione x è ottima(dato un vettore) uguale al punto 8
9. come si fa il duale
10. forma standard

## 1. vettore può essere soluzione di base ammissibile?
l'esercizio sarà tipo così
![[Pasted image 20250516200722.png]]
1. sostituisco le rispettive x nel vettore sul problema di program lineare
2. 4 corrisponde a x1 0 corrisponde a x2 e così via...
3. verifico se la disequazione ha senso
4. faccio la forma standard
5. sostituisco pure nella forma standard il vettore
6. gli slack in più vengono recuperati facendo sostituzioni
7. creo il nuovo vettore con in più anche i valori degli slack
8. controllo se il numero dei vincoli è uguale a quello delle variabili diverse da 0 nel vettore
9. se sono diverse no SBA se uguali SBA
## 2.vertice della regione ammissibile del problema con x1 e x2 strettamente positivi
![[Pasted image 20250516201309.png]]
1. si pongono le variabili richieste x1 e x2 a > di 0 e tutte le altre a 0
2. si sostituisce così nella forma standard
3. ciò che rimane è tutto tranne x1 e x2 perché gli altri sono a 0
4. si mettono a sistema con l'uguale i vincoli
5. svolgi il sistema
6. il sistema ti dirà quanto valgono x1 e x2
7. confronta i loro valori con le variabili del programma lineare
8. in questo esempio x1 e x2 devono essere >= di 0
9. in questo caso li chiede strettamente positivi quindi non possono essere uguali a 0
## 3.Può esistere una soluzione ottima con x3 in base?
![[Pasted image 20250516201931.png]]

1. fai il duale non a partire dalla standard
2. da min a max
3. selezioni la riga della base richiesta in questo caso x3
4. svolgi la disequazione 
5. la disequazione deve rispettare le variabili nel problema di programmazione lineare

- cosa succede se ho due variabili nel vincolo che voglio del duale?
## 4. può esistere una soluzione ottima con x1 e x2 strettamente positivi
![[Pasted image 20250517121144.png]]
1. fai il duale
2. definisci la complementarietà delle due variabili che ti ha detto il prof e mettile positive
3. sostanzialmente devi scrivere questo
![[Screenshot_2025-05-17-12-39-52-88_45415775811cea13943236d9369df411.jpg]]
4. metti a sistema i due vincoli con l'uguale al posto dei segni delle disequazioni
5. svolgi il sistema
6. le variabili del sistema devono rispettare i segni iniziali che avevi sul duale quindi se Y1 è uguale a 1/2 e nel duale avevi scritto che doveva essere $\leq 0$ allora significa che c'è una contraddizione e non esiste soluzione ottima
## 5. algoritmo del simplesso a due fasi
quando il prof chiede il simplesso duale fai questo
![[Pasted image 20250517124350.png]]
1. fai la forma standard
2. se nella forma standard hai degli slack negativi allora significa che la base non è ottima
3. applichi il simplesso a 2 fasi
4. fase 1, poni come obiettivo facendo il min con le variabili che hai che non vanno bene
![[Pasted image 20250517124650.png]]
5. in questo caso il problema era su solo un vincolo e quindi faccio
![[Pasted image 20250517124706.png]]
6. aggiungo solo una variabile artificiale
7. successivamente riprendo i vincoli fatti prima ma aggiungo al vincolo quello strano la variabile artificiale(proprio al sommo se vedi)
8. da qui effettuo il simplesso però senza sostituire S1 alla funzione z
9. devo sottrarre il vincolo con S1 con l'obiettivo per togliere 1 su S1
![[Pasted image 20250517124902.png]]
10. successivamente faccio un simplesso normale finché la b di z non torna uguale a 0
11. dopo essere arrivati qui prendo la vecchia funzione obiettivo della forma standard e la sostituisco alla riga di z
12. faccio il simplesso finché non ho tutte le variabili di z maggiori o uguali a 0
13. in questo caso $\geq$ perché abbiamo la standard in forma di min se fosse stato max tutte le variabili dovevano essere $\leq$ 

## 6. simplesso normale
per fare il simplesso bisogna
1. forma standard
2. metti tutto a tabella
![[Screenshot_2025-05-17-13-04-28-00_45415775811cea13943236d9369df411.jpg]]
3. devi trovare sulla riga obiettivo il valore più piccolo
4. successivamente devi trovare la corrispondente riga degli altri e per farlo devi prendere i termini noti di ogni vincolo e farlo fratto la colonna scelta, se però devi fare una frazione negativa o con lo 0 non lo prendi in considerazione
![[Screenshot_2025-05-17-13-11-35-32_45415775811cea13943236d9369df411.jpg]]

5. ora abbiamo definito esattamente quale è il pivot
6. una volta scelto il pivot faccio tutta la riga scelta fratto il pivot scelto, se è 1 fai tutto fratto 1, quindi in questo caso tutta la riga di x6 fratto il pivot 1
7. inoltre scrivi che la variabile della riga ora diventa quella della colonna scelta
![[Screenshot_2025-05-17-13-15-35-05_45415775811cea13943236d9369df411.jpg]]
8. cancello tutte le righe tranne quelle che nella colonna scelta hanno già coefficiente zero
9. per ricreare la riga faccio un giochetto
10. se ad esempio voglio riscrivere b di z prendo l'elemento della riga scelta sulla colonna di b lo moltiplico per la riga corrispondente a z negando tutto e poi sommo con la b di z iniziale
![[Screenshot_2025-05-17-13-15-52-34_45415775811cea13943236d9369df411.jpg]]
11. lo fai per tutte le righe e tutte le colonne che hanno il coefficiente della colonna diverso da 0
12. riempio una tabella nuova praticamente
13. una volta fatto controlli se la funzione obiettivo era un min tutti i valori devono essere $\geq0$ se era un max tutti devono essere $\leq0$ 
14. poi scrivi alla fine dell'esercizio 
![[Screenshot_2025-05-18-12-27-39-82_45415775811cea13943236d9369df411.jpg]]

## 7. simplesso primale-duale a partire da una soluzione duale y
1. fare la forma standard
2. Duale della forma standard
3. prendi il vettore fornito oppure inventalo tu e sostituiscilo al duale fatto se non ti viene fornito un vettore metti 0,0 a caso
4. dopo aver sostituito al duale vedi se ammissibile, ti devono tornare tutte le disuguaglianze
![[Screenshot_2025-05-17-20-10-16-86_45415775811cea13943236d9369df411.jpg|400]]
5. se si prendi e isola le variabili del duale
6. se la risposta è no devi definire una nuova base e poi fai il punto 5
![[Screenshot_2025-05-17-20-10-06-86_45415775811cea13943236d9369df411.jpg|400]]
7. primale ristretto lo fai sempre in min e metti tante a quante le variabili con scritto NO
8. la forma sarà così devi prendere quante variabili quanti NO
9. poi sostituisci e metti a 0 nella forma standard e le variabili con no le lasci libere
10. riscrivi aggiungendo le a
![[Screenshot_2025-05-17-20-45-49-35_45415775811cea13943236d9369df411.jpg]]
11. faccio il tableaux e come sempre cerco di togliere i valori alle a
![[Pasted image 20250517212305.png]]
12. sostanzialmente faccio il simplesso se z diventa uguale a 0 allora significa che la y scelta è base ottima
13. altrimenti devo scegliere la nuova base $Y^1=Y^0+\Theta \pi$ 
14. per trovare $\pi$ faccio il duale del primale ristretto
![[Pasted image 20250517212715.png]]
15. di tutto questo prendo in considerazione solo le variabili che stavano a sinistra del tableaux uscito male quindi in questo caso sono a1 e a2 e le metto uguali a 1
16. saranno i valori di $\pi$
![[Pasted image 20250517212819.png]]
17. prendo il duale fatto all'inizio e ci sostituisco i valori del nuovo $Y$ per vedere se tornano le disuguaglianze mettendole su un grafico dei segni
18. sostanzialmente bisogna vedere se nel grafico si hanno le intersezioni di tutte le disuguaglianze e si deve prendere quel punto per trovare il valore di theta
19. in questo caso theta è 1/4 e viene sostituito nel vettore $Y$
![[Pasted image 20250517213115.png]]
20. per verificare ora devi ripartire dal punto 6 ma sicuramente esce base ottima(spero)
## 8. verificare se le soluzioni del punto a sono ottime
oppure 
- applicare le condizioni di complementarietà primale-duale per verificare se la soluzione x è ottima(dato un vettore) uguale al punto 8
1. sostituisci il vettore al problema di programmazione lineare originale e vedi se c'è ammissibilità vedendo se le disuguaglianze tornano 
2. faccio il duale senza forma standard
3. applico la complementarietà
4. raccolgo moltiplicando alle y i vincoli del programma lineare classico
![[Screenshot_2025-05-18-14-49-22-58_45415775811cea13943236d9369df411.jpg]]
5. Y3 è appartenente ai reali quindi non la prendo in considerazione
6. ora faccio la stessa cosa mettendo tra parentesi i vincoli del duale e fuori le x della forma normale
![[Pasted image 20250518145116.png]]
7. in questo caso il vincolo che appartiene ai reali lo metto un attimo da parte 
8. metto a sistema i due tipi di raccoglimenti fatti e applico il vettore sulle rispettive x
9. quello che prendeva i vincoli della forma normale verrà come il primo sistema mentre l'altro è il secondo
10. da questi sistemi possiamo trarre quanto valgono le varie y in base al fatto se si saturano o mento ovvero se c'è uno zero o meno
![[Pasted image 20250518145313.png]]
11. ora posso aggiungere quella riga che nel raccoglimento con i vincoli del duale avevo tolto perché aveva i reali
12. ci posso ora sostituire i valori delle y trovati
13. controllo se le y rispettano le variabili scritte sul duale
14. ora che ho tutti i valori delle y posso sostituirli al duale e controllare se le disuguaglianze tornano
15. metto a sistema gli obiettivi del duale e del programma lineare e vedo se sostituendo vengono uguali

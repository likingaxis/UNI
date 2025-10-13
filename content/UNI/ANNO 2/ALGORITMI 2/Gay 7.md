## Problema dei k-centri (2-approximation)
***DEFINIZIONE***
> Dati un set di `n` siti $s_{1}, ..., s_{n}$ e un intero `k` $> 0$.
> selezionare `k` centri `C` affinché la distanza tra un sito e il centro più vicino sia minima.

![[Pasted image 20250828105024.png]]

>[!tip] `r(C)` indica la distanza peggiore tra tutte le `dist(s_i, C)`
>Nel senso
>- calcola TUTTE le distanze dei siti dai centri più vicini
>- prendi la peggiore -> quella è `r(C)`
>- così tu sai che il minimo raggio di copertura per coprire tutti i siti è questo valore qui
 
#### Algoritmo greedy
Sceglie `k` volte il sito più lontano da qualsiasi centro finora creato, e lo usa come prossimo centro.
![[Pasted image 20250828105111.png]]


>[!lemma] ![[Pasted image 20250906111611.png]]
>L'algoritmo greedy potrebbe non essere ottimo ma la sua soluzione non si discosta più del doppio rispetto all'ottimo.
>
>DIMOSTRAZIONE
>1. Per assurdo ipotizziamo che l'ottimo sia molto più piccolo $$r(C^{*}) < \frac1 2 r(C)$$
>	- ossia il centro ottimale copre con sfere grandi la metà di quelle del greedy
>2. Costruiamo sfere intorno ai centri trovati $c \in C$, con raggio $\frac1 2 r(C)$
>	- in questa nuova sfera deve esserci ALMENO un centro ottimo $c_{i}^{*}$ altrimenti l'ipotesi sarebbe sbagliata
>3. Tutte le sfere, per costruzione, sono disgiunte (non si sovrappongono) e quindi in ognuna c'è ESATTAMENTE un centro ottimale
>	- quindi c'è una corrispondenza tra i centri di `C` e quelli di `C*`, in particolare $$|C| = |C^{*}|$$
>4. Ora colleghiamo un sito `s` al suo centro
>	- prendiamo un sito `s`
>	- sia $c_{i}^{*}$ il centro ottimo più vicino a `s`
>	- e sia $c_{i}$ il centro di `C` che "si abbina a $c_{i}^{*}$" (ossia che si trova nella stessa sfera)
>	- LA DISTANZA DI `s` dal centro $c_{i}$ trovato dal greedy soddisfa $$dist(s,C) \le dist(s, c_{i}^{*}) + dist(c_{i}^{*}, c_{i})$$
>		- la prima parte $dist(s, c_{i}^{*})$ è al massimo $r(C^{*})$, per definizione
>		- la seconda parte $dist(c_{i}^{*}, c_{i})$ anche è al massimo $r(C^{*})$, perché i due centri si trovano nella stessa sfera
>5. QUINDI la distanza totale è $$dist(s, C) \le 2 \cdot r(C^{*})$$
>6. E QUESTO VALE PER OGNI SITO `s`


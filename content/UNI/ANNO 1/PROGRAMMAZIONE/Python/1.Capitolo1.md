In questo capitolo vedremo i seguenti argomenti:
Cicli, dati, condizioni, input, output, costi computazionali

### I dati

# int 
```python
p=5
```
# float
```python
x=3.5
```
# lista-modificabile
```python
a=[3,4,5]
```
# tuple
```python
b=(3,4,5)
```
**tuple non modificabili** 
# dictionary
```python
c={"chiave":"valore","chiave1":"valore2"}
```

## Le condizioni
### if, else ed elif
```python

if p>0:
  print('ciao')
else: 
  print("suca")

#elif
if p>0:             
                
  print('ciao')
elif p>1:
  print(3)
```
## costo computazionale:
### anche se bruno lo ha spiegato meglio

***I programmi hanno un costo computazionale "sprecano" risorse temporali e spaziali.
 Temporali: tempo per es eguire il programma
 Spaziale: la memoria che utilizzano in più
 Le unità di misura sono:
 O: quando non siamo sicuri del costo effettivo (limitazione massima)
 Theta: quando ne siamo sicuri (esattamente)***

## i cicli:
```python

k='giuseppe'
n=len(k) #n=lunghezza di k, esempio dell'etichetta

for i in k:      #i è una variabile temporale muore out ciclo
                  #costi computazionali: temp:Theta(n) perchè
                  #siamo esattamente sicuri di quanto il for 
                #ci mette, tira dritto fino all'ultimo elemento
                    #spaz:O(1)
  if i=="c":    #costa temp: O(1), siccome nel for Theta(n)
    print("c'è la c")
#se qua si mettesse "break"interrompe il ciclo quando si 
#verifica la condizione rende il costo del ciclo O(n)
  print(i)
#utilizzo di "in"
q='giuseppe'
if k in q:
  print("ciao")

#while
y=3
while y==3:         #costo temp:O(n) e spaz:O(1)
  print("cacchina")
  y+=1
#input by luca gugliottong
m=input("inserisci qui la parola")
print(m)
```

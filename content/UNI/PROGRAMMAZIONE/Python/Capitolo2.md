# ARGOMENTI
Stringhe, funzione, frame, liste, tuple  

# stringhe
```python
le stringhe sono contenitori con all'interno caratteri
a="hey"  #cosa fa il pitone? prende char per char 
print(a)
print(a[0])
```
###  confronto tra stringhenx
```python
b="ciao"
if a>b:
  print(a>b)    #output:True costi spaz: O(1) temp:O(n) n=len più piccola

```
### confronto tra due stringhe semi uguali
```python
p="ciaox"
o="ciao"
print(p>o) #printerà True

```
# le funzioni
# la join  
##### costo temp:O(n*m)  spaz:O(n*m)
```python
a="-."
b="ciao"
l=a.join(b)
print(l)
#output:c--..i--..a--..o  #ad ogni carattere di b mette a
```
## strip    toglie i valori cercati a dx e sx finchè non trova altro
###### negli argomenti mettiamo ciò che ci serve togliere
```python
txt = ".....banana...."

x = txt.strip(".")

print("k", x, "frakka")
```
# slicing a[start: stop: step]  
### se stop è -1 mi farà default -1
### se step è -1 mi farà passi indietro
```python
a="ciaop"
print(a[::-1])
```
### lower/upper  ritorna una stringa min o maiusc
```python
a="ciAo"
print(a.upper())
print(a.lower())
```
### replace  sostituisce parola con un'altra

```python
m="odio i jilinx"
print(m)
print(m.replace("odio","amo"))
```
### split separa la stringa in base a quello che hai e mette parola per parola e la trasforma in una lista di default spazi
```python
txt = "luca fai schifo"

x = txt.split()

print(x)
```

## confronto tra stringhe esercizio

```python
a="papaaa"
b="papa"
k=False
i=0
m=len(a)
n=len(b)
while(k is False ):
  if i in (m, n):
    if len(a)>len(b):
      print("a è >b")
      break
    elif len(a)<len(b):
      print("a è <b")
      break
  if a[i]>b[i]:
    print("a è >b")
    k=True
  elif a[i]<b[i]:
    print("a è <b")
    k=True
  else:
    i+=1
```
# Le funzioni:
le funzioni servono per creare delle azioni che il programmatore può usare più volte, richiamandolo, quindi se vogliamo creare una somma tra elementi basta creare una funzioneng

### esempio:
```python
''' def indica che è una funzione somma è il nome          che vogliamo dargli le parentesi,servono per passare i     parametri
'''
def somma(a,b):
                 
  return a+b            

x,y=int(input()),int(input())
print(somma(x,y))
```
### framing, come funziona?
#esistono le funzioni locali e globali
#esiste il global frame(prende i valori del main)
#le variabili locali sono quelle variabili che vengono usate all'interno delle funzioni e non vengono ritornate

#LISTE
#Liste,sono mutabili,ci puoi fa dei metodi,
#sono una raccolta indicizzata di dati 0,1,2...
#puoi ritornare quel valore in quell'indice
#possono avere dati diversi dentro
a=[]
a=[2,3,4,"ciao","b"]
#append costo O(1)
a.append(3)
print(a)
#len lunghezza
print(len(a))
#slicing si
print(a[:])
#extend aggiunge liste alla fine
b=[3,4,5,6]
a.extend(b)
#del e remove e pop
del a #elimina e sposta
a=[5,3,3]
del a[0]
print(a)
#rimuove il primo che trova
a.remove(3)

#pop rimuove la fine e la ritorna
print(a.pop())

#insert,copy,sort,reverse,index

#insert è come append ma scegli la posizione
#costo O(n)
a.insert(1,"ciao")

#copy vedi aliasing è come se fosse deep copy
#diverso da slicing
b=a.copy()

#sort è diverso da sorted
a.sort(reverse=True)
#key del sort,usa condizione per effettuare il sorting
def lunghezza(e):
  return len(e)

cars = ['Ford', 'Mitsubishi', 'BMW', 'VW']
cars.sort(key=lunghezza)
print(cars)

#reverse ritorna al contrario
a.reverse()
#index ritorna la posizione
a=[2,3,4,5]
a.index(3) #ritorna 1
#differenza tra metodi e funzioni di python
a=[7,9,2,1]
print(a) #in questo caso, la differenza tra .sort e func sorted è:
#a.sort() #la .sort è un metodo che ordina la lista senza aver bisogno di un return
#a.sort modifica la variabile, E FUNZIONA SOLO CON LE LISTE

#mentre la func sorted ha bisogno di essere richiamata e funziona come le altre funzioni 
sorted(a)
print(a)

#Le tuple, sono come le liste ma non sono modificabili
#puoi fare count e index
#count: ti dice quante volte appare quel dato
a=(1,1,2,3,4)
print(a.count(1))  #ritorna 2
#index è come nelle liste
#si possono mixare le liste con le tuple?
#si può fare list.extend(tupla)
#non si può fare tupla.extend pk no modificab
#per aggiungere un elemento alla tupla 
#a+=(1,2,3) crea una nuova tupla
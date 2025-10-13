##### Dettagli ulteriori sulle interfacce
###### nell'interfaccia vanno pure le costanti
non serve specificare public static final perché è scontato che si stia parlando di costanti
```java
public interface DoIt {
   String const="ciao";
   void doSomething(int i, double x);
   int doSomethingElse(String s);
}
```

###### Significato di Signature
per signature si intende la firma di un metodo che si trova in una classe o interfaccia
e indica:
- il nome del metodo
- l'ordine e il tipo dei parametri del metodo
viene usato tipo per l'overloading per differenziare i metodi

>[!quote] le interfacce servono per fornire un vocabolario unificante o un contratto che le classi devono rispettare. Fornendo delle sorta di api che qualcuno potrà utilizzare senza andare a leggere i dettagli implementativi

##### relatable
È un concetto che indica la possibilità di comparare due oggetti tra loro secondo delle caratteristiche
##### concetto di dato derivato
Quando tu fai un metodo lo ritorni facendo una formula di altri dati effettivi
```java
 public int getArea() {
        return width * height;
    }
```
#### Problema delle interfacce
>[!bug] se ho una interfaccia implementata da 1000 classi e la aggiorno, il problema è che poi devo implementare quel metodo in ogni classe:

- soluzione 1, estendo l'interfaccia cosi non rompo il cazzo agli altri
- soluzione 2 ma di merda, creo un metodo di default che vale per tutte le classi che implementano l'interfaccia ma che non sono costretti ad utilizzare
```java

public interface DoIt {

   void doSomething(int i, double x);
   int doSomethingElse(String s);
   default boolean didItWork(int i, double x, String s) {
       // il corpo del metodo
   }
   
}
```
>[!bug]- perché fa cagare?
>perché toglie tutto il concetto di generalizzazione delle interfacce e dovresti fare un override del metodo, è una non soluzione

>[!info] una serie di metodi della classe Object è che sono ereditati da tutti

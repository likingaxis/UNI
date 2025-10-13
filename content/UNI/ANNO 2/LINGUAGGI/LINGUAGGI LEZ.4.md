### Carrellata di caratteristiche di Java
>[!question]- Funzione vs Metodo
>La funzione è indipendente invece i metodi sono dipendenti dall'oggetto che usiamo
- Stringa fa parte di default del linguaggio Java
- La maggior parte delle volte non importiamo nessun pacchetto di classi perché sono già intrinsecamente nelle classi di base di Java
- il print si scrive cosi strano perché stiamo invocando un metodo di un oggetto statico chiamato `System.out`
>[!example]- esempio di compilazione e esecuzione di un file
>Javac file.java-> compilo (faccio riferimento a un file)
>Java file-> eseguo (non serve che faccia riferimento a un file in una dir) dico Java file senza estensione perché la classe è già disponibile nel classPath(con tutti i bytecode, posso fare -cp per modificare il classPath) nella macchina virtuale di Java
>Il classPath è presente nella cartella dove invochiamo Java(working directory)
## ELEMENTI FONDAMENTALI DELLA PROGRAMMAZIONE A OGGETTI
L'oggetto ha uno stato che può variare nel tempo dell'esecuzione del codice
può variare a seconda dei metodi dell'oggetto e degli attributi dell'oggetto

#### Codice con bicicletta
```java
class Bicycle {

    int cadence = 0;
    int speed = 0;
    int gear = 1;

    void changeCadence(int newValue) {
         cadence = newValue;
    }

    void changeGear(int newValue) {
         gear = newValue;
    }

    void speedUp(int increment) {
         speed = speed + increment;   
    }

    void applyBrakes(int decrement) {
         speed = speed - decrement;
    }

    void printStates() {
         System.out.println("cadence:" +
             cadence + " speed:" + 
             speed + " gear:" + gear);
    }
}

  
class BicycleDemo {
    public static void main(String[] args) {

        // Create two different 
        // Bicycle objects
        Bicycle bike1 = new Bicycle();
        Bicycle bike2 = new Bicycle();

        // Invoke methods on 
        // those objects
        bike1.changeCadence(50);
        bike1.speedUp(10);
        bike1.changeGear(2);
        bike1.printStates();

        bike2.changeCadence(50);
        bike2.speedUp(10);
        bike2.changeGear(2);
        bike2.changeCadence(40);
        bike2.speedUp(10);
        bike2.changeGear(3);
        bike2.printStates();
    }
}
```


>[!bug] Con la classe abbiamo creato lo stampino di una bicicletta quindi potrei crearne n oggetti

>[!info]- Creazione di un oggetto in java
>Creiamo uno spazio in memoria dinamico(hip) e salviamo il suo riferimento con un "puntatore", questo puntatore sarà ad esempio `nomeclasse nomeoggetto` e il suo riferimento = a
>`new nomeclasse()`

>[!question]- Se faccio una uguaglianza tra due puntatori ad oggetti? `nomeoggetto1=nomeoggetto2`
> avrò lo stesso puntamento a memoria quindi entrambe puntano allo stesso oggetto

>[!question] che succede all'oggetto a cui puntavo prima??
Su c++ avevo costruttori e distruttori ma in Java non ce ne frega nulla perchè è magico✨

>[!question]- a cosa serve `@override`?
>`@override` serve a sovrascrivere un metodo che già abbiamo nominato in precedenza con un altro metodo specifico per la singola classe
#### Concetto di ereditarietà
Posso creare delle sotto classi che riprendono TUTTE le caratteristiche della classe madre(o superclasse) ma aggiungono dei dettagli 
![[Pasted image 20241026111433.png|500]]

 
>[!bug] Una classe non può ereditare da più classi come in c++

>[!bug] In Java le variabili bisogna sempre dichiararle prima con lettere e poi numeri

> [!example]- esempio di codice con sottoclassi
> ```java
> 
> class Schedavideo{
> 
>     int ventole=0;
> 
>     int vram=0;
> 
>     int sborra;
> 
>     String colore="bianco";
> 
>     void stampadati (){
> 
>         System.out.println(ventole+" "+vram+" "+sborra+" "+colore+" ");   
> 
>     }
> 
> }
> 
>   
>   
> 
> class NVIDIA extends Schedavideo{
> 
>     double DLSS=1.0;
> 
>     @Override
> 
>     void stampadati (){
> 
>         System.out.println(DLSS);
> 
> }
> 
> }
> 
>   
> 
> class AMD extends Schedavideo{
> 
>     double FSR=1.5;
> 
>     @Override
> 
>     void stampadati (){
> 
>         System.out.println(FSR);
> 
> }
> 
> }
> 
>   
> 
> class test2{
> 
>     public static void main(String[] args){
> 
>         Schedavideo RTX3060= new Schedavideo();  
> 
>         RTX3060.ventole=5;
> 
>         RTX3060.vram=7;
> 
>         RTX3060.sborra=0;
> 
>         RTX3060.colore="rosso";
> 
>         NVIDIA TI3070=new NVIDIA();
> 
>         TI3070.DLSS=1.6;
> 
> 
>         AMD XT6700=new AMD();
> 
>         XT6700.FSR=2.1;
>         XT6700.ventole=3;
> 
> 
>         RTX3060.stampadati();
> 
>         TI3070.stampadati();
> 
>         XT6700.stampadati();
> 
>     }
> 
> }
> ```

>[!info]- piccola spiegazione sugli override
>quando vogliamo sovrascrivere un metodo di una superclasse usiamo override sopra al metodo 
>della sottoclasse
>```java
>   @Override
>
>   void stampadati (){
>
>        System.out.println(DLSS);
>
>}
>```
>

### Cosa è una interfaccia
>[!info]- Definizione
>Le interfacce in Java servono principalmente per definire un insieme di metodi _generici_ che devono essere implementati da varie classi.
>Le interfacce si possono definire come dei contratti che vanno rispettati dalle varie classi che lo firmano e che devono OBBLIGATORIAMENTE applicare quei metodi  definiti
> 
> ```Java
> interface Animale {
>     void verso();
> }
> 
> class Cane implements Animale {
>     @Override
>     public void verso() {
>         System.out.println("Bau bau");
>     }
> }
> 
> class Gatto implements Animale {
>     @Override
>     public void verso() {
>         System.out.println("Miao miao");
>     }
> }
> 
> ```

✖️ In java non esiste l'ereditarietà multipla, una classe figlia non può avere due genitori
>[!tip]- utilizzo di interfaccia per creare una sorta di ereditarietà multipla dei metodi
>Infatti in java posso far accettare più contratti ad una classe
>
>
> ```java
> interface TERRA
> { 
> void GUIDA(); 
> } 
> interface ACQUA{ 
> void NAVIGA();
> } 
> class AUTOMOBILE implements TERRA{  
> int velocità= 5; @Override  
> public void GUIDA()
> { System.out.println(velocità); 
> }  
> } 
> class BARCA implements ACQUA{ int velocità= 60; @Override  
> public void NAVIGA(){ System.out.println(velocità); }  
> } class HOVERCRAFT implements TERRA,ACQUA{ int velocità=100; @Override  
> public void GUIDA(){ System.out.println(velocità); } @Override  
> public void NAVIGA(){ System.out.println(velocità); } } class interfacce{ public static void main(String[] args) { AUTOMOBILE lamborghini=new AUTOMOBILE(); lamborghini.velocità=400; BARCA yatch=new BARCA(); yatch.velocità=50; HOVERCRAFT aereo= new HOVERCRAFT(); aereo.velocità=700;  
> lamborghini.GUIDA(); yatch.NAVIGA(); aereo.NAVIGA(); aereo.GUIDA(); } }
> ```


![[Pasted image 20241026151525.png|600]]


>[!question]- perchè non creo dei metodi e li uso e basta senza fare le interfacce?
>È una domanda molto comune! Le interfacce in Java possono sembrare ridondanti all'inizio,
> specialmente se pensi: "_Perché non posso semplicemente definire dei metodi in una classe e 
> chiamarli quando ne ho bisogno?_". Tuttavia, le interfacce servono a risolvere alcuni problemi di 
> **organizzazione del codice** e **manutenzione** che diventano evidenti quando il progetto 
> cresce in complessità.

>[!info]- cosa significa interoperabilità
>indica in java la sua capacità di essere flessibile e la possibilità di integrare più linguaggi di programmazione o servizi esterni, Java non è un ecosistema chiuso
>Anche per i contratti abbiamo un discorso di interoperabilità sempre per un discorso di flessibilità 

>[!info]- clash delle implementazioni
>Questo termine si dice se c'è un conflitto di interessi tra le varie implementazioni come metodi classi ecc...
## PACKAGE
- Un software al giorno d'oggi contiene migliaia di classi ecc
- I package sono un modo per separare in cassetti le classi che voglio creare
- Posso organizzare i package In più cartelle come se fossero un file system
>[!info]- un package è un modo per mettere varie classi in una sorta di file system con la possibilità di implementarle ogni volta che richiamiamo questo package in fase di codice
>import nomepackage.test.progetto il .  serve per muoversi all'interno delle cartelle del package come se fossero degli /
>![[Pasted image 20241027112725.png|300]]
>una volta importato il package possiamo creare oggetti di quella classe o fare delle sue sottoclassi
>- per metterlo si fa import nomepackage
>- per crearlo dobbiamo fare un file che poi dovrà essere compilato 

>[!bug]- I package non hanno nessun rapporto funzionale tra di loro anche se sono uno dentro l'altro
###### Esempio creazione package

```java

package animali;  // creo la mia cartella

  

public class Cane {  // creo la mia classe

    public void abbaia() {

        System.out.println("Bau Bau!");

    }

}

```

Utilizzo la stessa cartella ma utilizzo una variabile diversa
```java

package animali;  // dico che la classe dovrà andare dentro la cartella

  

public class Gatto {  // creo la mia classe

    public void miagola() {

        System.out.println("Miao!");

    }

}

```
###### Esempio utilizzo package

```java

import animali.Cane;  // utilizzo .Cane per specificare un file

  

public class Main {

    public static void main(String[] args) {

        Cane mioCane = new Cane();

        mioCane.abbaia();  // Stampa: Bau Bau!

    }

}

```


```java

import animali.Gatto;  // utilizzo .Gatto specificare un file

  

public class Main {

    public static void main(String[] args) {

        Gatto mioGatto = new Gatto();

        mioGatto.miagola();  // Stampa: Miao!

    }

}

```

SE VOGLIO UTILIZZARE TUTTA LA CARTELLA USO  `.*`
```java
import animali.*;  // utilizzo .* per utilizzare tutta la cartella
```
### CARRELLATA DI COSE DA RICORDARE
 ## LESSON: Language Basics
 
>[!question]- DOMANDA D'ESAME:Che tipologie di variabili esistono in Java 
>In senso che ruoli può avere
>
>
>1. Le variabili globali
>2. Variabili che descrivono lo stato di un oggetto: campi(fields o attributi) campi statici e campi non statici 
>3. Variabili locali interne a un metodo temporanee
>4. Variabili dei parametri
>variabili primitive != variabili in generale

>[!question]- Differenza tra parametri e argomenti
>- i parametri sono quei dati che passiamo a un metodo o funzione 
>	`void metodo(int numero, String gino)`
>- gli argomenti sono quei dati che passiamo quando chiamiamo la funzione
>	 `metodo(5,"ciao")`

>[!bug]- Campo(o attributo) statico e non statico
>- Non statico, ogni oggetto ha i suoi attributi della classe che al massimo se non vengono messi rimangono di default
>- Statica, ogni istanza della classe(oggetto) avrà questo attributo e il suo valore in comune, non è definibile una costante perchè nel corso del codice posso modificare il valore del seguente campo e questa cosa varrà per ogni sua istanza, esempio di una classe con uno standard europeo, ogni oggetto potrà salvare questo standard e se cambia ogni oggetto avrà lo standard cambiato. per usare invece le costanti faremo static final
>- Staticità ha a che fare con la posizione in memoria di quel campo
>- Heap indica una prozione di memoria dinamica, qua in questa porzione dinamica avremo ad esempio i new oggetti

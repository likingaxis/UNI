Prima di iniziare con i Generics si può precisare che è possibile sfruttare oggetti ovunque vogliamo
- in classi
- metodi
- interfacce
ecc...
**Tutte le classi comprese quelle che si creano sono figlie di Object**
```java
public class Box {
    private Object object;

    public void set(Object object) { 
	    this.object = object; 
    }
    public Object get() { 
	    return object; 
    }
}
```
Visto che usiamo un Object la dentro possiamo metterci quello che ci pare

Generics

//Se noi facciamo una arraylist, che oggetti mettiamo dentro? che cazzo ne so?
io voglio vincolarla ad avere determinati valori//
>[!bug] se uso Object potrei incorrere in problemi di correlazione tra oggetti, cioè magari per sbaglio, uso Stringhe e poi subito dopo altri tipi di oggetti

```java

public class Box {
    private Object object;

    public void set(Object object) { 
	    this.object = object; 
    }
    public Object get() { 
	    return object; 
    }
}

Box box = new Box();
box.setContent("Hello");
String value = (String) box.get(); // Serve per forza il cast
System.out.println(value);
```
Serve per forza il cast perché una Stringa non può accogliere un oggetto qualsiasi
>[!done] uso Generics per risolvere il problema lasciando spazio all'utilizzatore della classe nel definire una volta per tutte quella classe cosa prevede


T è un **placeholder** viene deciso **quando istanzi la classe**
```java
public class Box<T> {
    private T content;

    public void setContent(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}

Box<String> box = new Box<>();
box.setContent("Hello");
String value = box.getContent(); // Nessun cast necessario
System.out.println(value);

```

>[!info]- In C++ 
>`List<E>` `List<Person>` indica che al posto della cosa con E lui deve sostituire tutte le volte con 
>Person

##### USO DI GENERICS MULTIPLE E IN INTERFACCE
come si può vedere dal codice qua sotto ho usato molteplici generics in interfacce, vanno in base all'ordine

```java
public interface Pair<K, V> {
    public K getKey();
    public V getValue();
}

public class OrderedPair<K, V> implements Pair<K, V> {

    private K key;
    private V value;

    public OrderedPair(K key, V value) {
	this.key = key;
	this.value = value;
    }

    public K getKey()	{ return key; }
    public V getValue() { return value; }
}

nel main avremo:

Pair<String, Integer> p1 = new OrderedPair<String, Integer>("Even", 8);
Pair<String, String>  p2 = new OrderedPair<String, String>("hello", "world");
```

#### USO DEI RAW(Sconsigliato e deprecated)

- Qui si parla di codice Legacy ovvero vecchio prima di un aggiornamento
prima di Java 5 non esistevano le generics, quindi dovevo fare in una ipotetica classe che implementa le generics la cosa del casting
Anche se una nuova classe implementa i generics
```java
public class Box <T> {
    private T content;

    public void setContent(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}

```
magari ho un vecchio main o da qualche altra parte che non lo fa
funziona lo stesso senza usare il diamond in box ma devo mettere poi il casting
```java
Box box = new Box(); // Uso senza specificare il tipo
box.setContent("Hello");
String value = (String) box.getContent(); // Serve il cast
System.out.println(value);

```

#### Si possono dichiarare anche solo i metodi in modo generic senza tutta la classe, si usano soprattutto con i metodi statici
```java
public class Util {
    **public static <K, V> boolean compare(Pair<K, V> p1, Pair<K, V> p2)** {
        return p1.getKey().equals(p2.getKey()) &&
               p1.getValue().equals(p2.getValue());
    }
}
```

### Posso usare generics in questo modo <U **extends Number**>
per fare in modo che sicuramente estendono la classe number in questo esempio così sono sicuro che uso un numero

#### Extends con la `&`
Facciamo finta che mi creo una classe A una interfaccia B e un'altra C

class D <T extends A & B & C>
{ /* ... */ }
- devono rispettare una gerarchia e la classe può essere solo una se viene messa
	- deve oltretutto essere messa per prima rispetto alle interfacce
- extends indica sia implement che extend in questo caso

##### skip fino a wildcards
```java
public void printBoxContent(Box<?> box) {
    Object content = box.getContent(); // Tipo sconosciuto
    System.out.println(content);
}
```

 Si usa il `?` per indicare una cosa ancora piu generica, quando invece con il placeholder T una volta che scrivevo String per quell'oggetto vale come String ogni volta, ora posso cambiare le cose a mio piacimento anche dopo aver creato l'oggetto e averlo basato su una String

Con le wildcard potrei ad esempio anche creare delle extends ma che ogni volta variano

#### Type Erasure
Riprende i concetti di java 5 e codice Legacy
È il meccanismo che rimuove le informazioni sui tipi generici a runtime per garantire la compatibilità con il codice legacy e ridurre la complessità del bytecode
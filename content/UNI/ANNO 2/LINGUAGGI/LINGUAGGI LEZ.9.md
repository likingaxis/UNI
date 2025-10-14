### Classi Locali
Le classi locali sono delle classi definite all'interno di un blocco (ad esempio un metodo, ciclo, istruzione).
Posso dichiararle ovunque nel codice, purché all'interno di un blocco delimitato da `{}`.

```java
public void exampleMethod() {
    class LocalClass {
        void printMessage() {
            System.out.println("Sono una classe locale!");
        }
    }
    
    LocalClass local = new LocalClass();
    local.printMessage();
}
```
In questo caso il metodo `exampleMethod` crea una classe.


#### Accesso ai membri esterni alle classi locali
Una classe locale può accedere ai membri esterni ad essa in queste modalità
- **CLASSE LOCALE DEFINITA IN UN METODO `STATICO`**
	- può accedere solo a **membri statici**
```java
public class StaticExample { // Classe esterna
    static String staticMessage = "Ciao statico!"; // Membro statico
    String instanceMessage = "Ciao istanza!"; // Membro di istanza (non 
                                              //accessibile direttamente)
	
    public static void staticMethod() { // Metodo statico
        // Classe locale definita dentro un contesto statico
        class LocalClass {
            void printMessage() {
                System.out.println(staticMessage); // OK, il membro è statico
                System.out.println(instanceMessage); // ERRORE: non può accedere a                                                                 membri non statici
            }
        }
    }
}
```

- **CLASSE LOCALE DEFINITA IN UN METODO `NON STATICO`**
	- può accedere a qualsiasi membro
```java
public class NonStaticExample { // Classe esterna
    static String staticMessage = "Ciao statico!"; // Membro statico
    String instanceMessage = "Ciao istanza!"; // Membro di istanza 
	
    public void nonStaticMethod() { // Metodo NON statico
        // Classe locale definita dentro un contesto non statico
        class LocalClass {
            void printMessage() {
                System.out.println(staticMessage); // OK
                System.out.println(instanceMessage); // OK 
	        }
	    }
    }
}
```


#### Accesso a variabili locali
Le classi locali possono accedere alle variabili locali del metodo in cui sono inserite solo se sono definite `final`, senza non va bene.
```java
public class LocalVariableExample {
	public void validateNumber() {
	    final int numberLength = 10; // VA BENE
	    class PhoneNumber {
	        void validate(String number) {
	            System.out.println("Validating number of length " + numberLength);
	        }
	    }
	}
}
```


#### Shadowing nelle Classi Locali
Nel caso in cui ci fossero due variabili o metodi identici, uno fuori dal metodo in cui è definita la classe locale e uno all'interno della classe locale, quest'ultimo va a **nascondere** (shadow) il primo.
```java
public class ShadowingExample {
	String message = "Classe esterna";
	public void shadowExample() {
	    class LocalClass {
	        String message = "Classe locale";
	        void printMessage() {
	            System.out.println(message); // Stampa "Classe locale"
	        }
	    }
	}
}
```


#### Cosa NON posso nelle classi locali
- NON POSSO definire **membri statici** (es. `static String message)
	- tuttavia se sono variabili posso farlo (es. `static final int numero = 10`)

- NON POSSO implementare un'**interfaccia** 
```java
public class NotInterface {
	public void wrongMetodo() {
		class LocalClass implements Interface { // NON POSSO FARLO
			// COSE
		}
	}
}
```

- NON POSSO avere inizializzatori statici (es. metodo statico)
```java
public class MetodoStaticoInClasseLocale {
	public void pisello() {
		class LocalClass { 
			public static void metodoStatico() { // NON POSSO FARLO
				// COSE
			}
		}
	}
}
```

- Possono accedere solo ai membri della classe esterna e ai membri locali finali o effettivamente finali.
	- IN PRATICA credo che le classi locali non possano accedere ai membri di altre classi locali.


#### Anonymous Classes
Le anonymous classes sono molto utili quando vuoi creare una classe "al volo" dentro (per esempio) un main.
Nel senso, se devo creare una classe per fare un qualcosa di molto semplice, piuttosto che crearla esternamente posso scriverla direttamente nel main.

Utilità delle classi anonime
- implementare velocemente un'interfaccia.
- estendere una classe esistente e personalizzarne il comportamento.
- Quando vuoi evitare di creare una classe separata per qualcosa di semplice (scritto prima)
###### SINTASSI BASE
```java
AnonymousClass classe = new AnonymousClass() { // il nome lo scelgo sul momento
    // Corpo della classe anonima: metodi e campi
};
```

###### ESEMPIO SEMPLICE: implementazione di un interfaccia
```java
interface Saluto {
    void sayHello();
}

public class AnonymousExample {
    public static void main(String[] args) {
        // Creazione di una classe anonima che implementa Saluto
        Saluto ciao = new Saluto() { // il nome è lo stesso dell'interfaccia
            @Override
            public void sayHello() {
                System.out.println("Ciao, classe anonima!");
            }
        };
		
        ciao.sayHello(); // Stampa "Ciao, classe anonima!"
    }
}
```
Scrivere 
```java
Saluto ciao = new Saluto() {
	// COSE
};
```
è come scrivere
```java
class ciao implements Saluto {
	// COSE
}
```


###### ESEMPIO SEMPLICE: estensione di una classe
L'idea è scrivere questo ma `Dog` deve essere una classe anonima.
```java
class Animal {
    void speak() {
        System.out.println("Sono un animale.");
    }
}

class Dog extends Animal {
	@Override
    void speak() {
        System.out.println("Bau! Sono un cane.");
        }
}
```

**SOLUZIONE**
```java
class Animal {
    void speak() {
        System.out.println("Sono un animale.");
    }
}

public class AnonymousExample {
    public static void main(String[] args) {
        // Creazione di una classe anonima che estende Animal
        Animal dog = new Animal() {
            @Override
            void speak() {
                System.out.println("Bau! Sono un cane.");
            }
        };
		
        dog.speak(); // Stampa "Bau! Sono un cane."
    }
}
```


#### Accesso a variabili locali
Le **anonymous classes** possono accedere a:
- **Membri statici** e **di istanza** della classe esterna.
- **Variabili locali** del metodo, ma solo se sono dichiarate `final` o **effettivamente finali**.


#### Restrizioni delle classi anonime
1. **Non puoi dichiarare un costruttore**, ma puoi usare un **inizializzatore di istanza**.
2. Non possono contenere membri statici, a meno che siano costanti (`static final`).
3. Possono avere campi e metodi aggiuntivi, ma questi non sono visibili se usi un'interfaccia o una classe madre come riferimento (questo perché, ad esempio, `Dog` è visto come `Animal`).
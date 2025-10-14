### DEFINIRE CLASSI ASTRATTE DI METODI ASTRATTI
>[!question]- perché fare abstract class e non normali?
>un metodo abstract indica un metodo incompleto che ipoteticamente è previsto nell'interfaccia

se fai un metodo abstract dichiari la classe abstract
- **Sottoclasse concreta**: È obbligata a implementare tutti i metodi astratti definiti sia nella classe base sia di una ipotetica sottoclasse astratta.
- Tutte le cose statiche su una classe abstract funzionano come in una normale classe
```Java
public abstract class GraphicObject {
   // declare fields
   // declare nonabstract methods
   abstract void draw();
}
```

```Java
public class Circle extends GraphicObject { 
	@Override void draw() 
		{ 
		System.out.println("Drawing a circle"); 
		} 
}
```
### Le eccezioni
>[!tip] in c non esiste un metodo per gestire gli errori bensi verranno ritornati valori negativi che appartengono a qualcosa, quindi -1 leggi sul manuale -3 leggi ecc...

Le chiamiamo eccezioni perché indicano un evento che avviene al di fuori del solito flusso di istruzioni del programma

![[Pasted image 20241209142246.png|300]]
- quando chiamiamo un metodo avviamo un call stack
	- rappresenta le varie chiamate scendendo sempre più a basso livello
quindi effettuo delle chiamate così main->m1->m2->m3 
poi per le restituzioni di controllo a chi mi ha chiamate m3->m2->m1->main
- immaginiamo che durante una chiamata succede qualcosa🤚🛑
tipo $m3$ ha un errore, potrebbe risolverlo oppure potrebbe farla risalire al chiamante
come se fosse una bolla, quello che vedremo e impacchettare la bolla e portarla su 
```Java
public class ExceptionExample {
    public static void main(String[] args) {
        method1(); // Chiamata al metodo 1
    }

    static void method1() {
        try {
            method2(); // Chiamata al metodo 2
        } catch (ArithmeticException e) {
            System.out.println("Gestito in method1: " + e.getMessage());
        }
    }

    static void method2() {
        method3(); // Chiamata al metodo 3
    }

    static void method3() {
        int result = 10 / 0; // Questo genera un'eccezione
    }
}
```

>[!question]- Quando avviene una exception
>il sistema runtime cerca un metodo all'interno del call stack per gestire questa eccezione
>- questo metodo viene detto gestore delle eccezioni
>- viene prima ricercato nel metodo che la causa e poi a ritroso sale ai vari chiamanti
>- quando viene trovato questo gestore viene passato l'oggetto eccezione e verrà gestito
>le eccezioni SONO OGGETTI!!!!
>se non viene trovato un gestore viene terminato il programma

##### Gercarchia delle eccezioni
Ad esempio ho le `I/O exception` che gestiscono gli errori di input e output ma in modo generico
potrebbe esserci invece una sotto classe `FileNotFoundException` che è un sotto errore della I/O,
- posso quindi scegliere se gestire eccezioni generiche oppure cose meno generiche
##### TRE TIPI DI EXCEPTION
- **checked exception**, Vengono controllate in compile time, e queste eccezioni possono essere gestite proprio nel codice con
	- blocchi try catch
	- throw
- **unchecked exception** si dividono in:
	- **runtime exception** tipo: nullpointer exception oppure segmentation fault
		- per gestirle non serve usare try catch o throw
		- vengono lanciate direttamente da metodi appartenenti alle classi predefinite.
	- **error** non sono eccezioni bensì sono errori di basso livello terribile e rarissimo
		- tipo errori hardware tipo dove ti finisce la memoria

#### Vediamo ora i metodi per gestire le eccezioni
##### `Try-Catch` 
###### Con Checked Exception (*IOException*)
Proviamo a gestire un file che non può essere aperto.
```java
import java.io.*;

public class CheckedExceptionExample {
    public static void main(String[] args) {
        try {
            // Prova ad aprire un file
            FileReader file = new FileReader("nonexistent.txt");
        } catch (IOException e) {
            // Gestione dell'eccezione
            System.out.println("Errore: Il file non esiste.");
        }
    }
}

// OUTPUT
// Errore: Il file non esiste.
```
Io qui provo a eseguire il codice con il `try`, qualora non dovesse andare a buon fine utilizzo il `catch` per gestire quell'eccezione.

###### Con Runtime Exception (*IndexOutOfBoundsException*).
Proviamo ad accedere ad un indice che non esiste in una lista.
```java
import java.util.ArrayList;
import java.util.List;

public class RuntimeExceptionExample {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        numbers.add(1); // Lista con un solo elemento
		
        try {
            // Prova ad accedere a un indice non valido (es. indice 5)
            System.out.println(numbers.get(5));
        } catch (IndexOutOfBoundsException e) {
            System.out.println("Errore: Indice fuori dai limiti.");
        }
    }
}

// OUTPUT
// Errore: Indice fuori dai limiti.
```

###### `Finally`
Il blocco `finally` viene eseguito indipendentemente dal verificarsi di un'eccezione
- il finally serve per rilasciare le risorse e chiudere tutto(lo vedremo dopo)
```java
public class FinallyExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // Questo genera un'eccezione
        } catch (ArithmeticException e) {
            System.out.println("Errore: Divisione per zero.");
        } finally {
            System.out.println("Blocco finally eseguito sempre.");
        }
    }
}

// OUTPUT
/* Errore: Divisione per zero.
   Blocco finally eseguito sempre.
*/
```

###### `Try-with-resources`
Il `try-with-resources` è una variante del blocco `try` che garantisce automaticamente la chiusura delle risorse dopo che sono state usate, senza bisogno di farlo manualmente nel blocco `finally`.
Generalmente dopo aver aperto una risorsa, nel finally scrivo
```java
finally {
	RISORSA.close();
}
```
così lo chiudo.
Con il `try-with-resources` posso chiuderla automaticamente.
```java
public void writeList() throws IOException {
    try (FileWriter f = new FileWriter("OutFile.txt");
         PrintWriter out = new PrintWriter(f)) {
        for (int i = 0; i < SIZE; i++) {
            out.println("Value at: " + i + " = " + list.get(i));
        }
    }
}
```

>[!tip] Boh non lo so prendilo molto alla larga



##### `Throws`
Quando si verifica un'eccezione è sempre meglio non gestirla direttamente nel metodo (con il `try-catch`) ma lasciare che sia il metodo chiamante a gestirla (letteralmente quello che abbiamo visto prima nel *call stack*).

Per farlo utilizziamo la clausola `throws` nel metodo "chiamato", andando a specificare il tipo (uno o più) di eccezioni che potrebbero verificarsi.
###### Esempio
*METODO CHIAMATO*
```java
public void writeFile() throws IOException {
    PrintWriter out = new PrintWriter(new FileWriter("output.txt"));
    out.println("Ciao!");
    out.close();
}
```
Il metodo dice al chiamante "senti a me mi importa 'na ricca sega, io faccio il mio lavoro e se genero un'eccezione gestiscitela tu (down)".
Letteralmente il metodo chiamato ***LANCIA***  la sua eccezione(vedremo meglio come).

*METODO CHIAMANTE*
```java
public static void main(String[] args) {
    try {
        new MyClass().writeFile();
    } catch (IOException e) {
        System.out.println("Errore gestito in main.");
    }
}
```
Qui il metodo prova a eseguire `writeFile`, quando questo avrà finito, il chiamante controlla se ha lanciato un'eccezione e nel caso la gestisce personalmente.


>[!tip]- Esempio con più eccezioni
>Mettiamo caso che il chiamato possa generare più tipologie di eccezioni
>```java
>public void piuEccezioni() throws IOException, IndexOutOfBoundsException {
>    // Potenziale IOException
>    PrintWriter out = new PrintWriter(new FileWriter("output.txt"));
>
>    // Potenziale IndexOutOfBoundsException
>    int[] numbers = {1, 2, 3};
>    System.out.println(numbers[5]); // Accesso non valido
>
>    out.close();
}
>```
>
>Di conseguenza il chiamante deve essere in grado di "catturarle" tutte
>```java
>public static void main(String[] args) {
>    try {
>        new MyClass().piuEccezioni();
>    } catch (IOException e) {
>        System.out.println("Errore di I/O gestito.");
>    } catch (IndexOutOfBoundsException e) {
>        System.out.println("Errore di accesso alla lista gestito.");
>    }
}
>```


#### Tutto bello, ma se ci sono eccezioni che vengono generate in Runtime da Java come faccio? Utilizzo il `throw`
In pratica io uso `throw` per creare la mia eccezione e con il `throws` specifico quale eccezione sto per lanciare.

##### SINTASSI
```java
throw new NomeEccezione("Messaggio di errore");
```
- **`NomeEccezione`**: Deve essere una classe che eredita da `Throwable`.
	- se io genero un'eccezione che non è standard, posso creare una sottoclasse di `exception` e inserisco tutte le mie "nuove" eccezioni
- **`Messaggio di errore`**: Una stringa opzionale che descrive l'errore

##### ESEMPIO
*UTILIZZO `THROW` MA NON `THROWS`* quando mi aspetto un'*unchecked excpetion*
```java
public double calcolaRadiceQuadrata(double numero) {
    if (numero < 0) {
        throw new IllegalArgumentException("È un numero negativo!!");
    }
    return Math.sqrt(numero);
}
```
`IllegalArgumentException` è una ***Unchecked exception*** e quindi posso non scrivere `throws`.


*UTILIZZO `THROW` E `THROWS`* quando mi aspetto una *checked exception*
```java
public void scriviSuFile(String testo) throws IOException {
        // Lancia un'eccezione checked
        throw new IOException("Errore di scrittura su file");
    }
```


*UTILIZZO `THROW` E `THROWS`* quando mi aspetto un'eccezione "personalizzata", ossia inserita da me in una sottoclasse di `exception`, <u>INDIPENDENTEMENTE SE SIA CHECKED O UNCHECKED</u>.
```java
public void calcolaRadice(double numero) throws NumeroNegativoException {
    if (numero < 0) {
        throw new NumeroNegativoException("Numero negativo: " + numero);
    }
    return Math.sqrt(numero);
}
```
Qui `NumeroNegativoException` è una mia eccezione personalizzata (non scrivo il codice della sottoclasse ma fai finta).

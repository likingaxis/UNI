piccola nota: ringrazio Samuele per aver carryato l'intera lezione visto

## Espressioni

Un’espressione è una combinazione di **variabili**, **operatori** (come `+`, `-`, `/`) e, talvolta, **chiamate a metodi**, che insieme producono un valore. Ad esempio, `1 + 2` è un’espressione che restituisce `3`, e anche `System.out.println("Ciao")` è un’espressione perché esegue un’azione e ha un valore di ritorno.

Ovviamente il tipo di valore ritornato da un'espressione dipende dagli elementi usati all'interno di essa, ad esempio:
- `int numero = 10;` ritorna un `int`
- `String parola = "ciao"`; ritorna una `String`
#### Precedenza degli operatori
Come visto nella tabella degli operatori nella lezione precedente, ogni operatore ha una “precedenza” (quelle matematica) che ovviamente Java rispetta.
- Esempio: In `x + y / 100`, Java eseguirà prima `y / 100`, poi sommerà il risultato a `x` perché la divisione ha precedenza sull’addizione.

Per "ovviare" e per eliminare le ambiguità si usano le `()`.
## Statement
Lo Statement è un'istruzione completa, e al suo interno contiene espressioni.
ci sono 4 tipi di Statement:
- di assegnazione `aValue = 8933.234;
- di dichiarazione `double aValue = 8933.234;`
- quando si usa ++ o -- `aValue++;`
- invocazione di metodi `System.out.println("Hello World!");`
- espressioni sulla creazione di oggetti `Bicycle myBike = new Bicycle();`
E poi soprattutto ci sono i:
#### Control Flow Statements
In Java (e in molti altri linguaggi di programmazione), un **control flow Statement** è un’istruzione che gestisce l’ordine in cui vengono eseguiti i blocchi di codice, determinando **il flusso di esecuzione del programma**.
Prima di passare a spiegare i vari tipi di Statements spiegherei cosa sono i blocchi:
###### I blocchi
una serie di Statements messi insieme e raggruppati dalle parentesi `{ }`
```java
class BlockDemo {
    public static void main(String[] args) {
        boolean condition = true; // Dichiarazione e inizializzazione di 
                                  // 'condition'
        
        if (condition) { // Inizio del blocco 1
            System.out.println("Condition is true."); // Stampa se 'condition' è 
                                                      // true
        } // Fine del blocco 1
        
        else { // Inizio del blocco 2
            System.out.println("Condition is false."); // Stampa se 'condition' è 
                                                       // false
        } // Fine del blocco 2
    }
}
```
###### Tipi di control flow Statements
1. **Condizionali (`if`, `if-else`, `switch`)**
- **`if` e `if-else`**: Eseguono un blocco di codice solo se una condizione è vera (`true`).
```java
int x = 10;

if (x > 5) {
    System.out.println("x è maggiore di 5");
} 
else {
    System.out.println("x è minore o uguale a 5");
}
```

- **`switch`**: Seleziona uno tra diversi blocchi di codice in base al valore di una variabile.
```java
int giorno = 1;

switch (giorno) {
    case 1:
        System.out.println("Lunedì");
        break;
    case 2:
        System.out.println("Martedì");
        break;
    default: // opzionale, se non lo metto non restituisce nulla e va bene
        System.out.println("Altro giorno");
}
```
>[!warning] SWITCH ACCETTA `String` MA NON ACCETTA `float`, `double`, `boolean`.

2. **Cicli (`for`, `while`, `do-while`)**
- **`for`**: Ripete un blocco di codice per un numero definito di volte.
```java
for (int i = 0; i < 5; i++) {
    System.out.println("Ripetizione numero " + i);
}
```

- **`while`**: Ripete un blocco finché una condizione è vera.
```java
int i = 0;

while (i < 5) {
    System.out.println("Ripetizione numero " + i);
    i++;
}
```

- **`do-while`**: Simile a `while`, ma garantisce che il blocco venga eseguito almeno una volta, perché la condizione è verificata alla fine.
```java
int i = 0;
do {
    System.out.println("Ripetizione numero " + i);
    i++;
} while (i < 5);
```

3. **Interruzioni di flusso (`break`, `continue`, `return`)**
ESISTONO DUE TIPI di `break`
- `break senza etichetta`: Esce immediatamente dal ciclo o dal blocco `switch`.
```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break; // Interrompe il ciclo quando i è 5
    }
    System.out.println(i);
}
```

- `break con etichetta (labeled)`: serve per uscire da cicli annidati, in pratica se scrivo un'etichetta, sotto un ciclo for con dentro un altro ciclo for, con questo tipo di break, se esco dal ciclo più interno mi esce da tutto il blocco.
```java
etichetta: // Etichetta per il ciclo esterno
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break etichetta; // Esce dal ciclo esterno, si collega a etichetta e 
                             // salta TUTTO il blocco
        }
        System.out.println("i: " + i + ", j: " + j);
    }
}
```

- **`continue`**: Salta l'iterazione corrente e passa a quella successiva del ciclo.
```java
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue; // Salta i numeri pari
    }
    System.out.println(i);
}
```

- **`return`**: Termina l’esecuzione di un metodo e può restituire un valore.
```java
public int somma(int a, int b) {
    return a + b; // Interrompe il metodo e restituisce il risultato
}
```
>[!warning] DEVO SEMPRE SCRIVERE COSA RITORNARE, `return` da solo non va bene.

>[!bug]- cosa succede se non uso le parentesi { } ad esempio in un if?
>java non si basa sull'indentazione dobbiamo usare le graffe
>``` java
>  if(x>10) 
> 	non esco;
> 	piove;
> else
> 	roba;
>``` 
>lui farà se si verifica l'if non esco ma piove lo eseguirà come un blocco che non dipende dall'if 
## CLASSI
Una classica dichiarazione di una classe è questa
```java
class esempioClasse {
	// campi
	// costruttore 
	// metodi
}
```
DEFINIZIONI:
1. Campi (o Attributi)
	- sono **variabili** che rappresentano le caratteristiche o i dati di un oggetto.
	- definiscono lo **stato** di un oggetto e sono dichiarati all'interno della classe ma fuori dai metodi.

2. Costruttore
	- è uno **speciale metodo** che viene chiamato automaticamente quando si crea un nuovo oggetto di una classe.
	- serve per **inizializzare** i campi di un oggetto.
	- ha lo stesso nome della classe e non ha un tipo di ritorno.

3. Metodi
	- sono **funzioni** definite all'interno di una classe che permettono di eseguire azioni o comportamenti specifici su un oggetto.
	- possono modificare lo stato di un oggetto (cambiando i valori dei campi) o eseguire altre operazioni.

Definiamo una classe `Automobile`
```java
public class Automobile {
    
    // La classe Automobile ha tre campi
    public int velocità;
    public int marcia;
    public int livelloCarburante;
    
    // La classe Automobile ha un costruttore
    public Automobile(int velocitàIniziale, int marciaIniziale, int 
                      livelloCarburanteIniziale) {
        velocità = velocitàIniziale;
        marcia = marciaIniziale;
        livelloCarburante = livelloCarburanteIniziale;
    }
    
    // La classe Automobile ha quattro metodi
    public void cambiaMarcia(int nuovaMarcia) {
        marcia = nuovaMarcia;
    }
    
    public void accelera(int incremento) {
        velocità += incremento;
    }
    
    public void frena(int decremento) {
        velocità -= decremento;
    }
    
    public void rifornisci(int carburanteAggiunto) {
        livelloCarburante += carburanteAggiunto;
    }
    
}
```
Dove:
- **Campi**: `velocità`, `marcia`, `livelloCarburante`
	- `velocità`: rappresenta la velocità attuale dell'automobile.
	- `marcia`: rappresenta la marcia attuale dell'automobile.
	- `livelloCarburante`: rappresenta il livello di carburante nell'automobile.

- **Costruttore**: `Automobile(int velocitàIniziale, int marciaIniziale, int livelloCarburanteIniziale)` che inizializza i campi dell'automobile con i valori specificati quando viene creata una nuova istanza.

- **Metodi**:
	- `cambiaMarcia(int nuovaMarcia)`: cambia la marcia dell'automobile.
	- `accelera(int incremento)`: aumenta la velocità dell'automobile.
	- `frena(int decremento)`: riduce la velocità dell'automobile.
	- `rifornisci(int carburanteAggiunto)`: aggiunge carburante al serbatoio.
#### Sottoclasse
Possiamo dare più informazioni ad una classe, ad esempio immaginiamo che esempioClasse sia una sottoclasse:
```java
class esempioClasse extends SuperClasse implements Interfaccia{
	// campi
	// costruttore 
	// metodi
}
```
Quindi sappiamo che `esempioClasse` è una sottoclasse di `SuperClasse` che implementa `interfaccia`

###### CREIAMO ORA UNA `SOTTOCLASE` CHE `ESTENDE` `AUTOMOBILE`
```java
public class AutomobileSportiva extends Automobile {
    
    // La sottoclasse AutomobileSportiva ha un campo
    public int potenzaMotore; // potenza del motore in cavalli
    
    // La sottoclasse AutomobileSportiva ha un costruttore
    public AutomobileSportiva(int potenzaIniziale, int velocitàIniziale,
                              int marciaIniziale, int livelloCarburanteIniziale) {
        super(velocitàIniziale, marciaIniziale, livelloCarburanteIniziale);
        potenzaMotore = potenzaIniziale;
    }
    
    // La sottoclasse AutomobileSportiva ha un metodo
    public void aumentaPotenza(int incremento) {
        potenzaMotore += incremento;
    }  
}
```
Ha tutte le caratteristiche di `Automobile` ma 
- ha un campo in più, `potenzaMotore`
- il suo costruttore riprende quello di `Automobile` (con `super`) e aggiunge `potenzaMotore`
- ha un metodo nuovo, `aumentaPotenza`

#### IN GENERALE LA DICHIARAZIONE DI UNA CLASSE HA QUESTE COMPONENTI, IN ORDINE
1. modificatori come `public`, `private` e altri (che vedremo poi).
2. il nome della classe.
3. il nome della classe padre (`superclass`), se presente, deve essere preceduta da extends. Una classe può essere figlia di un solo padre.
4. l'interfaccia, se presente, deve essere preceduta da `implements`. Se implementi più interfacce, separale con `,`.
5. il corpo della classe deve trovarsi tra `{}`

## Tipi di variabili
1. **Variabili di istanza** (o campi):
	- sono variabili definite direttamente all'interno di una classe ma **fuori da qualsiasi metodo**.
	- rappresentano le **caratteristiche** o lo **stato** di un oggetto della classe e sono quindi memorizzate per ogni istanza creata (ogni sottoclasse ha queste caratteristiche), e per questo vengono chiamate **campi** o **variabili di istanza**. 
	- sono composti da tre componenti, in ordine
		- zero o più **modificatori**, come `public` o `private`
		- il **tipo**
		- il **nome**
```java
public class Automobile {
    // Variabili di istanza
    private int velocità;
    private int marcia;
    private int livelloCarburante;
    
    // Costruttore per inizializzare le variabili di istanza
    public Automobile(int velocitàIniziale, int marciaIniziale, int 
                      livelloCarburanteIniziale) {
        velocità = velocitàIniziale;
        marcia = marciaIniziale;
        livelloCarburante = livelloCarburanteIniziale;
    }
}
```

2. **Variabili locali**:
	- sono dichiarate all'interno di un **metodo**, un **blocco di codice**, o un **costruttore**.
	- esistono solo all'interno di quello specifico metodo o blocco e **non possono essere utilizzate** all'esterno di esso.
	- non conservano il valore quando il metodo termina.
```java
public class EsempioVariabiliLocali {
	
    public void calcolaDistanza() {
        // Variabile locale
        int distanzaPercorsa = 100;
        
        // Uso della variabile locale
        System.out.println("La distanza percorsa è: " + distanzaPercorsa + " km");
    }
}
```

3. **Parametri**:
	- sono variabili che vengono dichiarate all'interno della **firma di un metodo**.
	- servono per ricevere valori passati al metodo quando viene chiamato.
	- esistono solo all'interno del metodo in cui sono definiti.
```java
public class EsempioParametri {
	
    public void impostaVelocità(int nuovaVelocità) {
        // `nuovaVelocità` è un parametro
        System.out.println("Imposta la velocità a: " + nuovaVelocità + " km/h");
    }
}
```


### Modificatori d'accesso
Abbiamo visto prima due modificatori, `public` e `private` (ma ce ne sono anche altri).
Questi servono per definire **chi può accedere** a variabili (campi), metodi e costruttori di una classe:

- **public**: rende accessibile un campo o un metodo **a tutte le altre classi**. Se un campo è `public`, può essere visto e modificato direttamente da qualunque classe (sottoclassi e non).

- **private**: limita l’accesso a un campo o un metodo solo alla classe stessa. Questo significa che nessun'altra classe può accedere direttamente ai campi `private`.
>[!bug] anche il main è in una classe quindi non può accedere ai campi privati di altre classi
#### Incapsulamento
È un concetto che consiste nel mantenere i **dati privati** all'interno della classe, permettendo l'accesso solo tramite metodi pubblici. Questo permette di controllare e proteggere i dati di una classe e di evitare che vengano modificati in modo imprevisto o non autorizzato.
```java
public class Persona {
    
    // Campo privato
    private String nome;
    
    // Costruttore per inizializzare il nome
    public Persona(String nomeIniziale) {
        nome = nomeIniziale; 
    }
    
    // Metodo pubblico per ottenere il valore di nome (getter)
    public String getNome() {
        return nome;
    }
    
    // Metodo pubblico per impostare un nuovo valore per nome (setter)
    public void setNome(String nuovoNome) {
        if (nuovoNome != null && !nuovoNome.isEmpty()) { // controllo per evitare 
                                                         // nomi vuoti
            nome = nuovoNome; 
        } else {
            System.out.println("Il nome non può essere vuoto.");
        }
    }
}
```
I metodi `get` e `set` servono per accedere ai campi privati dall'esterno della classe
- un **getter** restituisce il valore di un campo
- un **setter** contente di modificate il valore di un campo

##### COSE NON CAPITE A LEZIONE DA LUCA
>[!tip]- Un metodo statico non puo accederea gli attributi dell'oggetto
>### Cosa significa `static`?
>
>- Un metodo o una variabile dichiarata come `static` **appartiene alla classe** stessa, non a una singola istanza (oggetto) della classe.
>- Questo significa che puoi usare i metodi o le variabili `static` **senza creare un oggetto della classe**.
>
>### Variabili di istanza vs Variabili statiche
>
>- **Variabili di istanza**: sono specifiche per ogni oggetto della classe. Ogni volta che crei un nuovo oggetto, ottiene la propria copia di queste variabili.
>- **Variabili statiche**: sono condivise da tutti gli oggetti della classe e appartengono alla classe stessa, non a singoli oggetti.
>
>### Perché un metodo `static` non può accedere alle variabili di istanza?
>
Un **metodo `static` non "vede" nessuna istanza della classe** (cioè nessun oggetto specifico). Poiché le variabili di istanza appartengono a singoli oggetti, un metodo `static` non può accedervi direttamente, perché non sa quale oggetto dovrebbe "vedere".
>
Invece, un metodo `static` può accedere solo alle **variabili e metodi statici**, perché questi appartengono alla classe, proprio come il metodo `static`.

>[!tip]- Si parte da questa frase
>`La dimensione dei dati primitivi è invariante perchè tutto è adattato alla jvm il byte è un byte invece un char è un carattere 16bit flat.`
>
>In java **“flat”** si riferisce al fatto che il tipo di dato è **di dimensione fissa** e non cambia indipendentemente dalla piattaforma o dal sistema operativo su cui gira il programma. In Java, i tipi primitivi (come `byte`, `int`, `char`) hanno una dimensione precisa e invariabile, che è garantita dalla **Java Virtual Machine (JVM)**.
>
>Quando si dice che un **`char` è un carattere "16-bit flat"** in Java, significa che:
>- Ogni variabile di tipo `char` occupa esattamente **16 bit** (2 byte) di spazio in memoria.
>- Questo è un valore fisso e **non dipende dalla piattaforma** (Windows, Linux, ecc.) o dall'architettura del sistema (32-bit o 64-bit).

## Metodi

Gli unici elementi **di base** richiesti nella dichiarazione di un metodo sono

- il **tipo** restituito
- il **nome**
- un paio di parentesi `()`
- un corpo tra le graffe `{}`

IN GENERALE, la dichiarazione di un metodo ha sei componenti, in ordine.

`public int calcolaDoppio(int numero) {     return numero * 2; }`

1. **Modificatori**
    
    - `public`
    - `private`
    - ecc.
    

2. **Tipo di Ritorno**
    
    - nel nostro caso `int`, il che vuol dire che quel metodo restituirà un intero
    - allo stesso modo abbiamo `float`, `double`, ecc.
    - se un metodo non restituisce alcun valore si usa `void`
    

3. **Nome del metodo** Viene utilizzato come un'etichetta che ci permette di chiamare o riferirci a questo metodo in altre parti del programma.
    
    - nel nostro caso `calcolaDoppio` (convenzionalmente in java si usa il camelCase).
    

4. **Lista di parametri** Sono variabili di input che il metodo riceve per lavorare. Se un metodo non richiede parametri, si usano **parentesi vuote** `()`.
    
    - nel nostro caso `(int numero)`
    

5. **Lista di eccezioni** (la vedremo poi)

6. **Corpo del metodo** È il blocco di codice tra graffe `{}`. Può contenere calcoli, dichiarazioni di variabili locali, controlli condizionali, ecc.
    
    - nel nostro caso `{ return numero * 2; }`.

#### Nomi di un metodo
per quanto uno possa dare qualsiasi nome a un metodo ci sono dei nomi che vengono usati per convenzione, scritti in camelCase
- run
- runFast
- getBackground
- getFinalData
- compareTo
- setX
- isEmpty

DEFINIZIONE: FIRMA La firma del metodo (o method signature) è una combinazioni di due componenti della dichiarazione di un metodo.

1. nome del metodo
2. tipi dei parametri del metodo, nell'ordine in cui appaiono

La firma di un metodo non include né il tipo di ritorno né i nomi dei parametri; conta solo il nome del metodo e i tipi dei parametri.

### Perché la Firma del Metodo è Importante?

La firma del metodo è ciò che distingue un metodo dagli altri all'interno di una classe. Java utilizza la firma per capire quale metodo chiamare in caso di _overloading_ (sovraccarico di metodi), cioè quando esistono più metodi con lo stesso nome ma con tipi o numeri di parametri diversi. #### Esempio Consideriamo questi metodi

`>public class Calcolatrice {     public int somma(int a, int b) {         return a + b;     }      public double somma(double a, double b) {         return a + b;     }      public int somma(int a, int b, int c) {         return a + b + c;     } }`

In questo esempio, tutti e tre i metodi si chiamano `somma`, ma le loro firme sono diverse:

1. `somma(int, int)` – nome del metodo `somma` e parametri `int, int`.
2. `somma(double, double)` – nome del metodo `somma` e parametri `double, double`.
3. `somma(int, int, int)` – nome del metodo `somma` e parametri `int, int, int`.

##### Metodi di Overload
Java distingue i metodi con lo stesso nome all'interno di una classe dalle differenze nel passaggio di parametri
Se vuoi ad esempio usare dei metodi simili in una classe sarebbe una rottura trovare dei nuovi modi per chiamare ogni metodo, e qui entra in gioco l'overloading

``` java
public class DataArtist {
    ...
    public void draw(String s) {
        ...
    }
    public void draw(int i) {
        ...
    }
    public void draw(double f) {
        ...
    }
    public void draw(int i, double f) {
        ...
    }
}

```
sono tutti dei metodi distinti perché alla loro chiamata richiedono argomenti diversi
#### Costruttori
Un **costruttore** è un blocco di codice speciale in una classe che viene chiamato quando viene creato un nuovo oggetto. Serve per **inizializzare l'oggetto**, impostando i valori iniziali dei campi (attributi) secondo le specifiche desiderate. 
##### Come Appare un Costruttore? Un costruttore:

- Ha lo **stesso nome della classe**.
- Non ha un **tipo di ritorno** (non può essere `void` o altro).

##### Creare un oggetto con un costruttore Riprendendo la classe `Automobile` che abbiamo visto prima, possiamo creare un oggetto inserendo nel main questo:

`Automobile fiatPunto = new Automobile(0, 1, 60)`

Questo codice:

- **Alloca spazio in memoria** per un nuovo oggetto `Automobile`.
- Chiama il costruttore `Automobile(int, int, int)` per **inizializzare i campi** `velocità`, `marcia`, e `livelloCarburante` con i valori `0`, `1`, e `60`, rispettivamente.

###### Costruttori Multipli Una classe può avere **più costruttori**, ciascuno con un diverso numero e tipo di parametri. Questo è utile per creare oggetti con diverse configurazioni iniziali.

``` java
public class Bicycle {     
private int gear;     
private int cadence;     
private int speed;      // Costruttore senza argomenti (no-argument constructor)     
public Bicycle() {         
gear = 1;         
cadence = 10;         
speed = 0;    
} 
}
```

###### Costruttori di Default Se non dichiari nessun costruttore, il compilatore Java crea "automaticamente" (se lo crea da solo ma noi non lo vediamo) un **costruttore di default senza argomenti** per la tua classe. Questo costruttore chiama il costruttore senza argomenti della superclasse, e al massimo mette i valori di default degli attributi che abbiamo messo nella classe.
###### Uso dei Costruttori della Superclasse In una classe che estende un'altra (sottoclasse), puoi chiamare il costruttore della superclasse usando `super(...)`. Questo permette di inizializzare i campi della superclasse.
## Passare informazioni a un metodo o ad un costruttore
Due concetti fondamentali
- **Parametri**: sono le **variabili dichiarate nella firma** del metodo o del costruttore. Sono come "segnaposto" per i dati che il metodo userà quando viene chiamato.
- **Argomenti**: sono i **valori reali** passati al metodo al momento della chiamata, che devono corrispondere in `tipo` e `ordine` ai parametri.
###### ESEMPIO
```java
public class Calcolatrice {
    
    // Metodo che somma due numeri
    public int somma(int numero1, int numero2) {
        int risultato = numero1 + numero2;
        return risultato;
    }
}

public class Main {
    public static void main(String[] args) {
        Calcolatrice calc = new Calcolatrice(); // Crea un oggetto Calcolatrice
        
        int risultato = calc.somma(5, 3); // Chiama il metodo somma con gli 
                                          // argomenti 5 e 3
        System.out.println("La somma è: " + risultato); // Stampa: La somma è: 8
    }
}
```
- **Parametri**: `int numero1`, `int numero2`
- Argomenti: **5** (assegnato a `int numero1`) e **3** (assegnato a `int numero2`)

#### Passare un numero variabile di argomenti
Quando non sappiamo in anticipo quanti argomenti verranno passati al metodo possiamo usare una funzionalità java chiamata `varargs` (variadic arguments).
###### Come funziona?
Quando dichiari un metodo, scrivi
- tipo del parametro
- tre puntini e spazio `(... )`
- nome parametro
In questo modo, all'interno del metodo questo parametro verrà trattato come un **array**.
###### ESEMPIO
```java
public class Calcolatrice {
	
    // Metodo con varargs che accetta un numero variabile di int
    public int somma(int... numeri) {  // ho usato il varargs, numeri verrà 
                                       // trattato come un array di interi (int[])
        int sommaTotale = 0;
        for (int numero : numeri) {  // utilizzo il for-each
            sommaTotale += numero;
        }
        return sommaTotale;
    }
}

// vediamo nel main come funziona
public class Main {
    public static void main(String[] args) {
        Calcolatrice calc = new Calcolatrice();
		
        System.out.println(calc.somma(1, 2, 3));          // Output: 6
        System.out.println(calc.somma(10, 20));           // Output: 30
        System.out.println(calc.somma(5, 10, 15, 20, 25)); // Output: 75
        System.out.println(calc.somma());                 // Output: 0 (nessun 
                                                          // numero passato)
    }
}
```
>[!tip]- **Cosa Accade in Questo Codice?**
>- Quando chiamiamo `calc.somma(1, 2, 3)`, `numeri` diventa un array `[1, 2, 3]`, e il metodo restituisce `6`.
>- Quando chiamiamo `calc.somma(10, 20)`, `numeri` è `[10, 20]`, e il metodo restituisce `30`.
>- Quando chiamiamo `calc.somma(5, 10, 15, 20, 25)`, `numeri` è `[5, 10, 15, 20, 25]`, e il metodo restituisce `75`.
>- Quando chiamiamo `calc.somma()`, `numeri` è un **array vuoto** `[]`, e il metodo restituisce `0`.

##### UTILITÀ PRATICA DEL VARARGS
Il `varargs` può accettare anche tipi di dati contemporaneamente utilizzando `Object... NOME`
>[!lemma]- OBJECT
>In Java, `Object` è un **tipo di dato** (più precisamente, è la classe base di tutte le classi).
>Quindi io posso creare un array di `Object` (`Object[]`) che può contenere **qualsiasi tipo di oggetto**.
###### ESEMPIO
```java
public class Utility {

    // Metodo con varargs di tipo Object, accetta qualsiasi tipo di oggetto
    public void stampaOggetti(Object... oggetti) {
        for (Object oggetto : oggetti) {
            System.out.println(oggetto);
        }
    }
}

// ora utilizziamolo nel main
public class Main {
    public static void main(String[] args) {
        Utility cose = new Utility();
		
        // Passiamo diversi tipi di argomenti
        cose.stampaOggetti("Ciao", 123, 45.67, true, 'A');
    }
}
```
OUTPUT
```kotlin
Ciao
123
45.67
true
A
```

##### LIMITAZIONI DI VARARGS
1. Posso passare un solo parametro varargs per metodo.
	**ESEMPIO VALIDO**
	```java
	public void metodoConVarargs(int... numeri) {
	    // codice
	}
	```

	**ESEMPIO NON VALIDO**
```java
	public void metodoNonValido(int... numeri, String... parole) { 
	    // codice
	}

```

2. Il parametro `varargs` (`...`) deve essere l'ultimo nella lista di parametri
	**ESEMPIO VALIDO**
	```java
	public void metodoConVarargs(String nome, int... Cose) {
	    // codice
	}
	```

	**ESEMPIO NON VALIDO**
```java
	public void metodoNonValido(int... Cose, String nome) { 
	    // codice
	}
```


### Shadowing in java
In java non si mettono parametri con lo stesso nome in un metodo 

``` java
public void exampleMethod(int number, int number) {
    // This will cause a compilation error
}

```

però potrebbe accadere che tu abbia dei parametri che hanno lo stesso nome di alcuni attributi della classe, per ovviare a questo usiamo il `this` ma lo vedremo poi

``` java
public class Circle {
    private int x, y, radius;
    public void setOrigin(int x, int y) {
        ...
    }
}
```

## OGGETTI
Li abbiamo già visti, ma facciamo un altro esempio.
Proveremo a creare due oggetti `Giocatore` e `Squadra`
```java
public class Giocatore {
    String nome;
    int numero;

    // Costruttore per inizializzare nome e numero
    public Giocatore(String n, int num) {
        nome = n;   // Assegna il parametro `n` al campo `nome`
        numero = num; // Assegna il parametro `num` al campo `numero`
    }

    // Metodo per cambiare il numero di maglia
    public void cambiaNumeroMaglia(int nuovoNumero) {
        numero = nuovoNumero; // Cambia il numero di maglia
    }

    // Metodo per visualizzare le informazioni del giocatore
    public void mostraInfo() {
        System.out.println("Nome: " + nome + ", Numero: " + numero);
    }
}

public class Main {
    public static void main(String[] args) {
        // Creiamo alcuni oggetti Giocatore
        Giocatore Rin = new Giocatore("Rin", 10);
        Giocatore Isagi = new Giocatore("Isagi", 11);

        // Cambiamo il numero di maglia dei giocatori
        Rin.cambiaNumeroMaglia(11);
        Isagi.cambiaNumeroMaglia(10);

        // Visualizziamo le informazioni dei giocatori
        Rin.mostraInfo();
        Isagi.mostraInfo();
    }
}

```
 
#### Accedere ai campi di un oggetto all'interno della classe
Quando scrivi un metodo all'interno di una classe, puoi accedere direttamente ai campi (o attributi) della classe semplicemente usando i loro nomi. Vediamo un esempio con una classe `Rettangolo` che ha due campi: `larghezza` e `altezza`.
```java
public class Rettangolo {
    int larghezza;
    int altezza;
	
    // Costruttore per impostare larghezza e altezza
    public Rettangolo(int w, int h) {
        larghezza = w;
        altezza = h;
    }
	
	// Metodo per calcolare l'area del rettangolo
    public int calcolaArea() {
        return larghezza * altezza;
    }
}
```
Qui:
- All'interno della classe `Rettangolo`, possiamo accedere ai campi `larghezza` e `altezza` direttamente usando i loro nomi (`larghezza` e `altezza`) perché siamo **all'interno della stessa classe**.

Quando chiamiamo `mostraDimensioni()`, questo metodo stampa i valori di `larghezza` e `altezza` dell'oggetto.

##### Accedere ai campi e/o metodi di un oggetto dall'esterno della classe
Quando usi un oggetto della classe `Rettangolo` in un'altra classe, come nel `main`, per accedere ai suoi campi hai bisogno di usare il nome dell'oggetto seguito da un punto (`.`), e poi il nome del campo.
```java
public class Main {
    public static void main(String[] args) {
        // Creiamo un oggetto Rettangolo
        Rettangolo rettangolo1 = new Rettangolo(10, 20);
		
        // Accediamo ai campi dall'esterno della classe Rettangolo
        System.out.println("Larghezza di rettangolo1: " + rettangolo1.larghezza);
        System.out.println("Altezza di rettangolo1: " + rettangolo1.altezza);
    }
    
		// Chiamiamo il metodo calcolaArea sull'oggetto rettangolo1
        int area = rettangolo1.calcolaArea();
	
        // Stampiamo l'area
        System.out.println("L'area di rettangolo1 è: " + area);
}
```
Qui:
- `rettangolo1.larghezza` accede al campo `larghezza` dell'oggetto `rettangolo1`.
- `rettangolo1.altezza` accede al campo `altezza` dell'oggetto `rettangolo1`.
- `rettangolo1.calcolaArea()` accede al metodo `calcoloArea()` dell'oggetto `rerttangolo1`.

Poiché stiamo accedendo ai campi dall'esterno della classe `Rettangolo`, dobbiamo usare il riferimento all'oggetto (`rettangolo1`) per specificare **di quale oggetto stiamo parlando**.

#### Ogni oggetto ha i propri campi
Oggetti dello stesso tipo hanno campi con lo stesso nome, ma ogni oggetto ha la **propria copia di quei campi**. Questo significa che se creiamo due oggetti `Rettangolo`, ognuno avrà i propri valori per `larghezza` e `altezza`.
```java
public class Main {
    public static void main(String[] args) {
        // Creiamo due oggetti Rettangolo con dimensioni diverse
        Rettangolo rettangolo1 = new Rettangolo(10, 20);
        Rettangolo rettangolo2 = new Rettangolo(15, 25);
		
        // Mostriamo le dimensioni dei due rettangoli
        System.out.println("Dimensioni di rettangolo1: Larghezza = " + 
                            rettangolo1.larghezza + ", Altezza = " + 
                            rettangolo1.altezza);
        System.out.println("Dimensioni di rettangolo2: Larghezza = " + 
                            rettangolo2.larghezza + ", Altezza = " + 
                            rettangolo2.altezza);
    }
}
```
Qui, `rettangolo1` e `rettangolo2` hanno campi `larghezza` e `altezza` indipendenti. Quando accediamo a `rettangolo1.larghezza` o `rettangolo2.larghezza`, vediamo i valori specifici di ciascun oggetto.

#### Creare un Oggetto e Accedere Direttamente al Campo
Puoi anche creare un nuovo oggetto e accedere immediatamente a uno dei suoi campi, senza salvare l'oggetto in una variabile. Ad esempio:
```java
int altezza = new Rettangolo(10, 20).altezza;
System.out.println("Altezza del nuovo rettangolo: " + altezza);
```
In questo caso:
- Creiamo un nuovo `Rettangolo` con `larghezza = 10` e `altezza = 20`.
- Accediamo direttamente al campo `altezza` e salviamo il valore in `altezza`.

Dopo questa riga, non abbiamo più nessun riferimento al `Rettangolo` creato, quindi l'oggetto potrebbe essere eliminato dalla memoria dal **Garbage Collector** perché non è più utilizzabile.

#### Garbage Collector
Il **Garbage Collector** (GC) in Java è un meccanismo automatico che gestisce la memoria, liberando spazio occupato da oggetti non più utilizzati dal programma. In pratica, quando un oggetto non ha più riferimenti che lo puntano, il Garbage Collector lo elimina per recuperare la memoria.

##### Come Funziona il Garbage Collector?
1. **Creazione di Oggetti**: Ogni volta che creiamo un nuovo oggetto con `new`, Java riserva uno spazio in memoria per quell'oggetto.
    
2. **Riferimenti agli Oggetti**: Finché una variabile punta a quell'oggetto, esso è considerato "in uso". Se la variabile cambia valore o esce dal suo ambito (come una variabile locale che viene eliminata al termine di un metodo), l'oggetto può diventare non più raggiungibile.
    
3. **Oggetti Non Raggiungibili**: Quando non ci sono più riferimenti a un oggetto, Java lo considera non più necessario. Questo è un segnale per il Garbage Collector che l’oggetto può essere eliminato dalla memoria.
    
4. **Esecuzione del Garbage Collector**: Java, in automatico e a intervalli regolari, esegue il Garbage Collector per trovare e rimuovere questi oggetti inutilizzati, liberando così la memoria per nuovi oggetti.
###### ESEMPIO
```java
public class Main {
    public static void main(String[] args) {
        Persona p1 = new Persona("Mario"); // Crea un nuovo oggetto Persona
        Persona p2 = new Persona("Luigi"); // Crea un altro oggetto Persona
        
        p1 = null; // p1 non punta più a "Mario"
        p2 = null; // p2 non punta più a "Luigi"
        
        // A questo punto, entrambi gli oggetti "Mario" e "Luigi" non sono più 
        // raggiungibili e saranno eliminati dal Garbage Collector in un momento 
        // successivo
    }
}
```


#### Ritorno di un valore da un metodo
Un metodo in Java ritorna al punto in cui è stato chiamato in tre situazioni:
1. Quando completa tutte le istruzioni all'interno del metodo.
2. Quando raggiunge un'istruzione `return`.
3. Quando lancia un'eccezione (un concetto che verrà trattato successivamente).

In altre parole, appena il metodo ha finito di eseguire il suo lavoro in uno di questi modi, restituisce il controllo al codice che lo ha invocato.

##### Dichiarare il Tipo di Ritorno di un Metodo
Quando si dichiara un metodo, si deve specificare il tipo di dato che il metodo restituirà. Questo viene indicato prima del nome del metodo. All'interno del corpo del metodo, utilizziamo l'istruzione `return` per specificare il valore che vogliamo restituire.

##### Metodo `void` (che Non Ritorna Valori)
Un metodo dichiarato come `void` non restituisce alcun valore. Poiché non restituisce nulla, non è necessario includere un'istruzione `return` all'interno del metodo. 
Tuttavia, è possibile utilizzare `return;` per uscire dal metodo in determinati punti, se necessario. In questo caso, `return;` funziona come un'istruzione per uscire dal metodo e basta, senza restituire alcun valore.
###### ESEMPIO
```java
public void stampaMessaggio() {
    System.out.println("Questo è un messaggio.");
    return; // Questo return termina l'esecuzione del metodo
}
```
>[!warning]- Se provo a far ritornare qualcosa dal void mi da errore. Posso solo usare `return;`

#### Metodi che Non Sono Dichiarati `void`
Qualsiasi metodo che non è dichiarato `void` deve avere un'istruzione `return` con un valore da restituire, in questo formato:
```java
return valoreDiRitorno;
```
Il tipo di dato del valore restituito (dopo `return`) deve corrispondere al tipo di ritorno dichiarato del metodo. Ad esempio, se un metodo è dichiarato per restituire un `int`, non è possibile restituire un valore `boolean`, perché i tipi non corrispondono.


>[!warning] MANCA LA PARTE RETURN AN OBJECT E RETURN A CLASS OR INTERFACE


#### Parola chiave: This 
In Java, la parola chiave `this` rappresenta il **riferimento all'oggetto corrente**. Serve per distinguere i campi (o attributi) dell'oggetto dai parametri del metodo o del costruttore, soprattutto quando hanno lo stesso nome.
###### ESEMPIO
Immaginiamo di avere una classe `Persona` con un campo `nome` che rappresenta il nome di una persona. Vogliamo creare un costruttore che prenda un parametro `nome` per impostare il valore di questo campo.
```java
public class Persona {
    String nome; // Campo della classe
	
    // Costruttore
    public Persona(String nome) {
        // Usando `this` per distinguere il campo `nome` dal parametro `nome`
        this.nome = nome;
    }
}
```
In questo esempio:
- `String nome` è un campo della classe `Persona`.
- Nel costruttore, `nome` è anche il nome del parametro.

Quando scriviamo `this.nome = nome;`:
- `this.nome` si riferisce al **campo `nome` della classe** `Persona` (l'oggetto stesso).
- `nome` (senza `this`) si riferisce al **parametro** del costruttore.

IL MAIN RIMANE COME LO CONOSCIAMO, IL "CAMBIAMENTO" AVVIENE SOLO NELLA CLASSE


##### COSE NON CAPITE A LEZIONE DA LUCA
>[!tip]- Un metodo statico non puo accederea gli attributi dell'oggetto
>### Cosa significa `static`?
>
>- Un metodo o una variabile dichiarata come `static` **appartiene alla classe** stessa, non a una singola istanza (oggetto) della classe.
>- Questo significa che puoi usare i metodi o le variabili `static` **senza creare un oggetto della classe**.
>
>### Variabili di istanza vs Variabili statiche
>
>- **Variabili di istanza**: sono specifiche per ogni oggetto della classe. Ogni volta che crei un nuovo oggetto, ottiene la propria copia di queste variabili.
>- **Variabili statiche**: sono condivise da tutti gli oggetti della classe e appartengono alla classe stessa, non a singoli oggetti.
>
>### Perché un metodo `static` non può accedere alle variabili di istanza?
>
Un **metodo `static` non "vede" nessuna istanza della classe** (cioè nessun oggetto specifico). Poiché le variabili di istanza appartengono a singoli oggetti, un metodo `static` non può accedervi direttamente, perché non sa quale oggetto dovrebbe "vedere".
>
Invece, un metodo `static` può accedere solo alle **variabili e metodi statici**, perché questi appartengono alla classe, proprio come il metodo `static`.

>[!tip]- Si parte da questa frase
>`La dimensione dei dati primitivi è invariante perchè tutto è adattato alla jvm il byte è un byte invece un char è un carattere 16bit flat.`
>
>In java **“flat”** si riferisce al fatto che il tipo di dato è **di dimensione fissa** e non cambia indipendentemente dalla piattaforma o dal sistema operativo su cui gira il programma. In Java, i tipi primitivi (come `byte`, `int`, `char`) hanno una dimensione precisa e invariabile, che è garantita dalla **Java Virtual Machine (JVM)**.
>
>Quando si dice che un **`char` è un carattere "16-bit flat"** in Java, significa che:
>- Ogni variabile di tipo `char` occupa esattamente **16 bit** (2 byte) di spazio in memoria.
>- Questo è un valore fisso e **non dipende dalla piattaforma** (Windows, Linux, ecc.) o dall'architettura del sistema (32-bit o 64-bit).


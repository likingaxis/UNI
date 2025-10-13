### Livelli di Accesso
1. **public**: visibile a **tutti**. Se un campo o un metodo è `public`, qualsiasi classe, in qualsiasi pacchetto, può accedervi.
    
2. **protected**: visibile all'interno del **package** in cui è definito, **e** nelle **sottoclassi** (anche se sono in un altro pacchetto). Viene usato spesso quando vuoi che una variabile o un metodo sia accessibile solo dalle classi che derivano da quella principale.
    
3. **package-private** (nessun modificatore): se non scrivi nulla, il campo o metodo è visibile solo **all'interno del package** in cui si trova la classe. Questo è utile quando vuoi che qualcosa sia accessibile alle classi che fanno parte dello stesso gruppo (pacchetto), ma non fuori.
    
4. **private**: visibile solo **all'interno della classe** in cui è dichiarato. `private` è il modificatore più restrittivo e viene usato quando non vuoi che nessun’altra classe possa accedere a quella variabile o metodo.

###### TABELLA 
In questa tabella possiamo vedere, in base al modificatore, chi può vederne il contenuto
NB: per `WORLD` si intende dentro e fuori il pacchetto.

- class significa se gli elementi in quella classe possono vedere se stessi
- gli elementi che stanno nello stesso package possono vedersi tra di loro?
- da una sottoclasse posso vedere gli elementi della super classe
- al livello globale posso vedere gli elementi delle altre classi ecc...

| <center>MODIFICATORE</center>              | CLASSI              | PACCHETTO           | SOTTOCLASSI         | WORLD               |
| ------------------------------------------ | ------------------- | ------------------- | ------------------- | ------------------- |
| <center>***public***</center>              | <center>SI</center> | <center>SI</center> | <center>SI</center> | <center>SI</center> |
| <center>***protected***</center>           | <center>SI</center> | <center>SI</center> | <center>SI</center> | <center>NO</center> |
| <center>***nessun modificatore***</center> | <center>SI</center> | <center>SI</center> | <center>NO</center> | <center>NO</center> |
| <center>private</center>                   | <center>SI</center> | <center>NO</center> | <center>NO</center> | <center>NO</center> |

###### ESEMPI
```java
public class Alpha {
	// CAMPI
    public int campoPubblico;   // Visibile a tutti
    protected int campoProtetto; // Visibile solo nel pacchetto e nelle sottoclassi
    int campoSenzaModificatore; // Visibile solo nel pacchetto
    private int campoPrivato;   // Visibile solo all'interno di Alpha
	
    
    // METODI
    public void metodoPubblico() { /*...*/ }
    protected void metodoProtetto() { /*...*/ }
    void metodoSenzaModificatore() { /*...*/ }
    private void metodoPrivato() { /*...*/ }
}
```

###### ALTRO ESEMPIO
Immaginiamo di avere due pacchetti così
![[Pasted image 20241106190718.png]]
Ora vediamo dove posso vedere i membri della classe `Alpha` (ossia le sue variabili e i suoi metodi) in base ai modificatori che abbiamo visto prima

| <center>MODIFICATORE</center>              | ALPHA               | BETA                | ALPHASUB            | GAMMA               |
| ------------------------------------------ | ------------------- | ------------------- | ------------------- | ------------------- |
| <center>***public***</center>              | <center>SI</center> | <center>SI</center> | <center>SI</center> | <center>SI</center> |
| <center>***protected***</center>           | <center>SI</center> | <center>SI</center> | <center>SI</center> | <center>NO</center> |
| <center>***nessun modificatore***</center> | <center>SI</center> | <center>SI</center> | <center>NO</center> | <center>NO</center> |
| <center>private</center>                   | <center>SI</center> | <center>NO</center> | <center>NO</center> | <center>NO</center> |

>[!tip]- Alcuni consigli utili
>### Consigli Pratici
>
>1. **Usa `private` il più possibile**: rende il codice più sicuro, perché nessuna classe può modificare direttamente i campi privati. 
  >  
>2. **Evita campi `public`**, a meno che siano **costanti** (cioè variabili il cui valore non cambia). Questo perché i campi pubblici rendono difficile cambiare l'implementazione della tua classe in futuro senza rompere il codice di chi la usa.
 >   
>3. **Utilizza `protected` solo per le sottoclassi**: è utile quando pensi che le classi che derivano dalla tua (`subclassi`) abbiano bisogno di accedere a un campo o metodo, ma altre classi no.
  >  
>4. **Scegli `package-private`** (nessun modificatore) per metodi e campi che devono essere usati solo da classi dello stesso pacchetto, ma non dovrebbero essere accessibili da fuori.


---


In Java, la parola chiave `static` viene utilizzata per definire membri a livello di classe, il che significa che appartengono alla classe stessa piuttosto che a una specifica istanza della classe. Questo è applicabile sia alle variabili che ai metodi.

### Variabili di Classe (Campi Statici)
Quando un campo è dichiarato come `static`, significa che esiste solo una copia di quella variabile, condivisa tra tutte le istanze della classe. Questo è utile per i dati che devono essere coerenti tra tutti gli oggetti.
```java
public class Bicicletta {
    private int id;
    private static int numeroDiBiciclette = 0;
	
    public Bicicletta() {
        id = ++numeroDiBiciclette;
    }
}
```
In questo esempio, `numeroDiBiciclette` è un campo statico che tiene traccia di quante istanze della classe `Bicicletta` sono state create. Ogni nuovo oggetto `Bicicletta` incrementa questo conteggio e assegna a sé stesso un `id` unico.

### Metodi di Classe (Metodi Statici)
I metodi statici sono associati alla classe piuttosto che a un oggetto particolare. Possono essere chiamati senza creare un'istanza della classe.
```java
public class Bicicletta {
    private static int numeroDiBiciclette = 0;

    public static int getNumeroDiBiciclette() {
        return numeroDiBiciclette;
    }
}
```
Qui, `getNumeroDiBiciclette` è un metodo statico che restituisce il numero totale di istanze `Bicicletta` create. 
Può essere chiamato usando `Bicicletta.getNumeroDiBiciclette()` senza bisogno di istanziare un oggetto `Bicicletta` (ad esempio posso chiamarlo direttamente nel `main`).

il metodo dipende dallo stato dell'oggetto che lo chiama
E se io volessi fare qualcosa di indipendente dallo stato dell'oggetto?
uso static per fare funzioni
### Costanti
Ovviamente posso usare `static` anche con le costanti, in combinazione con `final` (che non mi permette più di modificarla).


---


### Inizializzazione campi
L'inizializzazione dei campi di una classe può essere gestita in diversi modi.

#### Inizializzazione diretta
È possibile assegnare un valore iniziale a un campo direttamente nella sua dichiarazione. Questo approccio è semplice e funziona bene quando il valore è noto e non richiede logica complessa.
```java
public class Esempio {
    private int numero = 10;
    private String testo = "Ciao";
}
```

#### Inizializzazione nei costruttori
I costruttori permettono di inizializzare i campi al momento della creazione di un'istanza della classe. Questo è utile quando l'inizializzazione dipende da parametri o richiede logica specifica.
```java
public class Esempio {
    private int numero;
    private String testo;
	
    public Esempio(int numero, String testo) {
        this.numero = numero;
        this.testo = testo;
    }
}
```

#### Blocchi di Inizializzazione
Blocco di Inizializzazione {}:

Viene eseguito ogni volta che un nuovo oggetto Esempio viene creato, indipendentemente da quale costruttore viene chiamato.

```java
public class Esempio {
    private int numero;
    private String testo;

    // Blocco di inizializzazione
    {
        numero = 5;
        testo = "Inizializzato";
    }

    public Esempio() {
        // Il blocco di inizializzazione viene eseguito prima di questo costruttore
    }

    public Esempio(int numero) {
        this.numero = numero;
        // Il blocco di inizializzazione viene eseguito prima di questo costruttore
    }
} 
```

Qui, numero viene impostato su 5 e testo su "Inizializzato".
Costruttori:

Ogni costruttore viene eseguito dopo il blocco di inizializzazione.
Nel costruttore senza parametri, il valore di numero sarà 5 (impostato nel blocco di inizializzazione).
- Nel costruttore con parametro, numero verrà impostato su 5 dal blocco di inizializzazione, ma poi sarà sovrascritto dal valore passato come parametro.
>[!question]- Perché Usare un Blocco di Inizializzazione?
> Immagina di avere del codice di inizializzazione che vuoi eseguire ogni volta che crei un oggetto
>  della classe, ma non vuoi ripeterlo in ogni costruttore. Il blocco di inizializzazione ti permette di
>   scrivere quel codice una sola volta, e viene eseguito sempre prima di qualsiasi costruttore.

#### Blocchi di Inizializzazione Statici 
Per i campi statici, che appartengono alla classe piuttosto che alle istanze, si utilizzano blocchi di inizializzazione statici. 
Questi vengono eseguiti una sola volta, quando la classe viene caricata.

```java
public class Esempio {
    private static int valoreStatico;

    static {
        valoreStatico = 100;
    }
}
```
#### PICCOLA PARENTESI SUL CONCETTO STATIC
Si può applicare su 3 cose:
- attributi
	- quando un attributo cambia per qualsiasi oggetto che istanzia la classe
- metodi
	- non varia in base allo stato dell'oggetto, quindi non ha senso chiamare l'oggetto
	- Possono essere chiamati senza creare un'istanza della classe.
	- si deve fare un eventuale passaggio di parametri per comunicare con questo tipo di metodo
	- si chiama facendo ``nomeclasse.nomemetodo(parametri)``
- classi annidate
	- la classe dentro non può accedere direttamente alla classe fuori
### Classi annidate
Quando abbiamo una classe con dentro un'altra classe
- possono essere statiche o dinamiche


###### Shadowing in classi annidate: 
- Lo shadowing si verifica quando una dichiarazione di una variabile in un determinato ambito (scope) ha lo stesso nome di una dichiarazione in un ambito esterno. In tali casi, la variabile nell'ambito interno "oscura" quella nell'ambito esterno, rendendo quest'ultima inaccessibile direttamente tramite il suo nome.
- quando siamo nella classe interna e vogliamo parlare 
	- della variabile locale al metodo: non usiamo nulla `nomevar`
	- della variabile interna alla classe: usiamo `this.nomevar`
	- variabile esterna: usiamo `nomeclasse.this.nomevar`

```java 
public class Esterna {
    int x = 10;

    class Interna {
        int x = 20;

        void mostraValori(int x) {
            System.out.println("x locale: " + x); // Variabile locale al metodo
            System.out.println("x di Interna: " + this.x); // Variabile di Interna
            System.out.println("x di Esterna: " + Esterna.this.x); // Variabile di Esterna
        }
    }

    public static void main(String[] args) {
        Esterna esterna = new Esterna();
        Esterna.Interna interna = esterna.new Interna();
        interna.mostraValori(30);
    }
}
```


>[!question]- a che serve usare classi annidate?
>in generale il concetto è dell'incapsulation, si usa un esempio di una macchina con uno specifico sportello, magari abbiamo una classe che va bene solo con una determinata classe, lo sportello 
>non lo avrò mai al di fuori di quella classe dove lo chiamo dentro


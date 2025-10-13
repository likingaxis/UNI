La seguente esercitazione è suddivisa in diverse sezioni in package
##### TUTTO FUORI DAL PACKAGE IL MAIN
```java
//TIP To <b>Run</b> code, press <shortcut actionId="Run"/> or
// click the <icon src="AllIcons.Actions.Execute"/> icon in the gutter.
public class Main {
    public static void main(String[] args) {
        //TIP Press <shortcut actionId="ShowIntentionActions"/> with your caret at the highlighted text
        // to see how IntelliJ IDEA suggests fixing it.
        System.out.printf("Hello and welcome!");

        for (int i = 1; i <= 5; i++) {
            //TIP Press <shortcut actionId="Debug"/> to start debugging your code. We have set one <icon src="AllIcons.Debugger.Db_set_breakpoint"/> breakpoint
            // for you, but you can always add more by pressing <shortcut actionId="ToggleLineBreakpoint"/>.
            System.out.println("i = " + i);
        }
    }
}
```
#### PACKAGE: it.uniroma2.lmp.lmp0
abbiamo test.java
```java
package it.uniroma2.lmp.lmp0;

import it.uniroma2.lmp.lmp0.model.*;

public class Test {

    public static void main(String[] args) {

        Persona franco = new PersonaImpl("Franco", "Bellucci", "xyz02");

        System.out.println("Abbiamo appena creato: " + franco);

        franco.saluta();


        Professore professore = new ProfessoreImpl("Armando", "Stellato", "1234", "Knowledge Engineering");

        Universita torVergata = new Universita();


        Studente stud1 = null;
        Studente stud2 = null;
        Studente stud3 = null;
        try {
            stud1 = torVergata.iscriviStudente("Mario" , "Rossi", "mrrs", CorsoDiStudi.INFORMATICA, 3);
            stud2 = torVergata.iscriviStudente("Luigi" , "Bianchi", "mr8e", CorsoDiStudi.INFORMATICA, 1);
            stud3 = torVergata.iscriviStudente("Marco" , "Neri", "rts", CorsoDiStudi.PSICOLOGIA, 7);
        } catch (Exception e) {
            System.err.println("C'è stato un problema di iscrizione: " + e.getMessage());
        }
        System.out.println(stud1 + "\n" + stud2 + "\n" + stud3);
        Professore x = null;
        stud1.saluta(x);
    }

}
```
#### it.uniroma2.lmpl.mp0.model
ABBIAMO 11 FILE 
AnnoCorsoException
```java
package it.uniroma2.lmp.lmp0.model;

public class AnnoCorsoException extends Exception {
    public AnnoCorsoException(int annoCorso) {
        super("L'anno " + annoCorso + " è fuori dai limiti ammessi da questa università");
    }
}

```
CorsoDiStudi
```java
package it.uniroma2.lmp.lmp0.model;

public enum CorsoDiStudi {
    INFORMATICA, PSICOLOGIA, LETTERE;
}

```
Persona
```java
package it.uniroma2.lmp.lmp0.model;

public interface Persona {
    //Normalm. si pensa prima all'interf. e poi alla classe

    //In questo caso e' piu' utile un getter invece del setter
    String getNome();

    String getCognome();

    String getCodiceFiscale();

    void saluta();

}

```
PersonaImpl
```java
package it.uniroma2.lmp.lmp0.model;

//Tra classi e interfacce si usa "implements", mentre tra classi/classi o
//interfacce/interfacce si usa "extends"

public class PersonaImpl implements Persona {
    String nome;
    String cognome;
    String codiceFiscale;
    /** <-- commento per doc (es. javadoc)
     * @param nome nome <em>persona</em>
     * @param cognome <-- i param sono dei tag
     * @param codiceFiscale
     */
    public PersonaImpl(String nome, String cognome, String codiceFiscale) {
        this.nome = nome;
        this.cognome = cognome;
        this.codiceFiscale = codiceFiscale;
    }

    //In questo caso e' piu' utile un getter invece del setter
    @Override
    public String getNome() {
        return nome;
    }
    @Override
    public String getCognome() {
        return cognome;
    }
    @Override
    public String getCodiceFiscale() {
        return codiceFiscale;
    }


    public void saluta() {
        System.out.println("Salve a tutti!");
    }

    @Override
    public String toString() {
        return nome + " " + cognome + ": " + codiceFiscale;
    }
}

```
Professore
```java
/**
 *
 */
package it.uniroma2.lmp.lmp0.model;

/**
 *
 */
public interface Professore extends Persona {

    //per scontato anche i metodi son tutti public
    String getCattedra();

    void setCattedra(String cattedra);
}

```
ProfessoreImpl
```java
/**
 *
 */
package it.uniroma2.lmp.lmp0.model;

/**
 *
 */
public class ProfessoreImpl extends PersonaImpl implements Professore {

    String cattedra;

    /**
     * @param nome
     * @param cognome
     * @param codiceFiscale
     * @param cattedra
     */

    public ProfessoreImpl(String nome, String cognome, String codiceFiscale, String cattedra) {
        super(nome, cognome, codiceFiscale);
        this.cattedra = cattedra; //e' cio' che fa setCattedra
    }

    @Override
    public String getCattedra() {
        return this.cattedra; //e' meglio this.cattedra
    }

    @Override
    public void setCattedra(String cattedra) {
        this.cattedra = cattedra;
    }

}

```
ProfessoreNonPresenteException
```java
package it.uniroma2.lmp.lmp0.model;

public class ProfessoreNonPresenteException extends RuntimeException {
    public ProfessoreNonPresenteException() {
        super("Il professore è assente (null) e non può essere salutato");
    }
}

```
Studente
```java
/**
 *
 */
package it.uniroma2.lmp.lmp0.model;

/**
 *
 */
public interface Studente extends Persona {

    String getMatricola();

    void saluta(Professore professore);

}

```
StudenteCDS
```java
package it.uniroma2.lmp.lmp0.model;

public class StudenteCDS extends StudenteImpl implements Studente {

    CorsoDiStudi CDS;
    int annoCorso;

    StudenteCDS(String nome, String cognome, String codiceFiscale, CorsoDiStudi CDS, int annoCorso) {
        super(nome, cognome, codiceFiscale, CDS.toString() + numStudenti);
        this.CDS = CDS;
        this.annoCorso = annoCorso;

    }

    StudenteCDS(Persona persona, CorsoDiStudi CDS, int annoCorso) {

        this(persona.getNome(), persona.getCognome(), persona.getCodiceFiscale(), CDS, annoCorso);
        //invoco il costruttore "principale"
    }


}

```
StudenteImpl
```java
package it.uniroma2.lmp.lmp0.model;

public class StudenteImpl extends PersonaImpl implements Studente {
    static int numStudenti;
    String matricola;

    protected StudenteImpl(String nome, String cognome, String codiceFiscale, String matricola) {
        super(nome, cognome, codiceFiscale);
        numStudenti++;
        this.matricola = matricola;

    }

    protected StudenteImpl(Persona persona, String matricola) {
        this(persona.getNome(), persona.getCognome(), persona.getCodiceFiscale(), matricola);
        //invoco il costruttore "principale"
    }

    @Override
    public String getMatricola() {
        return this.matricola;
    }


    @Override
    public void saluta(Professore professore) {
        if( professore == null) throw new ProfessoreNonPresenteException();
        System.out.println("Salve prof. " + professore.getCognome());

    }

    @Override
    public String toString() {
        return super.toString() + " " + matricola;
    }
}

```
Universita
```java
package it.uniroma2.lmp.lmp0.model;

public class Universita {

    public Studente iscriviStudente(String nome, String cognome, String codiceFiscale, CorsoDiStudi CDS, int annoCorso) throws AnnoCorsoException{
        if (annoCorso > 5){
            throw new AnnoCorsoException(annoCorso);
        }
        return new StudenteCDS(nome, cognome, codiceFiscale, CDS, annoCorso);
    }
}

```
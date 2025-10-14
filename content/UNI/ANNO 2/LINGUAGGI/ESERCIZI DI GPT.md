# ES 1
#### **Consegna:**

1. **Creare un'interfaccia chiamata `StudenteI`**:
    
    - Deve estendere un'altra interfaccia esistente chiamata `PersonaI`.
    - Dichiarare un metodo aggiuntivo:

        `public String getCorsoDiStudi();`
        
2. **Creare una classe concreta chiamata `Studente`**:
    
    - La classe deve implementare l'interfaccia `StudenteI`.
    - Deve avere i seguenti campi:
        - `String nome`: il nome dello studente.
        - `String cognome`: il cognome dello studente.
        - `String codicefiscale`: il codice fiscale dello studente.
        - `int piedi`: un campo qualsiasi per simulare l'esempio (es. altezza in piedi).
        - `String corsoDiStudi`: il corso di studi dello studente.
    - Implementare un costruttore che accetta tutti i campi come parametri.
    - Implementare i metodi richiesti dalle interfacce (`PersonaI` e `StudenteI`).
    - Sovrascrivere il metodo `toString()` per restituire una descrizione leggibile dello studente.
    - Implementare il metodo `saluta()`, che stampa un messaggio personalizzato, ad esempio: _"Ciao a tutti, sono uno studente di [corso di studi]!"_.
3. **Scrivere un programma di test**:
    
    - Creare un file di test chiamato `Test`.
    - Nel metodo `main`, creare un oggetto di tipo `Studente` e inizializzarlo con valori significativi.
    - Stampare l'oggetto utilizzando il metodo `toString()` e verificare il suo contenuto.
    - Chiamare il metodo `saluta()` dell'oggetto.
#### **Cosa consegnare:**

- Il codice sorgente dell’interfaccia `StudenteI`.
- Il codice sorgente della classe `Studente`.
- Il file di test con il `main`.

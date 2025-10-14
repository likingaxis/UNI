
>[!info]- factory 
>indica una classe che avrà un oggetto, questo oggetto ha il compito di creare altri oggetti attraverso i suoi metodi
>esempio di codice:
>
>
> ```java
> // Interfacce per i prodotti
> interface Button {
>     void paint();
> }
> 
> interface Checkbox {
>     void paint();
> }
> 
> // Implementazioni concrete dei prodotti
> class WindowsButton implements Button {
>     public void paint() {
>         System.out.println("Rendering a Windows Button");
>     }
> }
> 
> class WindowsCheckbox implements Checkbox {
>     public void paint() {
>         System.out.println("Rendering a Windows Checkbox");
>     }
> }
> 
> 
> // Abstract Factory
> interface GUIFactory {
>     Button createButton();
>     Checkbox createCheckbox();
> }
> 
> // Concrete Factory
> class WindowsFactory implements GUIFactory {
>     public Button createButton() {
>         return new WindowsButton();
>     }
> 
>     public Checkbox createCheckbox() {
>         return new WindowsCheckbox();
>     }
> }
> 
> // Uso dell'Abstract Factory
> public class Main {
>     public static void main(String[] args) {
>         GUIFactory factory = new WindowsFactory();
> 
>         Button button = factory.createButton();
>         Checkbox checkbox = factory.createCheckbox();
> 
>         button.paint();
>         checkbox.paint();
>     }
> }
> ```
> 
### Le annotazioni
>[!info] definizione
>Sono dei tag che ci consentono di "metaprogrammare" collegabili a qualsiasi cosa all'interno del nostro codice, semplicemente devi mettere $@annotazione$ sopra una classe, un metodo o quello che vuoi

- servono al <font color="#ff0000">compilatore</font> tipo override che gli indica di sovrascrivere un metodo
- servono per "chi viene dopo" e capire eventuali informazioni extra

>[!info]- cosa si intende per metaprogrammazione
>la programmazione che include metadati, ovvero informazioni aggiuntive ai dati stessi

##### CARATTERISTICHE DELLE ANNOTAZIONI
###### posso aggiungere dei campi a una annotazione
![[Pasted image 20241125181120.png|290]]
###### posso fare annotazioni multiple
![[Pasted image 20241125181256.png]]
###### posso ripetere le stesse annotazioni(da mettere in un contenitore repeatable)
![[Pasted image 20241125181451.png]]
###### Come creare una annotazione
![[Pasted image 20241125182016.png|500]]
creo il tipo di annotazione e ciò che devo contenere poi la applico ad una classe
![[Pasted image 20241125182054.png|400]]

### ANNOTAZIONI PREDEFINITE IN JAVA
#### 1.@DEPRECATED
Se lo mettiamo su un metodo indica che quest'ultimo è in disuso e quando verrà eseguito il codice verrà mandato un warning dal compilatore
<font color="#f79646">esempio di cobolzongz</font>
![[Pasted image 20241125183321.png|400]]
#### 2.@OVERRIDE
viene usato per indicare che un metodo interno a una classe sovrascrive un altro metodo 
![[Pasted image 20241125183443.png|400]]
#### 3.@SUPPRESSWARNINGS
Serve per sopprimere eventuali warning da parte del compilatore, bisogna specificare la categoria del warning es:
- deprecated: indica warning di tipo deprecated
- unchecked: warning generici
![[Pasted image 20241125183842.png|400]]
![[Pasted image 20241125183913.png|400]]
ESEMPIO FATTO BENE
![[Pasted image 20241125184055.png|600]]
#### 4.@SAFEVARARGS
[[LINGUAGGI LEZ.6+7#Passare un numero variabile di argomenti|se non ti ricordi varargs]]
Quando viene utilizzato questo tipo di annotazione, gli avvisi non controllati relativi all'utilizzo varargs vengono soppressi.

### ANNOTAZIONI CHE SI APPLICANO AD ALTRE ANNOTAZIONI
da cui nasce il termine <font color="#ff0000">meta annotazioni</font>
- sono definite nel pacchetto `java.lang.annotation`

ESEMPI:
#### 1.@RETENTION
Specifica come una determinata annotazione viene salvata in memoria:
questi sono i 3 casi:
![[Pasted image 20241125185533.png]]
#### 2.@DOCUMENTED
indica che la tua annotazione deve essere documentata con lo strumento JavaDoc
#### 3.@TARGET
specifica la tua annotazione dove può essere messa es: solo sui metodi, solo sui package...
![[Pasted image 20241125190028.png|400]]

#### 4.@INHERITED
Indica che un'annotazione applicata a una classe è ereditata dalle sottoclassi, funziona solo per annotazioni applicate alle classi

#### 5.@REPEATABLE
Serve per creare il contenitore delle varie annotazioni ripetute
### Le type annotations
le type annotations servono per annotare determinate cose sui dati per migliorare la programmazione in java.
Se ad esempio voglio che una variabile String non assuma mai null creo un plug-in che mi controlla il NullPointerException, ovvero il gestore di quando ho un null
e faccio in modo di attaccare questo plug-in con una annotazione alla variabile
![[Pasted image 20241125191526.png]]


### Annotazioni Ripetibili
- sono real-time
- servono per fare azioni ripetibili
tipo :
#### 1.@SCHEDULE
Serve per eseguire un metodo in momenti diversi
![[Pasted image 20241125192015.png|400]]
#### 2.@Alert
Usato ad esempio per definire ruoli
![[Pasted image 20241125192416.png|500]]
#### COME SI IMPLEMENTANO QUESTI REPEATABLE?
Utilizzo il @Repeatable così da specificare che la struttura che sto creando per le annotazioni può essere ripetuta.
mi creo il contenitore per inserire l'oggetto schedule
![[Pasted image 20241125193033.png|500]]
![[Pasted image 20241125193315.png]]

#### Reflection API
reflection gestisce le ripetizioni prendendo i contenitore e lo gestisce

### STORIA SU JAVA
Necessità di astrarre la programmazione
Tutti gli oggetti sono passati per riferimento quindi prevedono puntatori ma non visibili perfettamente 
Java è una implementazione completa della programmazione a oggetti ad alto livello
### Java e la sua portabilità
In C il codice andava compilato e il compilatore differiva in base all'hardware e al s.o.
Java ha una virtual machine che converte il linguaggio scritto in java nel linguaggio della macchina che usiamo, ciò consente di non dover riscrivere i codici per macchine diverse
>[!cit] write once, run everywhere

È portabile
Java si dice un linguaggio High performance per l'uomo, C viene eseguito più velocemente ma è più complesso
La sicurezza di Java più o meno dipende dalla macchina virtuale e basta
Java si utilizza anche per sviluppare app web con applet
>[!question]- Cosa è un applet?
>Piccolo programma che viene eseguito su un browser web per fornire interazioni, sostituito poi da JavaScript e altre cose

Java oggigiorno viene principalmente utilizzato in ambienti back-end e non front-end
#### Come funziona la Java Virtual Machine
Ci sono due cose principali
- il codice sorgente(il codice in Java) e il file sarà contraddistinto in .Java
- il bytecode è il risultato dell'operazione di compilazione fatta da Javac il file sarà in .class 
La jvm traduce in real-time il bytecode(.class) in linguaggio macchina
![[Pasted image 20241017181737.jpg|400]]
![[Pasted image 20241017181748.jpg|400]]
### API(Application Programming Interface) IN JAVA
È un insieme di regole e meccanismi come classi, oggetti e metodi che danno funzionalità aggiuntive al programma in Java
Come ad esempio java.net che aggiunge funzioni per la gestione delle reti
![[Pasted image 20241017175333.jpg|400]]
### Cose importanti nelle tecnologie  Java
- avere strumenti  di sviluppo come l'eseguibile Java e Javac ovvero il compilatore di bytecode e anche javaDOC(prende I commenti che fai in Java e genera del codice in HTML per visualizzare ciò che commenti)
- Tool per le interfacce come JavaFX e Swing
# COSE TANGIBILI
## esempio hello world
``` Java
class Helloworld{
	public static void main(String[] args){
		System.out.println("Hello World");
	}
}
```
- Dichiarazione della Classe che avrà il compito di svolgere il main e deve avere lo stesso nome del file
- ha un metodo pubblico, statico e di tipo void e si deve chiamare main
- in questo main è previsto un passaggio di parametri 
- stiamo passando $string[] args$  ovvero un array di stringhe che prende le info dalla linea di comando

Se esegui questo programma con:
```
java MyProgram uno due tre

```
gli args saranno rispettivamente
```
Argomento 0: uno
Argomento 1: due
Argomento 2: tre

```

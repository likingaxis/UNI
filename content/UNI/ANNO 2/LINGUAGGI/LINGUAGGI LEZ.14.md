#### Le Collections sono un **framework** che racchiudono diverse strutture dati
>[!info] Per framework si intende un insieme di strumenti, codici librerie e funzionalità già preparate

apportano a dei miglioramenti
- aumentano l'efficienza e la qualità del codice e delle sue implementazioni
- riduce la fatica nel creare nuove API
Le collections sono un framework che hanno una struttura interna con delle interfacce come la collection
#### La gerarchia delle interfacce di collection
![[Pasted image 20241214170809.png]]

| **Tipo**  | **Cosa fa**                                                                                    | **Esempio**                   |
| --------- | ---------------------------------------------------------------------------------------------- | ----------------------------- |
| **List**  | Una lista ordinata di elementi. Può avere duplicati.                                           | `ArrayList`, `LinkedList`     |
| **Set**   | Un insieme di elementi **unici**, senza duplicati.                                             | `HashSet`, `TreeSet`          |
| **Queue** | Una coda FIFO (First In, First Out).                                                           | `LinkedList`, `PriorityQueue` |
| **Deque** | Una coda dove puoi aggiungere/rimuovere elementi sia dalla testa che dalla coda.               | `ArrayDeque`                  |
| **Map**   | Una struttura **chiave-valore**, dove ogni chiave è unica e associata a un valore. (dizionari) | `HashMap`, `TreeMap`          |

#### un esempio di ArrayList e Supporta i Generics
```java
List<String> list = new ArrayList<>();
```
###### Che operazioni posso fare su una lista?
- add facendo `list.add("Apple");`
- remove `list.remove("Banana");`
	- per eliminare a un indice `list.remove(1);`
	- `list.remove(Integer.valueOf(1)); // Rimuove il numero 1`
- posso usare strumenti di iterazione(lo vedremo tra poco)

### Diverse Operazioni che iterano sulle Collection
#### 1. Le aggregate operations
Sostanzialmente uso uno `stream` che mi scorre la sequenza della collection e poi ci applico dei
- filter
- map
- foreach
per effettuare delle funzionalità specifiche di ricerca 
###### Esempio
```java
myShapesCollection.Stream()
    .filter(e -> e.getColor() == Color.RED)  //uso una lambda expression
    .forEach(e -> System.out.println(e.getName()));
```

##### Lambda expression
uso `e` come variabile temporale che assume prima il primo elemento poi il secondo ecc...
pongo una condizione sull'elemento 
forEach poi esegue un'azione su ogni elemento filtrato
`-> serve per indicare che prima della freccia ho gli attributi e dopo la condizione`
>[!bug] gli aggregator non ti consentono di modificare la collezione ma solo di giocarci su
#### 2. for -each
```java
for (Object o : collection)
    System.out.println(o);
```

>[!bug] pure con il foreach stessa cosa

#### 3. iterators
###### **Metodi principali dell'`Iterator`**

| **Metodo**  | **Descrizione**                                                           |
| ----------- | ------------------------------------------------------------------------- |
| `hasNext()` | Restituisce `true` se c'è un altro elemento nella collezione da scorrere. |
| `next()`    | Restituisce l'elemento successivo nella collezione.                       |
| `remove()`  | Rimuove l'elemento corrente dalla collezione in modo sicuro (opzionale).  |


```java
List<String> list = new ArrayList<>(List.of("Apple", "Banana", "Cherry"));

Iterator<String> iterator = list.iterator();

while (iterator.hasNext()) {
    String fruit = iterator.next();
    if (fruit.equals("Banana")) {
        iterator.remove(); // Rimuove "Banana" dalla collezione
    }
}

System.out.println(list); // Output: [Apple, Cherry]

```

### Bulk operations

| **Metodo**        | **Cosa fa**                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **`containsAll`** | Ritorna `true` se tutti gli elementi della collezione specificata sono presenti nella collezione presa in considerazione. |
| **`addAll`**      | Aggiunge tutti gli elementi di un'altra collezione alla collezione target.                                                |
| **`removeAll`**   | Rimuove dalla collezione target tutti gli elementi presenti in un'altra collezione.                                       |
| **`retainAll`**   | Mantiene solo gli elementi comuni tra la collezione target e quella specificata.                                          |
| **`clear`**       | Rimuove **tutti** gli elementi dalla collezione target.                                                                   |

>[!info] versioni con e senza eccezioni
>
>Per ogni struttura abbiamo versioni con e senza eccezioni perché ci sta chi dice che se tanto la 
>struttura la implementi bene nel codice a nessuno importa
>- le eccezioni ci sono comunque ma una in runtime

###### Differenza tra Integer e int
Int essendo un dato primitivo non è un oggetto, per usarlo come oggetto si sono inventati integer
- integer è un wrap dell' int ed è sottoclasse di number

#### Operatore ternario
`condizione ? valore1 : valore2`

`(x > 5) ? "Maggiore di 5" : "Minore o uguale a 5";`
se è True butta fuori la cosa a sx se é False la cosa a dx

#### Deque
- first indica il primo inserito
- last indica l'ultimo inserito

| **Tipo di Operazione** | **Elemento Iniziale (Inizio del Deque)** | **Elemento Finale (Fine del Deque)** |
| ---------------------- | ---------------------------------------- | ------------------------------------ |
| **Inserimento**        | `addFirst(e)`                            | `addLast(e)`                         |
| **Rimozione**          | `removeFirst()`                          | `removeLast()`                       |
| **Esaminazione**       | `getFirst()`                             | `getLast()`                          |
#### Le map(sono tipo i dizionari)

##### Le varie implementazioni

| **Implementazione** | **Caratteristiche principali**                                                       | **Quando usarla**                                                                  |
| ------------------- | ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------- |
| **`HashMap`**       | - Usa una tabella hash.                                                              | Quando serve alta velocità per inserimento, ricerca e rimozione.                   |
|                     | - Non garantisce ordine.                                                             |                                                                                    |
| **`LinkedHashMap`** | - Estende `HashMap`.                                                                 | Quando serve mantenere l'ordine di inserimento delle coppie chiave-valore.         |
|                     | - Mantiene l'ordine di inserimento.                                                  |                                                                                    |
| **`TreeMap`**       | - Implementa una mappa ordinata (usando un albero rosso-nero).                       | Quando serve un ordine naturale delle chiavi o un ordine personalizzato.           |
|                     | - Le chiavi sono ordinate in modo naturale o tramite un `Comparator` personalizzato. |                                                                                    |
| **`Hashtable`**     | - Simile a `HashMap` ma sincronizzata (thread-safe).                                 | Quando serve una mappa sincronizzata (ma è meno usata nelle applicazioni moderne). |


```java
Map<String, Integer> map = new HashMap<>();
map.put("Apple", 1);
map.put("Banana", 2);
System.out.println(map.get("Apple")); // Output: 1
System.out.println(map.keySet());     // Output: [Apple, Banana]
```

##### Metodi delle map

| **Metodo**           | **Descrizione**                                                             |
|-----------------------|-----------------------------------------------------------------------------|
| `put(K key, V value)` | Inserisce o aggiorna un valore associato alla chiave specificata.          |
| `get(K key)`          | Restituisce il valore associato alla chiave specificata, o `null` se non esiste. |
| `remove(K key)`       | Rimuove la chiave e il valore associato.                                   |
| `containsKey(K key)`  | Restituisce `true` se la chiave esiste nella mappa.                        |
| `containsValue(V value)` | Restituisce `true` se il valore esiste nella mappa.                    |
| `keySet()`            | Restituisce un `Set` di tutte le chiavi presenti nella mappa.              |
| `values()`            | Restituisce una `Collection` di tutti i valori presenti nella mappa.       |
| `entrySet()`          | Restituisce un `Set` di tutte le coppie chiave-valore come oggetti `Map.Entry`. |
| `size()`              | Restituisce il numero di coppie chiave-valore nella mappa.                 |
| `isEmpty()`           | Restituisce `true` se la mappa è vuota.                                    |
| `clear()`             | Rimuove tutte le coppie chiave-valore dalla mappa.                         |

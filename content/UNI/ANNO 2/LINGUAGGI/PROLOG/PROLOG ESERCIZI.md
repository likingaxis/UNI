E1. Aggiungi altri fatti alla famiglia, ad esempio: padre(anna, marco)., e verifica con query chi sono i nonni di marco. 

E2. Definisci un predicato madre/2 e prova a creare la regola nonna/2. 

E3. Query: trova tutti i padri, e tutti i figli di gianni. 

E4. Prova a chiedere a Prolog: ?- padre(X, anna). → chi è X? 

Lezione 15 settembre – Liste e ricorsione 

E5. Scrivi un predicato my_length/2 e testalo con: ?- my_length([1,2,3,4], N). 

E6. Scrivi un predicato my_member/2 e verifica se c è membro di [a,b,c,d]. 

E7. Implementa somma_lista/2 e prova con ?- somma_lista([5,7,2], S).. 

E8. Implementa conta_occorrenze/3 e trova quante volte a appare in [a,b,a,c,a].  


Lezione 16 settembre – Strutture e termini complessi

E9. Usa stessa_funzione/2 e chiedi: ?- stessa_funzione(mangia(cane,osso), mangia(gatto,pesce)). 

E10. Costruisci un albero binario con almeno 5 nodi e verifica con conta_nodi/2 quanti nodi ci sono. 

E11. Prova foglia/1 con più nodi diversi: uno con figli e uno senza. 

E12. Scrivi stessa_struttura/2 e confronta due alberi con stessa forma ma valori diversi.
```mysql
CREATE DATABASE progetto_basi;
USE progetto_basi;
create table SEDE_AMA(
    codice_sede INT AUTO_INCREMENT PRIMARY KEY,
    indirizzo VARCHAR(100) NOT NULL,
    cap SMALLINT NOT NULL
);
create table CLIENTE(
    codice_fiscale VARCHAR(16) PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cognome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    password VARCHAR(64) NOT NULL,
    numero_telefono INT NOT NULL,
    indirizzo VARCHAR(100),
    cap SMALLINT,
    token_spid VARCHAR(24),
    data_nascita DATE NOT NULL
);

create table LISTA_CAP(
    codice_sede INT,
    CAP SMALLINT,
    PRIMARY KEY(codice_sede, CAP),
    FOREIGN KEY(codice_sede) REFERENCES SEDE_AMA(codice_sede)
);


create table LAVORATORE(
    CID_lavoratore INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cognome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    password VARCHAR(64) NOT NULL,
    data_nascita DATE NOT NULL,
    ruolo ENUM('in_sede', 'corriere')
);

create table PRENOTAZIONE(
    codice_prenotazione INT AUTO_INCREMENT PRIMARY KEY,
    foto TEXT NOT NULL,
    descrizione TEXT,
    tipologia_servizio VARCHAR(100) NOT NULL,
    data_prenotazione DATE NOT NULL,
    orario_prenotazione TIME NOT NULL,
    stato_prenotazione VARCHAR(100) NOT NULL,
    costo_prenotazione DECIMAL(8,2) NOT NULL,
    codice_fiscale VARCHAR(16) NOT NULL,
    codice_sede INT NOT NULL,
    CID_lavoratore INT NOT NULL,
    FOREIGN KEY (codice_fiscale) REFERENCES CLIENTE(codice_fiscale),
    FOREIGN KEY (codice_sede) REFERENCES SEDE_AMA(codice_sede),
    FOREIGN KEY (CID_lavoratore) REFERENCES LAVORATORE(CID_lavoratore)
);

create table VALUTAZIONE(
    codice_prenotazione INT PRIMARY KEY,
    voto TINYINT NOT NULL,
    CHECK (voto BETWEEN 1 AND 5),
    commento VARCHAR(200),
    FOREIGN KEY(codice_prenotazione) REFERENCES PRENOTAZIONE(codice_prenotazione)
);

create table VEICOLO(
    targa VARCHAR(7) PRIMARY KEY,
    tipologia VARCHAR(30),
    CID_lavoratore INT,
    carico_massimo DECIMAL(8,2),
    stato ENUM ('disponibile','occupato','manutenzione'),
    FOREIGN KEY (CID_lavoratore) REFERENCES LAVORATORE(CID_lavoratore)
);

create table TURNO(
    id_turno INT AUTO_INCREMENT PRIMARY KEY,
    data_turno DATE NOT NULL,
    orario_inizio TIME NOT NULL,
    orario_fine TIME NOT NULL,
    pausa_inizio TIME NOT NULL,
    pausa_fine TIME NOT NULL
);

create table TURNO_SETTIMANALE(
    CID_lavoratore INT,
    id_turno INT,
    PRIMARY KEY(CID_lavoratore, id_turno),
    FOREIGN KEY (CID_lavoratore) REFERENCES LAVORATORE(CID_lavoratore),
    FOREIGN KEY (id_turno) REFERENCES TURNO(id_turno)
);

create table ORARIO(
    id_orario INT AUTO_INCREMENT PRIMARY KEY,
    orario_inizio TIME NOT NULL,
    orario_fine TIME NOT NULL,
    inizio_pausa TIME NOT NULL,
    fine_pausa TIME NOT NULL,
    data DATE NOT NULL
);

create table ORARIO_SETTIMANALE(
    id_orario INT,
    codice_sede INT,
    PRIMARY KEY(id_orario,codice_sede),
    FOREIGN KEY (id_orario) REFERENCES ORARIO(id_orario),
    FOREIGN KEY (codice_sede) REFERENCES SEDE_AMA(codice_sede)
);
```


#### Query
```mysql
INSERT INTO TURNO(data_turno, orario_inizio, orario_fine, pausa_inizio, pausa_fine)
VALUES ('2025-06-09', '08:00', '18:00', '12:00', '13:00'),
	   ('2025-06-10', '08:30', '17:30', '12:00', '13:00'),
       ('2025-06-11', '9:30', '17:30', '12:00', '14:00');


INSERT INTO SEDE_AMA(indirizzo,cap)
VALUES('Via Calderon de la Barca 87',00142),
      ('Via del Verano 74',00185),
      ('Via Capo d’Africa 23B',00184);


INSERT INTO CLIENTE
VALUES ('DSNFR1DVG810JDED', 'Paolo', 'Rossi', 'paolorossi@gmail.com', 'Paol.1456', 333567541, 'Via dei Corazzieri 110', 00143, 'A7X9F2KD3LQ8Z1MV5T6W4B0J', '1998-09-06'),         
	   ('RSSMRA79P15H501T', 'Maria', 'Rossi', 'maria.rossi@example.com', 'Mari@2024', 328456789, 'Via Appia Nuova 200', 00179, 'L9X3C7DMT0WJ8ZQP5N2R6KAY', '1979-03-15'),
	   ('BNCLGU88S10F205K', 'Luigi', 'Bianchi', 'luigi.bianchi@email.com', 'Luig#1988', 347112233, 'Viale Trastevere 50', 00153, 'Z4E1W8NRK6MP3TQX9V7JB2YD', '1988-11-10'),
	   ('VRDGPP95L20C351U', 'Giuseppe', 'Verdi', 'giuseppe.verdi@demo.it', 'Gius$1995', 339998877, 'Piazza Bologna 10', 00162, 'Q2K7LPX43JM9AHYTF6WDEN8Z', '1995-07-20');


INSERT INTO LISTA_CAP (codice_sede, CAP)
VALUES (1, 00142),
       (1, 00143),
       (2, 00185),
       (3, 00184);


INSERT INTO LAVORATORE (nome, cognome, email, password, data_nascita, ruolo) VALUES ('Luca', 'Neri', 'luca.neri@ama.it', 'X8t9bP2q', '1985-05-10', 'corriere'), ('Elena', 'Rizzo', 'elena.rizzo@ama.it', 'aD4r9T6z', '1992-07-15', 'in_sede'), ('Marco', 'Gallo', 'marco.gallo@ama.it', 'P3kLm8vQ', '1988-10-22', 'corriere');
    

   
INSERT INTO PRENOTAZIONE (foto, descrizione, tipologia_servizio, data_prenotazione, orario_prenotazione, stato_prenotazione, costo_prenotazione, codice_fiscale, codice_sede, CID_lavoratore) 
VALUES ('foto1.jpg', 'Divano a 3 posti', 'ritiro a domicilio', '2025-06-12', '09:00', 'attiva', 35.00, 'RSSMRA79P15H501T', 1, 1), 
       ('foto2.jpg', 'Lavatrice vecchia', 'ritiro a domicilio', '2025-06-13', '10:00', 'completata', 40.00, 'BNCLGU88S10F205K', 2, 3), 
	   ('foto3.jpg', 'Materasso matrimoniale', 'consegna in sede', '2025-06-14', '11:00', 'attiva', 0.00, 'VRDGPP95L20C351U', 3, 2);


INSERT INTO VEICOLO (targa, tipologia, CID_lavoratore, carico_massimo, stato)
VALUES 
('AB123CD', 'Furgone', 1, 1200.50, 'disponibile'),
('EF456GH', 'Camioncino', 3, 1500.00, 'occupato'),
('IJ789KL', 'Furgone', NULL, 1100.75, 'manutenzione');

INSERT INTO VALUTAZIONE (codice_prenotazione, voto, commento)
VALUES 
(2, 5, 'Tutto perfetto');

INSERT INTO TURNO_SETTIMANALE (CID_lavoratore, id_turno)
VALUES 
(1, 1),
(2, 2),
(3, 3);

INSERT INTO ORARIO(orario_inizio,orario_fine,inizio_pausa,fine_pausa,data)
VALUES ('08:00','18:00','12:00','13:00','2025-06-09'),
        ('08:00','18:00','12:00','13:00','2025-06-10'),
        ('08:00','18:00','12:00','13:00','2025-06-11');
        
INSERT INTO ORARIO_SETTIMANALE (id_orario, codice_sede)
VALUES 
(1, 1),
(2, 2),
(3, 3);

SELECT * FROM TURNO;
SELECT * FROM CLIENTE;
SELECT * FROM SEDE_AMA;
```

INDICI
```sql
CREATE INDEX idx_prenotazione_cliente ON PRENOTAZIONE(codice_fiscale);
CREATE INDEX idx_prenotazione_lavoratore ON PRENOTAZIONE(CID_lavoratore);
CREATE INDEX idx_prenotazione_sede ON PRENOTAZIONE(codice_sede);

CREATE INDEX idx_cliente_email ON CLIENTE(email);
CREATE INDEX idx_cliente_telefono ON CLIENTE(numero_telefono);

CREATE INDEX idx_veicolo_stato ON VEICOLO(stato);

CREATE INDEX idx_lavoratore_ruolo ON LAVORATORE(ruolo);
```

IDEE VISTE
- **VistaPrenotazioniClienti**  
    - Mostra tutte le prenotazioni effettuate con i dati anagrafici dei clienti (nome, cognome, email).
```sql
CREATE VIEW VistaPrenotazioniClienti AS
SELECT C.nome,C.cognome,C.email 
FROM
 PRENOTAZIONE P JOIN CLIENTE C ON P.codice_fiscale=C.codice_fiscale;
```

- **VistaPrenotazioniCompletate**  
    - Elenco delle prenotazioni con stato "completata", includendo eventuali valutazioni.
```sql
CREATE VIEW VistaPrenotazioniCompletate AS
	SELECT P.*, 
	       V.voto,
	       V.commento
	FROM PRENOTAZIONE P 
	LEFT JOIN VALUTAZIONE V ON P.codice_prenotazione = V.codice_prenotazione
    WHERE P.stato_prenotazione = 'completata';
```

- **VistaDisponibilitaVeicoli**  
    - Elenco dei veicoli attualmente disponibili, con informazioni sull’autista assegnato (se presente).
```sql
CREATE VIEW VistaDisponibilitaVeicoli AS
	SELECT V.*,
		   L.nome,
           L.cognome,
           L.ruolo
    FROM VEICOLO V 
    LEFT JOIN LAVORATORE L ON V.CID_lavoratore = L.CID_lavoratore
    WHERE V.stato = 'disponibile';
```

- **VistaOrariSede**  
    - Raccoglie gli orari settimanali associati a ciascuna sede AMA, per facilitarne la consultazione.
```sql
CREATE VIEW VistaOrariSede AS
	SELECT S.*,
           O.*
    FROM ORARIO_SETTIMANALE OS
    JOIN SEDE_AMA S ON OS.codice_sede = S.codice_sede
    JOIN ORARIO O ON OS.id_orario = O.id_orario;
```

- **VistaTurniLavoratori**  
    - Mostra i turni assegnati a ciascun lavoratore, con date e fasce orarie.
```sql
CREATE VIEW VistaTurniLavoratori AS
	SELECT L.*,
           T.*
    FROM TURNO_SETTIMANALE TS
    JOIN LAVORATORE L ON L.CID_lavoratore = TS.CID_lavoratore
    JOIN TURNO T ON T.id_turno = TS.id_turno;
```

- **VistaClientiAttivi**  
    - Elenco dei clienti che hanno effettuato almeno una prenotazione negli ultimi 30 giorni.
```sql
CREATE VIEW VistaClientiAttivi AS
	SELECT * 
	FROM CLIENTE C 
	JOIN PRENOTAZIONE P ON C.codice_fiscale = P.codice_fiscale
    WHERE P.data_prenotazione >= CURDATE() - INTERVAL 30 DAY; 
```

- **VistaPrenotazioniPerCAP**  
    - Restituisce le quantità di prenotazioni suddivise per CAP dei clienti diversi, utile per analisi geografiche.
```sql
CREATE VIEW VistaPrenotazioniPerCAP AS
	SELECT C.cap, COUNT(DISTINCT C.codice_fiscale) as conta_cap
	FROM CLIENTE C 
	JOIN PRENOTAZIONE P ON C.codice_fiscale = P.codice_fiscale
    GROUP BY C.cap;
```

- **VistaValutazioniClienti**  
    - Mostra per ogni cliente le valutazioni lasciate, includendo commento e voto, ordinate per data.
```sql
CREATE VIEW VistaValutazioniClienti AS
	SELECT C.nome,
		   P.data_prenotazione,
		   V.voto,
		   V.commento
	FROM CLIENTE C 
	JOIN PRENOTAZIONE P ON C.codice_fiscale = P.codice_fiscale 
	JOIN VALUTAZIONE V ON P.codice_prenotazione = V.codice_prenotazione
    ORDER BY P.data_prenotazione DESC;
```

- **VistaPrenotazioniLavoratore**  
    - Elenco di tutte le prenotazioni prese in carico da ciascun lavoratore, con info sul cliente e il tipo di servizio.
```sql
CREATE VIEW VistaPrenotazioniLavoratore AS
	SELECT P.tipologia_servizio,
		   C.nome,
		   C.cognome,
		   C.numero_telefono,
		   L.nome,
		   L.cognome
	FROM PRENOTAZIONE P 
	JOIN LAVORATORE L ON P.CID_lavoratore = L.CID_lavoratore 
	JOIN CLIENTE C ON C.codice_fiscale=P.codice_fiscale
	ORDER BY L.nome;
```

- **VistaStatisticheSedi**  
    - Conta quante prenotazioni ha gestito ogni sede AMA, utile per report interni.
```sql
CREATE VIEW VistaStatisticheSedi AS
	SELECT  P.codice_sede, COUNT(P.codice_sede) as numero_prenotazioni_per_sede
	FROM PRENOTAZIONE P
	GROUP BY P.codice_sede;
```

- **VistaClientiSenzaPrenotazioni**  
    - Elenca i clienti registrati che non hanno mai effettuato una prenotazione.
```sql
CREATE VIEW VistaClientiSenzaPrenotazioni AS
	SELECT C.nome,
		   C.cognome
	FROM CLIENTE C 
	LEFT JOIN PRENOTAZIONE P ON C.codice_fiscale = P.codice_fiscale
	WHERE P.codice_prenotazione IS NULL;
```

- **VistaVeicoliAssegnati**  
    - Raccoglie tutti i veicoli con relativo lavoratore assegnato, filtrando solo quelli in uso o occupati.
```sql
CREATE VIEW VistaVeicoliAssegnati AS
	SELECT V.targa,
	       V.stato,
	       L.nome
	FROM VEICOLO V 
	JOIN LAVORATORE L ON V.cid_lavoratore = L.cid_lavoratore
	WHERE V.stato = "occupato" or V.stato = "disponibile";
```

- **VistaOrariCompletiPerSede**  
    - Combina le informazioni sugli orari, le pause e le sedi in un’unica vista consultabile.
```sql
CREATE VIEW VistaOrariCompletiPerSede AS
	SELECT O.orario_inizio,
	       O.orario_fine,
	       O.inizio_pausa,
	       O.fine_pausa,
	       S.codice_sede
	FROM SEDE_AMA S 
	JOIN ORARIO_SETTIMANALE OS ON S.codice_sede = OS.codice_sede 
	JOIN ORARIO O ON O.id_orario = OS.id_orario;
```


- **VistaPrenotazioniConFoto**  
    - Restituisce solo le prenotazioni che hanno foto associate, utile per verifiche operative.
```sql
CREATE VIEW VistaPrenotazioniConFoto AS
	SELECT P.*
	FROM PRENOTAZIONE P
	WHERE P.foto IS NOT NULL;
```

---

- **VistaPrenotazioniPerDataEOra**  
    - Mostra tutte le prenotazioni ordinate per data e orario, utile per pianificare gli interventi giornalieri.
```sql
CREATE VIEW VistaPrenotazioniPerDataOra AS
	SELECT *
	FROM PRENOTAZIONE
    ORDER BY data_prenotazione ,orario_prenotazione ;
```

- **VistaPrenotazioniConCosto**  
    - Elenco delle prenotazioni che hanno un costo maggiore di zero, quindi solo quelle a pagamento.
```sql
CREATE VIEW VistaPrenotrazioniConCosto AS
    SELECT *
    FROM PRENOTAZIONE
    WHERE PRENOTAZIONE.costo_prenotazione > 0;
```
- **VistaLavoratoriCorrieriAttivi**  
    - Mostra solo i lavoratori con ruolo "corriere" che sono attualmente associati a veicoli.
```sql 
CREATE VIEW VistaCorrieriAttivi AS
    SELECT *
    FROM LAVORATORE AS L
    WHERE L.ruolo = "corriere" AND EXISTS (
	    SELECT *
	    FROM VEICOLO AS V
	    WHERE L.CID_lavoratore = V.CID_lavoratore
	    );
```
- **VistaClientiConValutazioniAlte**  
    - Restituisce i clienti che hanno lasciato solo valutazioni pari o superiori a 4.
```sql
CREATE VIEW VistaClientiConValutazioniAlte AS
    
	SELECT *
    
	FROM CLIENTE AS C
    
	WHERE EXISTS (
		     SELECT *
		    FROM VALUTAZIONE AS V
		    JOIN PRENOTAZIONE AS P ON P. codice_prenotazione = 
		    V.codice_prenotazione
		    WHERE P.codice_fiscale = C.codice_fiscale AND V.voto >= 4);
```
- **VistaPrenotazioniConDettagliCompleti**  
    - Unisce informazioni da più tabelle (cliente, lavoratore, sede, veicolo) per ogni prenotazione.
```sql
CREATE VIEW VistaPrenotazioniConDettagliCompleti AS
    SELECT P.*, C.codice_fiscale AS codice_fiscale_cliente,
    C.numero_telefono AS numero_telefono_cliente,
    L.CID_lavoratore, L.email AS email_lavoratore, L.ruolo AS
     ruolo_lavoratore,
    V.targa AS targa_veicolo, V.tipologia AS tipologia_veicolo,
    S.indirizzo AS indirizzo_sede
    FROM PRENOTAZIONE P
    JOIN CLIENTE C ON P.codice_fiscale = C.codice_fiscale
    JOIN LAVORATORE L ON P.CID_lavoratore = L.CID_lavoratore
    JOIN SEDE_AMA S ON P.codice_sede = S.codice_sede
    JOIN VEICOLO V ON        V.CID_lavoratore = L.CID_lavoratore;
```

- **VistaSediConOrariDisponibili**  
    - Elenco delle sedi che hanno almeno un orario settimanale associato.
```sql
CREATE VIEW VistaSediConOrariDisponibili AS
	SELECT *
	FROM SEDE_AMA AS S
	WHERE EXISTS(
	    SELECT *
	    FROM ORARIO_SETTIMANALE AS O
	    WHERE O.codice_sede = S.codice_sede);
```

- **VistaVeicoliInManutenzione**  
    - Mostra i veicoli attualmente nello stato "manutenzione", con eventuale assegnazione lavoratore.
```sql
CREATE VIEW VistaVeicoliInManutenzione AS
	SELECT *
	FROM VEICOLO AS V
	WHERE V.stato = "manutenzione";
```

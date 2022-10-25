<center>Table of contents</center>

- [[#Concetti base]]
- [[#Interfaccia grafica]]
- [[#Data Manipulation Language (DML)]]
	- [[#Modifica degli schemi]]
	- [[#Transazione]]
		- [[#Transaction Isolation Levels]]
			- [[#Anomalie sui livelli]]
- [[#Data Definition Language (DDL)]]
	- [[#`SELECT`]]
	- [[#`CREATE TABLE`]]
- [[#Controllo dell'accesso]]
- [[#Esempi DDL e DML]]

# Structured Query Language (SQL)
#sql #pratica #comandi-sql #dml #ddl #transazione #sicurezza

## Concetti base

Linguaggio che contiene sia <u>DML</u>(che lavora solo su istanza) sia <u>DDL</u>.
Prima di parlare del linguaggio in sè, osserviamo i processi in esecuzione all'avvio del DBMS.

Per `psql`, parlando del comando, esistono diversi *worker* all'interno della nostra macchina linux che vengono avviati all'istanza. Il seguente comando li mostra in command line.
```
ps aux | grep mysql
```

- Il nostro server si prende la libertà di memorizzare le pagine all'interno della RAM, ma si occupa anche di possibili fallimenti, il *logging collector* è uno dei processi;
- *stats collector* ogni tanto lancia (possiamo farlo manualmente) per acquisire info sul database;
- *autovacuum launcher*, nelle mie tabelle ogni tanto faccio eliminazioni che sono logiche (alcune $n$-uple diventano invalide), aiuta a recuperare spazio liberato compattando le tabelle;
- *logical replication launcher* per replicare (come altro server) i contenuti del server corrente (master & slave);
- il *background writer* scrive pagine nella shared memory lentamente verso la memoria persistente;
- *WAL writer* che trasferisce dati WAL su memoria persistente;
- *archiver* che archivia il log eseguito.

![[Pasted image 20221007171922.png]]

## Interfaccia grafica
Per la GUI usiamo [`pgAdmin`](https://www.pgadmin.org/).
Nell'interfaccia grafica possiamo fare JOIN tra *schemi* (collezione di tabelle), possiamo vedere gli utenti con accesso al DB, possiamo vedere le relazioni. Le operazioni sono molteplici ma equivalgono alle stesse operazioni possibili tramite linea di comando (useremo soltanto da linea di comando).
>[!warning] L'interfaccia grafica a noi non interessa troppo siccome tutto quello che serve e' gia' incluso in linea di comando.


## Data Manipulation Language (DML)

### Modifica degli schemi
Usiamo `INSERT`, `DELETE`, `UPDATE` da una sola tabella per $0,1,n$ istanze, sulla base di una condizione coinvolgente anche altre relazioni.

Per <u>inserire</u> $n$-uple nello schema:
```sql
INSERT INTO nomeTabella(attributo1, attributo2, ...)
	VALUES (valore1, valore2, ...);
```

<center>oppure</center>

```sql
INSERT INTO nomeTabella(attributi)
	SELECT ();
```

Per <u>cancellarle</u>:
```sql
DELETE FROM nomeTabella
	WHERE condizione; -- senza questa, la tabella verrebbe svuotata
```
Se la politica di reazione per vincoli referenziali è specificata `CASCADE`, allora istanze di altre tabelle correlate vengono eliminate; significa che tutte le righe legate con chiave esterna, $n$-uple soddisfacenti il predicato della `DELETE`, verranno eliminate.

Per <u>modificarle</u>:
```sql
UPDATE nomeTabella
SET attributo = [ espressione | SELECT (); | NULL | DEFAULT | ... ]
	WHERE condizione;
```

### Transazione
> [!todo] Questa voce dell'argomento verra' ripresa nei capitoli successivi: non contenuta negli argomenti della prova in itinere.

$$\mathrm{A\ C\ I\ D}$$

Operazioni considerate indivisibili, corrette anche in presenza di concorrenza con effetti definitivi:
- <u>A</u>tomicità, una sola, unico oggetto, se fallisce una parte allora fallisce l'intero tentativo;
- <u>C</u>onsistenza;
- <u>I</u>solamento, transazioni iniziate nel passato e che termineranno nel futuro, non vedo mai la transazione diversa dalla mia;
- <u>D</u>urabilità.

```sql
-- per cominciare la transazione
START TRANSACTION;
-- START TRANSACTION ISOLATION LEVEL SERIALIZABLE;
-- applica la proprietà di serializzazione della teoria

-- operazioni da eseguire sulla base di dati
COMMIT WORK;
```

#### Transaction Isolation Levels
##### Anomalie sui livelli
- <u>dirty read</u>
  Una transazione legge dati scritti da una transazione concorrente non ancora committed
- <u>nonrepeatable read</u>
  Una transazione rilegge dati precedentemente letti e trova che i dati sono stati modificati da un'altra
- <u>phantom read</u>
  Una transazione riesegue una query che soddisfa una condizione di ricerca e trova che la condizione è stata modificata causa un'altra transazione
- <u>serialization anomaly</u>
  Il risultato di una transazione o gruppo, è inconsistente rispetto alle transazioni eseguite una a una
  
| Isolation Level  | Dirty Read                       | Nonrepeatable Read | Phantom Read           | Serialization Anomaly |
| ---------------- | -------------------------------- | ------------------ | ---------------------- | --------------------- |
| Read uncommitted | Allowed, not in `psql` | Possible           | Possible               | Possible              |
| Read committed   | Not possible                     | Possible           | Possible               | Possible              |
| Repeatable read  | Not possible                     | Not possible       | Allowed, not in `psql` | Possible              |
| Serializable     | Not possible                     | Not possible       | Not possible           | Not possible          | 

In `psql` possiamo richiedere uno dei quattro *isolamenti di livello*, anche se ne vengono implementati solo 3 (Read uncommitted = Read Committed).

## Data Definition Language (DDL)
### `SELECT`
[[SQL_SELECT]] -> vedere PDF associato

### `CREATE TABLE`
Per creare porzioni di schema usiamo l'istruzione `CREATE TABLE`:
- definisce uno schema di relazione e ne crea un'istanza vuota;
- specifica attributi, domini e vincoli.

```sql
CREATE TABLE [ IF NOT EXISTS ] nomeTabella (
	nomeColonna dominio [ CONSTRAINT ],
	...
);
```

Ci è possibile creare tabelle anche al risultato di un'espressione.

#### Domini elementari
- di *carattere*, singoli caratteri o stringhe;
- *numerici* esatti e approssimati;
- *data*, *ora*, *intervalli di tempo*;
- *boolean*, scritto per esteso
- *BLOB*(binary long object), *CLOB*(character long object)

Definiamo dei tipi di dato semplice con `CREATE DOMAIN`.
Ci permette di portarci dietro i vincoli ogni qual'ora ci serve scrivere lo stesso dato in più tabelle.

```sql
CREATE DOMAIN nomeDominio
	AS dominio [ CONSTRAINT ... ];
```

#### Vincoli Intrarelazionali
Chiamiamo un vincolo *intrarelazionale*, un vincolo riferito agli attributi della tabella su cui stiamo lavorando.
- `NOT NULL`, un attributo non può essere nullo;
- `UNIQUE` per creare una chiave, significa "ce ne può essere uno solo";
- `PRIMARY KEY` la chiave primaria (una soltanto, implica `NOT NULL` ma possiamo scriverlo per chiarezza);
- `CHECK` per vincolo di $n$-upla, sarebbe un *constraint*.

> [!note] Differenze tra `UNIQUE` e `PRIMARY KEY`
`UNIQUE` e `PRIMARY KEY` differiscono:
> - chiavi `UNIQUE` possono essere definite in diverso numero, mentre di `PRIMARY KEY`, associata o meno a più attributi, ne può esistere una soltanto;
> - i valori `NULL` in chiavi `UNIQUE` possono esistere, per la `PRIMARY KEY` non sono ammessi.

```sql
CREATE nomeTabella (
	-- un caso di creazione chiave primaria
	colonna1 dominio PRIMARY KEY,
	colonna2 dominio,
	colonna3 dominio,
	-- due attributi insieme formano una chiave
	UNIQUE(colonna2,colonna3),
	-- caso alternativo di creazione chiave primaria
	colonna1 dominio,
	PRIMARY KEY (colonna1) 
);
```

```sql
CREATE TABLE persone (
	...
	sesso CHAR(1) NOT NULL CHECK (sesso IN ('M','F')),
	...
);
```

#### Vincoli Interrelazionali
Riguardano la tabella che abbiamo in oggetto, ma si riferiscono anche ad altre tabelle.
Serve per indicare che un *attributo* della tabella corrente, fa *riferimento* a un altro attributo di un'altra tabella, e che quindi non c'è bisogno di riscrivere siccome già presente.

- `CHECK`;
- `REFERENCES` e `FOREIGN KEY` per definire vincoli d'integrità referenziale; sono due sintassi per scrivere la stessa cosa
	- per singoli attributi
	- su più attributi
- è possibile definire politiche di reazione alla violazione del vincolo imposto.

```sql
CREATE TABLE nomeTabella (
	-- primo modo per creare vincolo esterno
	colonna1 dominio
		REFERENCES altraTabella(colonna),
	colonna2 dominio,
	colonna3 dominio,
	-- modo alternativo di vincolo esterno
	FOREIGN KEY (colonna2,colonna3)
		REFERENCES altraTabella(colonna, colonna)
);
```

Per condizioni complicate, per vincoli, invece che `CHECK` usiamo `ASSERTION`.
In `psql` <u>non sono supportate</u>, perché non ci è garantita la loro efficienza.

La vista creata con `CREATE VIEW NomeVista`.
Sono come normali relazioni.

## Controllo dell'accesso
Controllare l'accesso di chi ha permesso per DDL.
In tutti i sistemi c'è un **amministratore** che nel caso di `psql` si chiama `postgres`. Sarebbe come l'account `root`, e può fare qualsiasi cosa sul DB. Per sicurezza è sempre meglio creare un utente che abbia privilegi minimi necessari per il suo lavoro.

L'utente amministratore `_system` può dare **privilegi** ad altri utenti:
- risorsa di riferimento;
- utente concedente la risorsa;
- l'utente ricevente la risorsa;
- l'azione che viene permessa;
- trasmissibilità del privilegio.

Tipi di privilegi:
- `INSERT` inserire dati
- `UPDATE` permette modifica del contenuto
- `DELETE` eliminare oggetti
- `SELECT` permette risorsa
- `REFERENCES` definizione di vincoli d'integrità referenziale, diritto se l'utente vuole creare chiave esterna
- `USAGE` utilizzo in una definizione

```sql
-- concessione
GRANT < Privileges | All privileges > on Resource
	TO Users [ WITH GRANT OPTION ]
	-- per specificare se altri utenti possono trasmettere il privilegio
```

```sql
-- revoca
REVOKE Privileges ON Resource FROM Users
	[ RESTRICT | CASCADE ]
	-- per specificare per altri utenti a cui trasmessi i privilegi
```

# Esempi DDL e DML
```sql
-- esempio di tabella con chiavi
CREATE TABLE Impiegati (
	matricola CHAR(6) PRIMARY KEY,
	nome VARCHAR(20) NOT NULL,
	cognome VARCHAR(20) NOT NULL,
	dipart VARCHAR(30),
	stipendio NUMERIC(9) DEFAULT 0,
	FOREIGN KEY(dipart)
		REFERENCES Dipartimenti(nomeDipart),
	UNIQUE (cognome, nome)
);
```

```sql
-- creo un dominio da riutilizzare in piu' tabelle se mi serve
CREATE DOMAIN voto
	AS SMALLINT DEFAULT NULL,
	CHECK (value >= 18 AND value <= 30)
```

```sql
-- il numero di figli di ciascun padre
SELECT Padre, COUNT(*) AS NumFigli
FROM paternita
GROUP BY Padre
```

```sql
INSERT INTO matricole
	VALUES ('Marco','Rondelli','306706');
```

```sql
DELETE FROM paternita
WHERE figlio NOT IN (SELECT nome
					 FROM persone);
```

```sql
UPDATE persone
	SET reddito = reddito * 1.1
	WHERE eta < 30
```
---
lezione: 2022-10-21
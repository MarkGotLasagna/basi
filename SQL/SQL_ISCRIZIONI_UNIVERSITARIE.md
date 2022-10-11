# Esempio SQL su tabella ISCRIZIONI UNIVERSITARIE
[[schemi_db]]
## corsi_laurea
Creiamo all'interno del nostro client `sql` un database che possiamo chiamare come vogliamo:
```sql
CREATE DATABASE universita;
USE universita;
```

Al suo interno creiamo una tabella, `corsi_laurea`, che e' la stessa tabella negli esempi SQL visti in precedenza:

![[Pasted image 20221007173155.png]]

```sql
CREATE TABLE corsi_laurea (
    codice integer NOT NULL PRIMARY KEY,
    nome VARCHAR(200) NOT NULL,
    descrizione VARCHAR(200) NOT NULL

--  alternative
--  PRIMARY KEY (codice)
--  creiamo i nostri vincoli
--  CONSTRAINT codice_non_nullo CHECK(codice IS NOT NULL)
--  CONSRAINT codice_pk PRIMARY KEY (codice)
);
```


La tabella puo' essere modificata con DML `INSERT INTO`:
```sql
INSERT INTO corsi_laurea (codice, nome, descrizione)
VALUES (1, 'Informatica', 'Corso di Laurea triennale Informatica');

INSERT INTO corsi_laurea (codice, nome, descrizione)
VALUES (2, 'Matematica', 'Corso di Laurea triennale Matematica');
```

Possiamo aggiungere specifiche alla tabella, alterandola con `ALTER TABLE`:
```sql
ALTER TABLE corsi_laurea
ADD UNIQUE(nome);
```


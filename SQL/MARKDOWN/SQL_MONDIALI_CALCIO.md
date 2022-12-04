![[Pasted image 20221103144700.png]]

```sql
CREATE TABLE nazioni (
  nome VARCHAR(200) NOT NULL,
  PRIMARY KEY (nome)
);
```

```sql
CREATE TABLE edizioni (
  anno NUMERIC(4) NOT NULL,
  nazione_ospitante VARCHAR(200) NOT NULL,
  nazione_vincitrice VARCHAR(200), -- annullabile
  PRIMARY KEY (anno),
  FOREIGN KEY (nazione_ospitante) REFERENCES nazioni(nome),
  FOREIGN KEY (nazione_vincitrice) REFERENCES nazioni(nome)
);
```

```sql
CREATE TABLE squadre (
  edizione NUMERIC(4) NOT NULL,
  nazione VARCHAR(200) NOT NULL,
  cognome_nome_allenatore VARCHAR(200)
);
```

```sql
-- Nota: si è deciso di non mettere i vincoli nella create table
-- allo scopo di mostrare l'uso del comando alter table, che consente
-- di modificare lo schema di una tabella esistente.

ALTER TABLE squadre
  ADD CONSTRAINT squadre_pkey
  PRIMARY KEY (edizione, nazione);

ALTER TABLE squadre
  ADD CONSTRAINT squadre_edizione_fkey
  FOREIGN KEY (edizione) REFERENCES edizioni(anno);

ALTER TABLE squadre
  ADD CONSTRAINT squadre_nazione_fkey
  FOREIGN KEY (nazione) REFERENCES nazioni(nome);

ALTER TABLE squadre
  ALTER COLUMN cognome_nome_allenatore
  SET NOT NULL;
```

```sql
CREATE TABLE giocatori (
  id NUMERIC(10) NOT NULL,
  cognome_nome VARCHAR(200) NOT NULL,
  anno_nascita numeric(4) NOT NULL,
  PRIMARY KEY (id)
);
```

```sql
CREATE TABLE convocati (
  squadra_edizione NUMERIC(4) NOT NULL,
  squadra_nazione VARCHAR(200) NOT NULL,
  numero_maglia INTEGER NOT NULL,
  giocatore NUMERIC(10) NOT NULL,
  PRIMARY KEY (squadra_edizione, squadra_nazione, numero_maglia),
  FOREIGN KEY (squadra_edizione, squadra_nazione)
    REFERENCES squadre(edizione, nazione),
  FOREIGN KEY (giocatore) REFERENCES giocatori(id)
);
```
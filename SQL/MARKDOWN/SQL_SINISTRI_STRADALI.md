![[Pasted image 20221019115031.png]]

```sql
CREATE TABLE assicurazioni (
	codice NUMERIC NOT NULL,
	nome VARCHAR(100) NOT NULL,
	sede VARCHAR(200) NOT NULL,
	PRIMARY KEY(codice)
);

CREATE TABLE proprietari (
	codice_fiscale CHAR(16) NOT NULL PRIMARY KEY,
	nome VARCHAR(100) NOT NULL,
	residenza VARCHAR(100) NOT NULL
);

CREATE TABLE auto (
	targa VARCHAR(15) NOT NULL PRIMARY KEY,
	marca VARCHAR(20) NOT NULL,
	cilindrata INTEGER NOT NULL,
	proprietario CHAR(16) NOT NULL
		REFERENCES proprietari(codice_fiscale),
	assicurazione NUMERIC NOT NULL,
	FOREIGN KEY (assicurazione) REFERENCES assicurazioni(codice)
);

CREATE TABLE sinistri (
	codice NUMERIC NOT NULL PRIMARY KEY,
	luogo VARCHAR(200) NOT NULL,
	data DATE NOT NULL
);

CREATE TABLE auto_coinvolte (
	sinistro NUMERIC NOT NULL REFERENCES sinistri(codice),
	auto VARCHAR(15) NOT NULL REFERENCES auto(targa),
	importo_danno NUMERIC(10,2) -- annullabile 12 cifre, 2 dopo virgola
);
```

---

```sql
-- creare vista relazione NoSinistri che elenchi tutti i proprietari che non sono mai stati coinvolti in sinistri (con nessuna auto posseduta)
CREATE OR REPLACE VIEW no_sinistri AS
	SELECT p.*
	FROM proprietari p
	WHERE NOT EXISTS (
		SELECT *
		FROM auto_coinvolte ac, auto a
		WHERE ac.auto = a.targa
			AND a.proprietario = p.codice_fiscale
	);
```

<center> oppure </center>

```sql
CREATE OR REPLACE VIEW no_sinistri AS
	SELECT p.*
	FROM proprietari p
	WHERE p.codice_fiscale NOT IN (
		SELECT a.proprietario
		FROM auto_coinvolte ac, auto a
		WHERE ac.auto = a.targa
	);
```

```sql
-- inserire nel DB il sinsitro di codice 1317 avvunto a Parma il 17 giugno 2013 che ha coinvolto tutte le auto la cui targa contiene la stringa 13 o la stringa 17 con danno non ancora quantificato
BEGIN TRANSACTION;

INSERT INTO sinistri
	VALUES(1317, 'Parma', '2013-06-17');

INSERT INTO auto_coinvolte (sinistro, auto, importo_danno)
	SELECT 1317, targa, NULL
	FROM auto A
	WHERE targa LIKE '%13%' OR targa LIKE '%17%'

COMMIT WORK;
```

```sql
-- calcolare per ogni assicurazione l'importo totale dei danni riportati dalle auto assicurate nel corso dell'anno 2013
SELECT ASS.codice, ASS.nome, SUM(AC.importo_danno)
FROM assicurazione ASS, auto A, sinsitri S, auto_coinvolte AC 
WHERE ASS.codice = A.assicurazione
	AND A.targa = AC.auto
	AND S.codice = AC.sinistro
	-- AND EXTRACT(year FROM S.data) = 2013
	AND estrai_anno(S.data) = 2013
GROUP BY ASS.codice, ASS.nome
```

```sql
-- estrarre luogo, codice, data dei sintri che hanno coinvolto almeno 3 auto ciascuna delle quali hanno danno superiore a 2500EUR
SELECT S.codice, S.luogo, S.data
FROM sinistri S, auto_coinvolte AC
WHERE S.codice = AC.sinistro
	AND AC.importo_danno > 2500
	-- AND AC.importo_danno IS NOT NULL -> ridondante
GROUP BY S.codice, S.luogo, S.data
HAVING COUNT(*) > 2
```

```sql
-- calcolare per ogni marca di auto il numero di auto distinte coinvolte in sinistri
SELECT A.marca, COUNT(DISTINCT A.targa)
FROM auto_coinvolte AC INNER JOIN auto A ON AC.auto = A.targa -- JOIN ESPLICITO
GROUP BY A.marca
```

```
-- Usando l'algebra relazionale estrarre i proprietari di almeno due automezzi che sono assicurati con compagnie distinte e sono stati entrambi coinvolti in sinistri
```

$botto1 := P\ \mathrm{JOIN}_{P.codice_fiscale = A.proprietario}\ A\ \mathrm{JOIN}_{A.targa = AC.auto}$

$botto2 := botto1$

$\mathrm{PROJ}_{botto1.codice_fiscale}(botto1$
$\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \mathrm{JOIN}_{botto1.codice_fiscale = botto2.codice_fiscale\ AND}$ $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ _{botto1.targa\ =! botto2.targa\ AND}$
$\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ _{\ botto1.assicurazione\ =!\ botto2.assicurazione}$
$\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ botto2)$

![[Pasted image 20221103145705.png]]

```sql
-- QUERY RICORSIVE

CREATE TABLE voli (
	partenza varchar,
	arrivo varchar 
);

INSERT INTO voli VALUES ('Roma', 'Milano');
INSERT INTO voli VALUES ('Milano', 'Parigi');
INSERT INTO voli VALUES ('Roma', 'Cagliari');
INSERT INTO voli VALUES ('Cagliari', 'Londra');
-- insert into voli values ('Londra', 'Parigi');
-- insert into voli values ('Parigi', 'Roma');
INSERT INTO voli VALUES ('Parigi', 'Londra');

WITH RECURSIVE raggiungibile(origine, destinazione) AS (
	SELECT partenza, arrivo FROM voli
	UNION DISTINCT
	SELECT r.origine, v.arrivo
	FROM raggiungibile r, voli v
	WHERE r.destinazione = v.partenza
)
SELECT * FROM raggiungibile WHERE origine = 'Roma'
```
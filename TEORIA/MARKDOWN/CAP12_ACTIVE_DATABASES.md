$\mathtt{NOTE}$
Sulle slide edizione in inglese del '99.

---
# Active Databases
I database possono reagire facendo qualcosa di più rispetto a quello richiesto dall'utente, mandano in esecuzione delle *regole di produzione* ('business rules' in marketing).

## Event-condition-action (ECA)
L'idea è che esistono dei **trigger** del paradigma **Event-codition-action (ECA)**, specificati da statement DDL `create trigger` che si attivano a un evento (come cancellazione di $n$-uple o loro aggiunta).
Con estensioni procedurali è possibile specificare politiche reattive molto intricate, molto più utile dello standard SQL che permetteva di eseguire solo istruzioni SQL nel DBMS.

## Granularity & execution mode
### Granularity
>[!note] Le azioni del trigger rimangono *atomiche*
>Una transazione atomica, seguita da un trigger, potrebbe sembrare violare la proprietà di atomicità. Questo tuttavia non succede perché la transazione e trigger, <u>insieme</u>, sono *atomiche*.

- livello di *riga*, il trigger viene attivato una volta <u>per ogni</u> tupla su cui l'evento è avvenuto
- livello di *statement*, il trigger viene attivato sullo statement SQL, indipendentemente dal numero di righe, viene <u>eseguito una volta</u>

### Execution mode
Momento in cui va in esecuzione il trigger.
Quando va in esecuzione il mio trigger rispetto la transazione?
- *immediate*, nel momento in cui si ha l'evento;
- *deferred* soltanto se facciamo il commit (maggior parte dei DBMS non li supporta).

## Trigger
>[!example] sintassi in Oracle
```sql
create trigger TriggerName
	-- Mode: before, after
	-- Event: insert, update, delete
	Mode Event{, Event}
	on TargetTable
	-- Reference: introduce variabili
	[[ referencing Reference ]
		-- specifica la granularità
		[ for each row ]
		[ when SQLPredicate ]]
		-- PL/SQLBlock
```

Grazie ai trigger possiamo definire vincoli di reazione, per esempio: le asserzioni non sono presenti come operazioni in postgreSQL ma possiamo imitarle con i trigger.
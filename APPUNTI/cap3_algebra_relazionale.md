# Algebra e calcolo relazionale
#algebra-relazionale #procedurali #ridenominazione 

I linguaggi possono essere distinti in:
- *dichiarativi*, specificano le proprietà del risultato("che cosa")
	- calcolo relazionale
	- SQL
	- Query By Example (QBE)
- *procedurali*, specificano le modalità di generazione del risultato ("come")
	- **algebra relazionale**

## Algebra relazionale
Insieme di operatori:
- su relazioni
- che producono relazioni
- possono essere composti

Con l'algebra relazionale lavoriamo con tabelle/relazioni e applichiamo operatori sulle stesse per produrre altre tabelle.

### Operatori insiemistici
Le relazioni sono degli **insiemi**, con risultati relazioni.
Posso fare l'unione $\cup$ di 2 relazioni con $n$-uple di entrambe? Sì, a condizione che le 2 relazioni siano definite sullo stesso insieme di attributi (non posso fare 15 $\cup$ 5).
- *unione* $\cup$, unisce gli attributi delle tabelle, il risultato è un insieme di $n$-uple (relazione), i duplicati vengono eliminati
- *intersezione* $\cap$, con le $n$-uple uguali tra entrambe le relazioni
- *differenza* $-$

### Ridenominazione
Operatore monadico (su una tabella) che *modifica lo schema*, non l'istanza, cambiando il nome di 1 o più attributi.

> [!example] Ridenominare 2 tabelle
> L'unione tra 2 tabelle con attributi "Madre" e "Padre" non è possibile siccome il nome degli attributi è diverso, possiamo tuttavia ridenominare questi
> 
> REN<sub>genitore$\gets$padre</sub>(Paternità) $\cup$ REN<sub>genitore$\gets$madre</sub>(Maternità)

### Selezione
Operatore monadico (su una sola tabella) che produce un risultato con lo stesso schema dell'operando e contiene una *selezione* delle $n$-uple che soddisfano un *predicato* (VERO o FALSO).

$$\mathrm{SEL}_{Condizione}(\mathrm{Operando})$$
dove <sub>condizione</sub> è una espressione booleana

> [!example] Impiegati che guadagnano più di 50
> SEL<sub>stipendio > 50</sub>(Impiegati)

> [!example] Impiegati che guadagnano più di 50 e lavorano a 'Milano'
> SEL<sub>stipendio > 50 AND filiale = 'Milano'</sub>(Impiegati)

### Proiezione
Decomposizione verticale, operatore ortogonale.
Anche lui operatore monadico, parametrico.

$$\mathrm{PROJ}_{ListaAttributi}(\mathrm{Operando})$$
> [!example] Cognome e filiale di tutti gli impiegati
> PROJ<sub>cognome,nome</sub>(Impiegati)

Una proiezione contiene al più tante $n$-uple quante l'operando e può contenerne di meno. 
Se $X$ è una superchiave di $R$, allora $\mathrm{PROJ}_X(R)$ contiene esattamente tante $n$-uple quante $R$.

Possiamo usare selezione e proiezione insieme:

> [!example] Matricola e cognome degli impiegati che guadagnano più di 50
> PROJ<sub>matricola,cognome</sub>(SEL<sub>stipendio > 50</sub>(Impiegati))

Non possiamo correlare informazioni presenti in relazioni diverse, nè informazioni in $n$-upla diverse di una stessa relazione.

---
up to: 28-09
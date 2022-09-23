# Modelli logici dei dati
#modelli #modello-relazionale #relazione-mate #ennupla 
3 modelli logici tradizionali:
- gerarchico, con puntatori come un albero
- reticolare, un grafo
- *relazionale*, che è ancora oggi il più utilizzato, basato sui valori della realtà che noi vogliamo modellare

## Modello relazionale
Creato ('70) per favorire l'indipendenza dei dati rispetto la rappresentazione e ha impiegato tempo per essere adottato ('80).
Si dice relazionale perché legato al concetto matematico (non strettamente), le relazioni hanno rappresentazione tramite tabelle:
- relazione matematica
- relazione secondo modello relazionale dei dati
- *relationship*, due entità hanno un qualche collegamento, termine di riferito agli schemi ER (la chiameremo 'associazione' per evitare confusione)

L'utilità della relazione per valori è nella facilità dei collegamenti logici, rispetto a quella dei puntatori dove la confusione è facile comparire.

**Schema di relazione**
un nome $R$ con un insieme di attributi $A_n$:
$$R(A_1, \dots, A_n)$$
**Schema di base di dati**
insieme/lista di schemi di relazione:
$$R = \{R_1(X_1), \dots R_k(X_k)\}$$
**Ennupla** -> $n$-upla
su insieme di attributi $X$, è una funzione che associa a ciascun attributo $A$ in $X$ un valore nel dominio di $A$, e $t[A]$ denota il valore di $t$ su $A$.

**Base di dati**
insieme di relazioni:
$$r = \{r_1, \dots, r_n\}$$


`esempio relazione su unico attributo:`

| matricola |  /   | 
| --------- | --- |
| 6554      |   /  |
| 3456      |    / |

`esempio struttura nidificata:`
Le strutture nidificate nel modello relazionale non sono consentite

| numero | data       | totale | quantità | descrizione |
| ------ | ---------- | ------ | -------- | ----------- |
| 1235   | 12/10/2002 | 39,20  | 3        | coperti     |
|        |            |        | 2        | antipasti   |
|        |            |        | 3        | primi       | 

vengono piuttosto separate in 2 tabelle

| numero | data | totale |
| ------ | ---- | ------ |
| ...    | ...  | ...    | 

| numero | quantità | descrizione |
| ------ | -------- | ----------- |
| ...    | ...      | ...         | 

Situazioni in cui i valori dell'attributo non sono specificati, possono esistere e sono normali. 

### Relazione matematica
$D_1 = \{a,b\}$
$D_2 = \{x, y, z\}$
Il prodotto cartesiano sarebbe $D_1 * D_2$
Una relazione $r \subseteq D_1 * D_2$

`esempio:` $partite \subseteq string * string * int * int$

| casa  | fuori | reticasa | retifuori |
| ----- | ----- | -------- | --------- |
| Juve  | Lazio | 3        | 1         |
| Lazio | Milan | 2        | 0         |
| Juve  | Roma  | 0        | 2         |
| Roma  | Milan | 0        | 1         |

La $n$-upla della tabella non la pensiamo come valore massimo $\infty$.

Alcune proprietà:
- non c'è ordinamento tra le $n$-uple
- le $n$-uple sono distinte
- ciascuna $n$-upla è ordinata
- la struttura è posizionale

### Tabelle e relazioni
Siccome la struttura posizionale non ci è comoda, associamo un nome unico alla tabella (*attributo*) che ne descrive il "ruolo" ('casa', 'fuori', 'reticasa', 'retifuori').

Una *tabella* rappresenta una relazione (nel modello logico relazionale teorico) dove:
- le righe sono diverse tra loro
- le intestazioni delle colonne sono diverse tra loro
- i valori di ogni colonna sono tra loro omogenei, sono valori del dominio (un numero non è una stringa)


---
up to: 23-09
last revision: 23-09
seso pazo in unipr
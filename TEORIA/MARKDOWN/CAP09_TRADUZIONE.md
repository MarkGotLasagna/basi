```toc
```
# Come tradurre lo schema E-R in schema Logico Relazionale

Le *entità* diventano delle relazioni sugli stessi attributi, le *associazioni* (non tutte) diventano tabelle/relazioni sulle entità coinvolte e se hanno degli attributi, questi vengono inseriti.

## Molti a molti ($N, N$)

![[Pasted image 20221130114844.png|450]]

I nostri ID delle relazioni, sono le *chiavi primarie* delle tabelle: nel caso sopra, `Partecipazione` diventa una *tabella* con chiavi `Matricola` e `Codice` delle relazioni a cui si associa `Impiegato` e `Progetto`.

$\mathtt{Impiegato}$ (<u>Matricola</u>, Cognome, Stipendio)
$\mathtt{Progetto}$ (<u>Codice</u>, Nome, Budget)
$\mathtt{Partecipazione}$ (<u>Matricola</u>, <u>Codice</u>, DataInizio)

Siamo felici con la traduzione?
Non proprio: vincoli di *chiave esterna* sarebbero migliori piuttosto che relazione con 2 chiavi che gia' esistono altrove, magari cambiando anche i nomi per renderli più espressivi. Inoltre, nell'associazione dal lato cardinalità $N$, non riusciamo a tenere conto delle cardinalità minime della relationship.

---

![[Pasted image 20221130115753.png|400]]

In questo caso l'associazione e' ricorsiva: fissato un prodotto abbiamo $N$ altri prodotti (`Composto`), oppure fissato un prodotto, lui è componente di altri (`Componente`).

$\mathtt{Prodotto}$ (<u>Codice</u>, Nome, Costo)
$\mathtt{Composizione}$ (<u>Composto</u>, <u>Componente</u>, Quantità)

Per scrivere che la nostra implementazione è ricorsiva, cambiamo il nome della chiave primaria di `Composizione`.

---

![[Pasted image 20221130120157.png|400]]

La traduzione segue le stesse meccaniche, solo che stavolta abbiamo una tripla di chiavi esterne.

$\mathtt{Fornitore}$ (<u>PartitaIVA</u>, Nome)
$\mathtt{Prodotto}$ (<u>Codice</u>, Genere)
$\mathtt{Dipartimento}$ (<u>Nome</u>, Telefono)
$\mathtt{Fornitura}$ (<u>Fornitore</u>, <u>Prodotto</u>, <u>Dipartimento</u>, Quantità)

## Uno a molti ($1, N$)

![[Pasted image 20221130120755.png|400]]

Per implementare la cardinalità uno a molti, un `Giocatore` non può avere più di un contratto. La relazione va forzata, uno e un solo `Contratto` dentro la relazione `Giocatore`, la cardinalità minima di 1 la imponiamo in questo modo:

$\mathtt{Giocatore}$ (<u>Cognome</u>, <u>DataNasc</u>, Ruolo, Squadra, Ingaggio)
$\mathtt{Squadra}$ (<u>Nome</u>, Città, ColoriSociali)

Quindi l'associazione viene eliminata e i nostri attributi inseriti nel lato molti `Giocatore`. Inoltre, se la cardinalità minima è:
- $0$ allora il valore nullo(\*) è *ammesso*;
- $1$ allora il valore nullo(\*) *non è ammesso*.

### Con identificatore esterno

![[Pasted image 20221130121531.png|400]]

Quando l'identificatore esterno c'è, la cardinalità massima diventa allora *uno a uno* ($1,1$), se cosi' non fosse, errori concettuali nello schema sono presenti.
Il nome dell'`Universita` entra come chiave in `Studente`.

$\mathtt{Studente}$ (<u>Matricola</u>, <u>Università</u>, Cognome, AnnoDiCorso)
$\mathtt{Universita}$ (<u>Nome</u>, Città, Indirizzo)

## Uno a uno ($1, 1$)

![[Pasted image 20221130121835.png|400]]

Come visto sopra, quando abbiamo una cardinalità massima $1$, non creiamo una tabella, ma spostiamo gli attributi in una relazione... ma su quale lo facciamo in questo caso che abbiamo in ambo lati $1$? 
Usiamo la logica che se per caso su uno dei due lati avessimo $0$, allora la traduzione sarebbe:

$\mathtt{Impiegato}$ (<u>Codice</u>, Cognome, Stipendio)
$\mathtt{Dipartimento}$ (<u>Nome</u>, Sede, Telefono, Direttore, InizioD)

E se non volessimo lo stesso `Direttore` per più `Dipartimenti`?
Codifichiamo con `UNIQUE` su `Direttore`, forzando l'associazione ad $1,1$.

![[Pasted image 20221130122406.png|400]]

# Esempio di traduzione

![[Pasted image 20221130122633.png|450]]

$\mathtt{Impiegato}$ (<u>Codice</u>, Cognome, Dipartiemento, Sede, Data\*)
$\mathtt{Dipartimento}$ (<u>Nome</u>, <u>Città</u>, Telefono, Direttore\*)
$\mathtt{Sede}$ (<u>Città</u>, Via, CAP)
$\mathtt{Progetto}$ (<u>Nome</u>, Budget)
$\mathtt{Partecipazione}$ (<u>Impiegato</u>, <u>Progetto</u>)
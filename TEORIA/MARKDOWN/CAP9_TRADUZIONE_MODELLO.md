# Tradurre che lo schema E-R in modello logico-relazionale

Le due *entità* diventano delle relazioni sugli stessi attributi, le *associazioni* (non tutte) diventano tabelle/relazioni sulle entità coinvolte e se hanno degli attributi, ce li mettiamo.

## Molti a molti
![[Pasted image 20221130114844.png|450]]
I nostri ID delle relazioni, sono le *chiavi primarie* delle tabelle, `Partecipazione` diventa una *tabella* con chiavi `Matricola` e `Codice` delle relazioni a cui si associa.

$\mathtt{Impiegato}$ (<u>Matricola</u>, Cognome, Stipendio)
$\mathtt{Progetto}$ (<u>Codice</u>, Nome, Budget)
$\mathtt{Partecipazione}$ (<u>Matricola</u>, <u>Codice</u>, DataInizio)

Siamo felici? Non proprio: mancherebbero i vincoli di chiave esterna, magari cambiando anche i nomi per renderli più espressivi.
Nell'associazione, dal lato cardinalità $N$, non riusciamo a tenere conto delle cardinalità minime della relationship.

---
Associazione ricorsiva: fissato un prodotto abbiamo $N$ altri prodotti (`composto`), oppure fissato un prodotto, lui è componente di altri (`componente`).

![[Pasted image 20221130115753.png|400]]
$\mathtt{Prodotto}$ (<u>Codice</u>, Nome, Costo)
$\mathtt{Composizione}$ (<u>Composto</u>, <u>Componente</u>, Quantità)

Per scrivere che la nostra implementazione è ricorsiva, cambiamo il nome della chiave primaria di `Composizione`.

---
Facciamo la solita traduzione, solo che abbiamo una tripla di chiavi esterne.

![[Pasted image 20221130120157.png|400]]
$\mathtt{Fornitore}$ (<u>PartitaIVA</u>, Nome)
$\mathtt{Prodotto}$ (<u>Codice</u>, Genere)
$\mathtt{Dipartimento}$ (<u>Nome</u>, Telefono)
$\mathtt{Fornitura}$ (<u>Fornitore</u>, <u>Prodotto</u>, <u>Dipartimento</u>, Quantità)

## Uno a molti
In questo caso la cosa diversa è che l'associazione è *uno a molti*.

![[Pasted image 20221130120755.png|400]]
Per implementare la cardinalità uno a molti, un giocatore non può avere più di un contratto. La relazione va forzata, uno e un solo contratto dentro la relazione `Giocatore`, la cardinalità minima di 1 la imponiamo in questo modo:

$\mathtt{Giocatore}$ (<u>Cognome</u>, <u>DataNasc</u>, Ruolo, Squadra, Ingaggio)
$\mathtt{Squadra}$ (<u>Nome</u>, Città, ColoriSociali)

Quindi l'associazione viene eliminata e i nostri attributi inseriti nel lato molti.
Inoltre, se la cardinalità minima è:
- $0$, il valore nullo è ammesso;
- $1$, il valore nullo non è ammesso.

### con identificazione esterna
Quando l'identificatore esterno c'è, la cardinalità massima è *uno a uno*, altrimenti errori concettuali sono presenti.

![[Pasted image 20221130121531.png|400]]

$\mathtt{Studente}$ (<u>Matricola</u>, <u>Università</u>, Cognome, AnnoDiCorso)
$\mathtt{Universita}$ (<u>Nome</u>, Città, Indirizzo)

## Uno a uno
Quando abbiamo una cardinalità massima 1, non creiamo una tabella, ma spostiamo gli attributi in una relazione... ma su quale lo facciamo in questo caso? Se per caso su uno dei due lati avessimo 0, allora sarebbe facile:

![[Pasted image 20221130121835.png|400]]
$\mathtt{Impiegato}$ (<u>Codice</u>, Cognome, Stipendio)
$\mathtt{Dipartimento}$ (<u>Nome</u>, Sede, Telefono, Direttore, InizioD)

E se non volessimo lo stesso direttore per più dipartimenti?
Codifichiamo con `UNIQUE` su `Direttore`, forzando l'associazione essere 1,1.

![[Pasted image 20221130122406.png|400]]

# Esempio di traduzione
![[Pasted image 20221130122633.png|450]]
$\mathtt{Impiegato}$ (<u>Codice</u>, Cognome, Dipartiemento, Sede, Data\*)
$\mathtt{Dipartimento}$ (<u>Nome</u>, <u>Città</u>, Telefono, Direttore\*)
$\mathtt{Sede}$ (<u>Città</u>, Via, CAP)
$\mathtt{Progetto}$ (<u>Nome</u>, Budget)
$\mathtt{Partecipazione}$ (<u>Impiegato</u>, <u>Progetto</u>)

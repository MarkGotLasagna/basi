# Esempi di schemi di basi di dati
> [!note]
> *pk* è <u>primary key</u>
> *fk* foreign key
> `*` indica opzionale, quindi annullabile

Per il nome delle tabelle ci concentriamo sul plurale.

## mondiali di calcio
Nazioni(<u>nome</u>)
Edizioni(<u>anno</u>, nazione_ospitante<sub>fk</sub>, nazione_vincitrice<sub>fk</sub>\*)
Squadre(<u>edizione</u><sub>fk</sub>, <u>nazione</u><sub>fk</sub>, cognome_nome_allenatore)
> insieme la chiave primaria identifica la squadra

Giocatori(<u>id</u>, cognome_nome, anno_nascita)
Convocati([<u>squadra_edizione</u>, <u>squadra_nazione</u>]<sub>fk</sub>, <u>numero_maglia</u>, giocatore<sub>fk</sub>)
> la fk si riferisce alla tabella `Squadre` e fa anche pk insieme a `numero_maglia`, `giocatore` è chiave esterna verso `Giocatori`

## sinistri stradali
Assicurazioni(<u>codice</u>, nome, sede)
Proprietari(<u>codice_fiscale</u>, nome, residenza)
Auto(<u>targa</u>, marca, cilindrata, proprietario<sub>fk</sub>, assicurazione<sub>fk</sub>)
Sinistri(<u>codice</u>, luogo, data)
AutoCoinvolte(<u>sinistro</u><sub>fk</sub>, <u>auto</u><sub>fk</sub>, importo_danno*)

## iscrizioni universitarie
Corsi_Laurea(<u>codice</u>, nome, descrizione)
Insegnamenti(<u>codice</u>, nome, crediti, ssd)
Manifesti(<u>laurea</u><sub>fk</sub>, <u>insegnamento</u><sub>fk</sub>, fondamentale*, anno_corso)
Studenti(<u>matricola</u>, nome, cognome, data_nascita)
Iscrizioni(<u>studente</u><sub>fk</sub>, <u>anno_iscrizione</u>, laurea<sub>fk</sub>, data_iscrizione, anno_corso)


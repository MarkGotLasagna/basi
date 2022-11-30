del gg. 13/06/2005

Mostrare lo schema concettuale per la base di dati di una sezione di una associazione di donatori di sangue, secondo le seguenti specifiche.

# Schema E-R passo per passo
1. Alla sezione afferiscono un certo numero di soci *donatori*; per essi si registrano il numero della tessera, il gruppo sanguigno (A+, 0+, B-, AB+, ecc.), la data delle ultime analisi di controllo, il codice fiscale, nome e cognome, data di nascita, indirizzo, nonche' telefono ed email, se disponibili.

	![[Pasted image 20221119154513.png]]

>[!note] Codificare elenco di possibilita' in schemi E-R
	>In questo caso, necessitiamo di un modo per codificare il "gruppo sanguigno": usare un attributo associato ai donatori diventerebbe sconveniente, alcune query SQL diventerebbero impossibili da realizzare.
	>
	>Ogni qual volta si presentera' un elenco di opzioni, usiamo una *entita'* per codificarle, dove il "nome" e' l'identificatore interno.
	>
	>![[Pasted image 20221119155044.png]]

> [!example] Associazione `GS` - `Donatori`
> ![[Pasted image 20221119155237.png]]

2. Un donatore puo' essere *sospeso* per un periodo determinato di tempo stabilito in base al motivo della sospensione (intervento chirurgico, terapia antibiotica, gravidanza, allattamento, ecc.).
   
	![[Pasted image 20221119155941.png]]
3. Alla sezione afferiscono un certo numero di *medici*, *infermieri* e altro *personale volontario*: per essi si devono registrare il codice fiscale, nome e cognome, indirizzo e telefono.
4. L’attivita' di donazione della sezione e' organizzata in “*giornate di donazione*”. Per ogni giornata, identificata dalla data, si registrano gli orari d'inizio e fine attivita' e il luogo.
5. Per regolamento, a ogni giornata debbono garantire la presenza un medico e tre infermieri: di questi va obbligatoriamente registrata la *partecipazione* (non interessa registrare la partecipazione di altro personale volontario).
   
	![[Pasted image 20221119160443.png]]

6. Per ogni giornata sono *convocati* (con un certo anticipo) un certo numero di donatori; di questi, a posteriori, interessera' distinguere coloro che hanno risposto alla convocazione: a tal fine, si considerano “assenti non giustificati” i convocati che non si sono presentati e neppure hanno comunicato l’impossibilita' di presentarsi. In generale, un sottoinsieme di coloro che si sono presentati ha effettuato la donazione vera e propria (perche' alcuni presenti sono considerati temporaneamente inidonei alla donazione dopo la visita medica).
	![[Pasted image 20221119162626.png|450]]
7. Le *donazioni* sono identificate da un codice; per ogni donazione si debbono registrare il peso in Kg, la pressione arteriosa (massima e minima, entrambe intere positive) e l’emoglobina del donatore (un valore tra 10.0 e 20.0), la quantita' di sangue donata (di norma 400 cc).
   
	![[Pasted image 20221119163034.png]]

# Schema E-R completo
![[Pasted image 20221119165537.png]]
## Traduzione in linguaggio logico-relazionale
$\mathtt{GS}$ (<u>Nome</u>)
$\mathtt{MotiviSospensione}$ (<u>Nome</u>, Durata)
$\mathtt{Donatori}$ (<u>Tessera</u>, CF (UNIQUE), Nome, Cognome, Email,
	GS_Nome<sub>fk</sub>, MotivoSospensione<sub>fk</sub>\*, DataInizioSospensione\*)
$\mathtt{M}$ (Volontari<sub>fk</sub>)
$\mathtt{I}$ (Volontari<sub>fk</sub>)
$\mathtt{GD}$ (<u>Data</u>, OraInizio, OraFine, 
	Medico<sub>fk</sub>, Infermiere1<sub>fk</sub>, Infermiere2<sub>fk</sub>, Infermiere3<sub>fk</sub>)
$\mathtt{Convocazioni}$ (<u>Giornata</u><sub>fk</sub>, <u>Donatore</u><sub>fk</sub>, Tipo)
$\mathtt{Donazioni}$ (<u>ID</u>, Quantità, Peso, \[Giornata, Donatore<sub>fk</sub>(Convocazioni)])
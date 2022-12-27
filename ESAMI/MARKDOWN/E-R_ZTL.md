del gg. 04/02/2008

Mostrare le schema concettuale Entita'-Relazione per (una parte de-) i dati memorizzati dal sistema informatico "Che fa, concilia?", che gestisce la rilevazione di alcune infrazioni stradali per conto di un'amministrazione cittadina. Si richiede di modellare le informazioni seguenti:

# Schema E-R passo per passo
1) Gli *automezzi*, identificati dalla targa (un codice alfanumerico di al piu' 8 caratteri), sono associati ai dati del loro unico *proprietario* (codice fiscale, cognome, nome, indirizzo).
   
   ![[Pasted image 20221226141100.png|500]]
2) Parti del territorio di competenza dell’amministrazione sono catalogate come zone a traffico limitato (*ZTL*), identificate da un codice.
3) Alcuni automezzi sono autorizzati al transito in determinate ZTL; ogni *autorizzazione* ha una data di scadenza e riguarda un solo automezzo e una sola ZTL; lo stesso automezzo puo' ottenere piu' autorizzazioni per ZTL distinte.
   
   ![[Pasted image 20221226141914.png|500]]
   > [!note] Identificatore di `AUTORIZZAZIONE`
   > Dato che nella consegna ci viene detto alcuni `AUTOMEZZI` sono *autorizzati* al transito ZTL, possiamo dedurre che l'identificatore della relazione `AUTORIZZAZIONE` sara' esterno. La deduzione viene confermata dalle cardinalita' uno-a-uno.
4) Alcuni automezzi (ad es., auto blu o auto addette al trasporto di soggetti disabili) sono forniti di “passepartout”, ovvero un’autorizzazione al transito in qualunque ZTL e che non e' soggetta a scadenza temporale. 
   $\mathtt{NOTA}$: *AS* => `A`utomezzi `S`peciali
   
   ![[Pasted image 20221226142337.png|200]]
   
5) Ogni ZTL ha alcuni punti d'ingresso, detti anche “*porte*”, presso i quali sono installati sistemi per il rilevamento fotografico degli automezzi in transito.
   
   ![[Pasted image 20221226142716.png|300]]
   > [!note] Identificatore di `PORTE`
   > Ogni `ZTL` puo' avere piu' `PORTE` a essa associata e quindi piu' codici. 
   > A una `PORTA` e' associata una sola zona `ZTL`.
6) A ogni *transito* attraverso una porta ZTL, il sistema memorizza la porta, l’istante temporale (data e ora, con precisione al secondo), il nome del file contenente l’immagine scattata, la lettura OCR della targa dell’automezzo e un ulteriore attributo che indica il successo o fallimento della procedura di lettura automatica della targa. Non vi possono essere piu' rilevazioni effettuate dalla stessa porta nel medesimo istante temporale; nel caso di fallimento della lettura OCR, la lettura targa e' comunque valorizzata con il risultato della lettura parziale.
   
   ![[Pasted image 20221226143330.png|350]]
   > [!note] Identificatore di `TRANSITO`
   > La consegna dice che non possono esserci piu' rilevazioni effettuate nel medesimo istante temporale. L'identificatore di `TRANSITO` sara' esterno, prendendo l'attributo `data_ora`.
7) Alcuni transiti sono “*identificati*”: tali transiti sono associati a un automezzo registrato nella base di dati; inoltre, la targa dell’automezzo associato coincide con il valore della lettura OCR.
8) Tra i transiti identificati si distinguono le *infrazioni*, per le quali si memorizzano la data di verbalizzazione e il numero di matricola del funzionario che ha accertato l’infrazione; inoltre, a soli fini statistici, si tiene traccia dell’esito finale della pratica (pagamento spontaneo, pagamento forzoso, ricorso vinto, ricorso perso); si noti che per alcune infrazioni l’esito finale
   
   ![[Pasted image 20221226143912.png|400]]
   > [!note] Identificatore di `IDENTIFICATI`
   > `IDENTIFICATI` contiene come chiavi esterne gli `AUTOMEZZI` e i `TRANSITI`; serve per mostrare, in un istante temporale, quali sono gli automezzi che hanno effettuato transito in `ZTL`. La relazione sara' da codificare nella traduzione.

# Schema E-R completo
![[Pasted image 20221226145335.png]]
## Traduzione in linguaggio logico-relazionale
$\mathtt{ZTL}$ (<u>codice</u>)
$\mathtt{AUTOMEZZI}$ (<u>targa</u>, passpartout (BOOLEAN), proprietario<sub>fk</sub>)
$\mathtt{AUTORIZZAZIONI}$ (<u>ZTL</u><sub>fk</sub>, <u>automezzo</u><sub>fk</sub>, data_scadenza)
$\mathtt{PORTE}$ (<u>codice</u>, <u>ZTL</u><sub>fk</sub>)
$\mathtt{PROPRIETARI}$ (<u>CF</u>, cognome, nome, indirizzo)
$\mathtt{TRANSITI}$ (<u>data_ora</u>, \[<u>codice_porta</u>, <u>ZTL</u>]<sub>fk_PORTE</sub>, file, OCR, successo)
$\mathtt{TRANS\_IDENTIFICATI}$ (\[<u>...</u>]<sub>fk_TRANSITI</sub>, automezzo<sub>fk</sub>)
$\mathtt{INFRAZIONI}$ (\[<u>...</u>]<sub>fk_TRANS_IDENTIFICATI</sub>, data, funzionario, esito\*)
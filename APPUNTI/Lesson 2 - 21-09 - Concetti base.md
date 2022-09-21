**Perché i dati**
I dati sono importanti, sono una risorsa, che però senza applicazione non servono a tanto. Conferiscono una risorsa strategica, insieme a essi servono applicazioni per implementarli.

<center> <mark> Basi di dati </mark> </center>
Un insieme organizzato di dati utilizzati per il supporto allo svolgimento delle attività di un ente, gestiti da un DBMS (database management systems). Un sistema è qualcosa di complicato, non è semplicemente uno strumento ma sono tante funzioni unite.

Le basi di dati hanno alcune caratteristiche, una di queste è che sono *grandi*, parliamo di dati transazionali, dati decisionali, dati scientifici che raggiungono centinaia di Terabyte a volte.
es. basi di dati bancari, a transazioni sicure
es. dati scientifici, astronomici

Le basi di dati devono essere *persistenti*.
Sono *condivise*, più persone-processi condividono gli stessi dati.

<center> <mark> DBMS </mark> </center>
- privatezza
- affidabilità, mettendo in gioco politiche per recuperare dati per malfunzionamenti, con gestione delle *transazioni*

<center> <mark> Transazione </mark> </center>
O vanno tutte a buon fine, oppure vengono riprese.
Un insieme *indivisibile* (<u>atomico</u>) corretto anche in presenza di concorrenza e con effetti definitivi.
es. se al nostro conto corrente fosse addebitata una somma, ma per un errore del DMBS questa venisse duplicata, non sarebbe una bella cosa
Sono <u>concorrenti</u>, 
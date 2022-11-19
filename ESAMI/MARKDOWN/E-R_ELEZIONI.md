del gg. 20/09/2016

Mostrare lo schema concettuale Entita-Relazione per il database del sistema Vota Antonio, che tiene traccia di alcune informazioni relative a una serie di elezioni. Si richiede di modellare i seguenti aspetti:

# Schema E-R passo per passo
1. ll territorio e' suddiviso in *distretti* elettorali, caratterizzati da un nome univoco; per ogni distretto si tiene traccia del numero di candidati che devono essere eletti.
    ![[Pasted image 20221119131505.png]]
2. Ogni distretto e' suddiviso in un certo numero di *sezioni* elettorali, per le quali si tiene traccia dell’indirizzo.
    ![[Pasted image 20221119131607.png]]
> [!example] Associazione "Composizione"
> ![[Pasted image 20221119131758.png]]

3. Gli *elettori*, individuati dal codice fiscale, sono caratterizzati da nome, cognome, sesso, data di nascita e data di morte (opzionale).
	![[Pasted image 20221119131837.png]]
4. Le *tessere elettorali*, individuate da un codice univoco, sono associate a un’unica sezione e un unico elettore. Per esse si registrano inoltre la data di emissione e la data di fine validita' (opzionale). Si noti che una tessera puo' essere utilizzata per piu' elezioni e un elettore puo' essere associato a piu' tessere (ad esempio, a causa di cambio di residenza con conseguente  cambio di sezione elettorale).
	![[Pasted image 20221119132447.png]]

5. Le *elezioni* si svolgono nell’arco di una sola giornata (durante la quale i seggi sono aperti dalle ore 8 alle ore 22) e sono quindi identificate dalla data di votazione. <u>Per ogni elezione</u>, si vogliono modellare le informazioni seguenti:
	1. le *liste* elettorali, identificate (all’interno di ogni elezione) da un nome e per le quali si memorizza il simbolo elettorale (il nome di un file immagine);
	![[Pasted image 20221119132754.png]]
	> [!error] Errore comune nell'uso degli identificatori
	> Per le *liste* viene esplicato che l'identificatore e' il "nome" per ogni "elezione"
	> ![[Pasted image 20221119133216.png]]

	2. le *candidature*, identificate (all’interno di ogni elezione) dall’elettore candidato; ogni candidatura e' associata aa unsolo distretto e fa parte di una sola lista elettorale;
	   ![[Pasted image 20221119133426.png]]
	3. i *voti espressi*, identificati (all’interno di ogni elezione) dalla corrispondente tessera elettorale; per essi si memorizza l’ora di voto, al fine di consentire il calcolo delle percentuali di affluenza ad orari prefissati;
	      ![[Pasted image 20221119133602.png]]
	4. le *schede scrutinate*, identificate (all’interno di ogni elezione) dalla corrispondente sezione e da un numero progressivo; si distinguono in schede *bianche*, schede *nulle* e schede *valide*; per ognuna di queste ultime, si tiene traccia della lista che ha ricevuto il voto e (opzionalmente) del candidato per il quale e' stato espresso il voto di preferenza (al piu' uno).
	    ![[Pasted image 20221119133744.png]]

# Schema E-R completo
![[Pasted image 20221119140630.png]]
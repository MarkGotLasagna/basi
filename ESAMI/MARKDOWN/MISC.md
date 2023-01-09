# Esempi estratti da prove in itinere
- Dato lo schema di relazione $R(X)$, sotto quali condizioni l’espressione dell’algebra relazionale  $\sigma_{A=B}(R)$ è ben definita, cioè non causa un errore?
  
	  Nell'algebra relazionale il simbolo $=$ indica la clausola `WHERE` di `SQL`.
	  Nessun errore si presenta fintanto che non siano presenti valori `NULL`.

- Date due tabelle con schemi $R_1(X_1)$, $R_2(X_2)$, dove $X_1 \cup X_2 = \{A\}$, sapendo che $\#(r_1) = n$ e $\#(r_2) = 0$ (cioè l’istanza di $R2$ è vuota), indicare le cardinalità delle seguenti espressioni dell’algebra relazionale:  
	- $R1 \bowtie_{NAT} R2$ (join naturale)     -> 0
	- $R1 \bowtie_{LEFT} R2$ (left outer join)  -> n
	- $R1 \bowtie_{FULL} R2$ (full outer join)  -> n + 0

- Fornire un esempio di una coppia di valori (per $A$ e $B$) per la quale i due predicati ($A \neq B)$ e $(A\ \mathtt{IS\ DISTINCT\ FROM}\ B)$ forniscono risultati diversi.
	
	Vedere tabella #NULL_VALUES 

- Date due tabelle con schemi $R_1(X_1)$, $R_2(X_2)$, sotto quali condizioni l’espressione dell’algebra relazionale $R1 \cap R2$ è ben definita, cioè non causa un errore?

	Non causa errore fintanto che le due relazioni abbiano la stessa cardinalità.

- Date due tabelle con schemi $R_1(X_1)$, $R_2(X_2)$, dove $X_1 \cap X_2 = \emptyset$, sapendo che $\#(r_1)=0$ e $\#(r_2)=n_2$ (cioè l'istanza di $R_1$ è vuota), indicare le cardinalità delle seguenti espressioni dell'algebra relazionale:
	- $R_1 \times R_2$ (prodotto cartesiano)     -> 0
	- $R_1 \bowtie_{RIGHT} R_2$ (right outer join)  -> n<sub>2</sub>
	- $R_1 \bowtie_{FULL} R_2$ (full outer join)       -> n<sub>2</sub> + 0

# Esempi estratti da prove d'esame
- Definire il concetto di granularita' dei TRIGGER.
  Quando parliamo di **granularita'**, parliamo dei momenti possibili in cui un TRIGGER puo' essere eseguito: a *livello di riga* (row-level) quando esegue per ogni tupla distinta, a *livello di statement* (statement-level) quando esegue una sola volta, in risposta all'evento che lo ha scatenato.
Operatori dell' #algebra-relazionale in sintesi.
## Unione ( $\cup$ )
$$RelazioneI\ \cup\ RelazioneII$$
![[Pasted image 20221015192008.png|350]]

## Intersezione ( $\cap$ )
$$RelazioneI\ \cap\ RelazioneII$$
![[Pasted image 20221015192252.png|350]]

## Differenza ( $-$ )
$$RelazioneI - RelazioneII$$
![[Pasted image 20221015192508.png|350]]

## Ridenominazione ( $\mathrm{REN}$ )
$$\mathrm{REN}_{NewName \gets OldName}(Relazione)$$
![[Pasted image 20221015192835.png|350]]
![[Pasted image 20221015192850.png|350]]

## Selezione ( $\mathrm{SEL}$ )
$$\mathrm{SEL}_{Condizione}(Operando)$$
![[Pasted image 20221015193445.png|350]]

## Proiezione ( $\mathrm{PROJ}$ )
$$\mathrm{PROJ}_{ListaAttributi}(Operando)$$
![[Pasted image 20221015193927.png|350]]
## Selezione + Proiezione
$$\mathrm{PROJ}_{ListaAttributi}(\mathrm{SEL}_{Condizione}(Relazione))$$
![[Pasted image 20221015193653.png|350]]

## Join Naturale ( $\mathrm{JOIN}$ )
$$R_1\ \mathrm{JOIN}\ R_2$$
![[Pasted image 20221015194534.png|350]]
## Join Esterno Left-Right-Full ( $\mathrm{JOIN}_{LEFT\ RIGHT\ FULL}$ )
$$R_1\ \mathrm{JOIN_{LEFT}}\ R_2$$
![[Pasted image 20221015195242.png|350]]
$$R_1\ \mathrm{JOIN_{RIGHT}}\ R_2$$
![[Pasted image 20221015195329.png|350]]
$$R_1\ \mathrm{JOIN_{FULL}}\ R_2$$
![[Pasted image 20221015195407.png|350]]
## Join + Proiezione
$$\mathrm{PROJ}_{ListaAttributi}(R_1\ \mathrm{JOIN}\ R_2)$$
![[Pasted image 20221015200005.png|350]]
## Theta-Join ( $\mathrm{JOIN}_{Condizione}$ )
$$R_1\ \mathrm{JOIN}_{Condizione}\ R_2$$
![[Pasted image 20221015200154.png|350]]
## Viste ( $:=$ )
$$NomeVista(ListaAttributi) := \mathrm{PROJ}_{ListaAttributi}(Operando) \dots$$
![[Pasted image 20221015200740.png|350]]
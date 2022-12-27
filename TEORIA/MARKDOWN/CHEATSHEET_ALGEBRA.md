# Operatori insiemistici
## Unione ( $\cup$ )
$$A\ \cup\ B$$
![[Pasted image 20221015192008.png|350]]

## Intersezione ( $\cap$ )
$$A\ \cap\ B$$
![[Pasted image 20221015192252.png|350]]

## Differenza ( $-$ )
$$A - B$$
![[Pasted image 20221015192508.png|350]]

# Operatori
## Ridenominazione ( $\mathrm{REN}$ | $\rho_{a/b}(R)$ )
$$\mathrm{REN}_{NewName \gets OldName}(R)$$
$$\rho_{A_1, \dotsc, A_n \gets a_1, \dotsc, a_n}(R)$$

![[Pasted image 20221015192835.png|350]]
![[Pasted image 20221015192850.png|350]]

## Selezione ( $\mathrm{SEL}$ | $\sigma_{\varphi}(R)$ )
$$\mathrm{SEL}_{Condizione}(Operando)$$
$$\sigma_{Condizione}(R)$$
![[Pasted image 20221015193445.png|350]]

## Proiezione ( $\mathrm{PROJ}$ | $\Pi_{a_1, \dotsc, a_n}(R)$ )
$$\mathrm{PROJ}_{ListaAttributi}(Operando)$$
![[Pasted image 20221015193927.png|350]]

## Selezione + Proiezione
$$\mathrm{PROJ}_{ListaAttributi}(\mathrm{SEL}_{Condizione}(Relazione))$$
![[Pasted image 20221015193653.png|350]]

## Join Naturale ( $\mathrm{JOIN}$ | $R \bowtie S$ )
$$R_1\ \mathrm{JOIN}\ R_2$$
$$R \bowtie S$$
![[Pasted image 20221015194534.png|350]]

## Join Esterno: Left-Right-Full ( $\mathrm{JOIN}_{LEFT\ RIGHT\ FULL}$ )
$$R_1\ \mathrm{JOIN_{LEFT}}\ R_2$$
![[Pasted image 20221015195242.png|350]]
$$R_1\ \mathrm{JOIN_{RIGHT}}\ R_2$$
![[Pasted image 20221015195329.png|350]]
$$R_1\ \mathrm{JOIN_{FULL}}\ R_2$$
![[Pasted image 20221015195407.png|350]]

## Join + Proiezione
$$\mathrm{PROJ}_{ListaAttributi}(R_1\ \mathrm{JOIN}\ R_2)$$
![[Pasted image 20221015200005.png|350]]

## Theta-Join ( $\mathrm{JOIN}_{Condizione}$ | $R\bowtie_{\theta}S$ )
$$R_1\ \mathrm{JOIN}_{Condizione}\ R_2$$
![[Pasted image 20221015200154.png|350]]

## Viste ( $:=$ )
$$NomeVista(ListaAttributi) := \mathrm{PROJ}_{ListaAttributi}(Operando) \dots$$
![[Pasted image 20221015200740.png|350]]
# Basi di dati 2022/2023

<div align=center>
	<image src=https://shields.io/badge/PostgreSQL-white?logo=postgresql&style=plastic></image>
	<image src=https://shields.io/badge/arch-white?logo=archlinux&style=plastic></image>
    </br>
    <image src=https://img.shields.io/github/stars/MarkGotLasagna/basi?style=social></image>
</div>

del corso di Laurea in Informatica 'Ottobre 2022 - Gennaio 2023'.
Contiene appunti presi durante le lezioni in presenza, lezioni registrare su Teams al seguente link d'invito (qhq0tun) anno 2021-2022, slide sul [drive WhatsApp](https://drive.google.com/drive/folders/1hdHk5s0ys5xMJSEa-XeIjJ0rjM3nY5jW).

Il corso si divide in 2 parti:
- nozioni base + algebra relazionale + SQL \[Itinere]
- schemi Entità-Relazione (ER) + teoria sulle transazioni + trigger \[Esame]

## Tools

**Text editors**
- `Obsidian.md` per prendere appunti in markdown ed esportare in PDF
- `vim` per modifiche rapide

**DBMS**
- `postgresql` strettamente legato al corso

## Directory structure

```
Documents/Obsidian Vault/UNI/BASI
├── ESAMI
│   ├── MARKDOWN
│   └── PDF
├── SQL
│   ├── MARKDOWN
│   └── PDF
└── TEORIA
    ├── MARKDOWN
    └── PDF
```

**Le sottocartelle a nome `PDF` sono quelle contenenti i file esportati** da Obsidian.md: **sono i file che vi interessano** alla fine della fiera:
- **appunti** di teoria presi a lezione e non, nella cartella `TEORIA`;
- **esercizi SQL**, nella cartella `SQL`;
- **esempi di esercizi in prove d'itinere** ed **esami** passati, nella cartella `ESAMI`.

Se scaricate [Obsidian.md](https://obsidian.md/) e importate i file dalle cartelle `MARKDOWN`, dovreste ottenere risultati migliori, in quanto noterete che, in alcuni `.pdf` ci sono troncamenti di pagina non voluti (purtroppo l'unico modo per risolvere sarebbe aggiungere interruzioni di linea, ma non stanno bene esteticamente).

I file a nome `_INDEX.md` sono utili per generare i grafi, se usate Obsidian.md vi conviene importare anche quelli.

![Graph view of 'basi'](https://github.com/MarkGotLasagna/basi/blob/main/PICS/graph_view.png)

## Similar repos
Repository di coetanei sono presenti, le uso io stesso perché alcune query SQL le perdo nella furia di scrivere tutto in modo esteticamente bello.

- Mattia Merenda > https://github.com/merendamattia/BdD

# Basi di dati 2022/2023

<div align=center>
	<image src=/PICS/basi_default.png width=75%></image></br></br>
	<image src=https://shields.io/badge/PostgreSQL-white?logo=postgresql&style=plastic></image>
	<image src=https://shields.io/badge/arch-white?logo=archlinux&style=plastic></image>
    	<image src=https://img.shields.io/github/stars/MarkGotLasagna/basi?style=social></image>
	</br></br>
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
│   └── PDF
├── SQL
│   └── PDF
└── TEORIA
    └── PDF
```

**Le sottocartelle a nome `PDF` sono quelle contenenti i file esportati** da Obsidian.md: **sono i file che vi interessano** alla fine della fiera:
- **appunti** di teoria presi a lezione e non, nella cartella `TEORIA`;
- **esercizi SQL**, nella cartella `SQL`;
- **esempi di esercizi in prove d'itinere** ed **esami** passati, nella cartella `ESAMI`.

Per installare soltanto i file PDF:
```
git clone --filter=blob:none --depth 1 --sparse https://github.com/MarkGotLasagna/basi && \
    cd basi && \
    git sparse-checkout init --cone && \
    git sparse-checkout set ESAMI/PDF SQL/PDF TEORIA/PDF
```

Trovate l'insieme degli snippets CSS all'interno della repo [.dots](https://github.com/MarkGotLasagna/.dots).
Lista di plugins utilizzati:
```
/home/maruko/Documents/Obsidian Vault/.obsidian/plugins
├── cm-editor-syntax-highlight-obsidian
├── cmenu-plugin
├── highlightr-plugin
├── obsidian-admonition
├── obsidian-dynamic-toc
├── obsidian-emoji-toolbar
├── obsidian-functionplot
├── obsidian-icon-folder
├── obsidian-icons-plugin
├── obsidian-languagetool-plugin
├── obsidian-pandoc
├── obsidian-tikzjax
└── table-editor-obsidian
```

## Contributing
Seguite la pagina [Wiki](https://github.com/MarkGotLasagna/basi/wiki)!

Se non siete familiari con GitHub, vi consiglio i DOCs ufficiali: [About forks](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/about-forks) e [About pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests).

## Similar repos
Repository di coetanei sono presenti, le uso io stesso perché alcune query SQL le perdo nella furia di scrivere tutto in modo esteticamente bello.

- Mattia Merenda > https://github.com/merendamattia/BdD

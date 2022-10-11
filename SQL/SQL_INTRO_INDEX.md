Questi esercizi sono provvisti dal sito di [w3schools](https://www.w3schools.com/sql/).
Sono introduzioni agli esercizi presenti all'esame di Basi di dati.

La collezione include query DDL e DML.

Il DBMS da me utilizzato e' [mariadb](https://wiki.archlinux.org/title/MariaDB), adottato da arch linux in default, non ha bisogno di configurazione alcuna se non quella di creare utente e password, al primo accesso.

`# mysql -u root -p`

`mariadb> CREATE USER 'utente'@'localhost' IDENTIFIED BY password;`
`mariadb> GRANT ALL PRIVILEGES ON database.* TO 'utente'@'localhost';`
`mariadb> FLUSH PRIVILEGES;`
`mariadb> quit`

La sintassi per `mariadb` e' pressoche' uguale a quella di `postgresql`.

# INDEX
- [[SQL_SELECT]]
- 

# ESEMPI
- [[SQL_ISCRIZIONI_UNIVERSITARIE]]
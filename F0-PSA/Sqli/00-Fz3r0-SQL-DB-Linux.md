
## Instalar MySQL Linux

Todo se debe hacer con `root` o `sudo`:

1. **Instalar MySQL**

    - En realidad solo es necesario instalar `mariadb`
 
````sh
sudo apt-get install mariadb-server
````

2. Habiliar `Apache Server` y `MySQL` para visualizar localhost /var/www/html (opcional)

````sh
# - Habilitar Apache y MySQL
service apache2 start && service mysql start  
````

3. Ejecutar `mysql`

````sh
mysql
````

````sh
❯ mysql

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 31
Server version: 10.5.19-MariaDB-0+deb11u2 Debian 11

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
````

## Crear Lab 1: `Fz3r0-PSA-SQLi-DB_-_tabla.sql`

En este laboratorio solo se crea y utiliza una sola tabla de pruebas.

- Copiar:

````sql
/*

################################################
#    Lab 1: `Fz3r0-PSA-SQLi-DB_-_tabla.sql`    #
################################################ 

*/

/* ## Query: crear db */
create database fz3r0_pwn;

/* ## Query: mostrar db */
show databases;

/* ## Query: usar db */
use fz3r0_pwn

/* ## Query: crear tabla */
create table users(id int auto_increment PRIMARY KEY, username varchar(32), password varchar(32), subscription varchar(32));

/* ## Query: mostrar tablas */
show tables;

/* ## Query: describir tabla en particular */
describe users;

/* ## Query: insertar datos */
insert into table users(id int auto_increment PRIMARY KEY, username varchar(32), password varchar(32), subscription varchar(32));
````



## Recursos

- https://dev.mysql.com/doc/refman/8.0/en/comments.html



## Biblia de bolsillo MySQl

create table users(id int auto_increment PRIMARY KEY, username varchar(32), password varchar32(), subscription varchar(32));

show databases

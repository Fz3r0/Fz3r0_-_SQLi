
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

################################################
#    Lab 1: `Fz3r0-PSA-SQLi-DB_-_tabla.sql`    #
################################################ 

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
insert into users() values(); -- Base del insert
insert into users(username, password, subscription) values("Fz3r0", "p@ssw0rd123-0", "1");
insert into users(username, password, subscription) values("F0n3", "p@ssw0rd123-1", "1");
insert into users(username, password, subscription) values("Ftw0", "p@ssw0rd123-2", "0");
insert into users(username, password, subscription) values("Fthr33", "p@ssw0rd123-3", "0");
insert into users(username, password, subscription) values("Ff0ur", "p@ssw0rd123-4", "1");
insert into users(username, password, subscription) values("Ff1v3", "p@ssw0rd123-5", "0");

/* ## Query: seleccionar todo(*) de una tabla(users) */
select * from users;

/* ## Query: seleccionar algo específico(username,password) de una tabla(users) */
select username,password from users;

/* ## Query: seleccionar algo específico(username,password) de una tabla(users) con alguna condicional */
select username,password from users where subscription = "1"; -- ejemplo 1
select username,password from users where username = "Fz3r0" or username = "Ftw0"; -- ejemplo 2

````

### Resultados de Laboratiorio

````python
# Bases de datos:

MariaDB [fz3r0_pwn]> show databases;
+--------------------+
| Database           |
+--------------------+
| fz3r0_pwn          |
| information_schema |
| mysql              |
| performance_schema |
+--------------------+

# DB=fz3r0_pwn | Tablas:

MariaDB [fz3r0_pwn]> show tables;
+---------------------+
| Tables_in_fz3r0_pwn |
+---------------------+
| users               |
+---------------------+

# DB=fz3r0_pwn | Tabla=users:

MariaDB [fz3r0_pwn]> describe users;
+--------------+-------------+------+-----+---------+----------------+
| Field        | Type        | Null | Key | Default | Extra          |
+--------------+-------------+------+-----+---------+----------------+
| id           | int(11)     | NO   | PRI | NULL    | auto_increment |
| username     | varchar(32) | YES  |     | NULL    |                |
| password     | varchar(32) | YES  |     | NULL    |                |
| subscription | varchar(32) | YES  |     | NULL    |                |
+--------------+-------------+------+-----+---------+----------------+

# DB=fz3r0_pwn | Tabla=users @ data:

MariaDB [fz3r0_pwn]> select * from users;
+----+----------+---------------+--------------+
| id | username | password      | subscription |
+----+----------+---------------+--------------+
|  1 | Fz3r0    | p@ssw0rd123-0 | 1            |
|  2 | F0n3     | p@ssw0rd123-1 | 1            |
|  3 | Ftw0     | p@ssw0rd123-2 | 0            |
|  4 | Fthr33   | p@ssw0rd123-3 | 0            |
|  5 | Ff0ur    | p@ssw0rd123-4 | 1            |
|  6 | Ff1v3    | p@ssw0rd123-5 | 0            |
+----+----------+---------------+--------------+
````


## Recursos

- https://dev.mysql.com/doc/refman/8.0/en/comments.html
- [SQL Injection (SQLI) - Explicado desde Cero](https://youtu.be/C-FiImhUviM)



## Biblia de bolsillo MySQl

create table users(id int auto_increment PRIMARY KEY, username varchar(32), password varchar32(), subscription varchar(32));

show databases
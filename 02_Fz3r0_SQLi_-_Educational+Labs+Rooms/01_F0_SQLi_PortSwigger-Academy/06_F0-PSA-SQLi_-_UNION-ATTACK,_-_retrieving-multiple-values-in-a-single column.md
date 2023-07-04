# `LAB`: SQL injection UNION attack, retrieving multiple values in a single column

## Descripción:

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs.

The database contains a different table called `users`, with columns called `username` and `password`.

To solve the lab, perform a **SQL injection UNION attack** that retrieves all usernames and passwords, and use the information to log in as the `administrator` user. 

---

### Explicación:

Este laboratiorio es exactamente igual al mismo, en realidad "la diferencia" es que solicitan mostrar la información **en una sola columna** pero ese ejemplo también se vió en el anterior.

- Debido a que la vulnerabilidad está en 2 columnas `'1','2'` se pueden usar ambar para poner la información, por ejemplo `'1':username` y `'2':password`, pero también se pueden poner ambas en una sola columna utilizando técnicas como `CONCAT`, `GROUP_CONCAT`, `||`, etc...

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
# Original



````

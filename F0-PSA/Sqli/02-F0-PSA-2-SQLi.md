# Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

- [Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data](https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data)

## 

Descripción:

This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like the following:

````sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
````

To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.

## Solución:

1. Abrir laboratorio

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/a56c4773-50c8-41b7-82b7-94631079ad1c)

2. 

## Recursos


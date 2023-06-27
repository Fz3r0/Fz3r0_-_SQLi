# Lab: SQL injection UNION attack, determining the number of columns returned by the query

- [Lab: SQL injection UNION attack, determining the number of columns returned by the query](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns)

## Descripción:

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack.

To solve the lab, determine the number of columns returned by the query by performing a `SQL injection UNION` attack that returns an additional row containing null values.

---

### Explicación:

Si solo se pone una comilla da error, ya que el query se quedaría con una sola comilla, es decir, **Se encuentra un error!!!**

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/a46c0863-5d12-4127-9887-7d5d1ecd7a1f)

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/a79c49df-b0d6-47f3-90b8-0c0c9f0e8b1b)

Ahora hay que buscar la manera que ya no regrese el error, como cerrar esa comilla extra.



## Solución:

1. En este caso la vulnerabilidad también está en categorías

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/8a87141b-dded-420f-b75f-05439d0def77)

2. Aquí encuentro donde puedo hacer inputs de strings

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/e6481b91-47f2-4b54-8cc9-0d036d9d99a1)


3. Query que usé (lo puse en ambos campos, aunque se puede usar en el primero y el segundo lo que sea...)

````sql
administrator'-- -
````
````http
Username: administrator'-- -
Password: Lo que sea...
````

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/95856f02-84de-4067-a9af-65183b9bb6a9)






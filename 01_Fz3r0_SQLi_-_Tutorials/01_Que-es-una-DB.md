# Bases de Datos

- Una base de datos es una forma organizada de almacenar colecciones de datos electrónicamente.
- Una base de datos está controlada por un Sistema de Gestión de Bases de Datos o Data Base Management System (DBMS).

### Hay dos tipos principales de DBMS: 

1. Relacionales.
2. No relacionales.

### Bases de datos relacionales (más comunes):

- MySQL
- Microsoft SQL Server
- Access
- PostgreSQL
- SQLite

### Estructura de Base de Datos Relacional

Dentro de un DBMS, puedes tener múltiples bases de datos, cada una con su propio conjunto de datos relacionados. Esto debido a que las empresas pueden tener bases de datos adicionales para otros fines, como almacenar información del personal o del equipo de cuentas.

**`HINT`: Un `servidor` puede contener muchas `bases de datos`, cada base de datos puede contener muchas `tablas` y cada una de esas tablas puede contener muchos `datos`...**

1. **`Server`** : El servidor físico o virtual que contiene el servicio de la base de datos, por ejemplo un **MySQL** server ejecutándose el cual contiene **una o varias DB** (`database`).
2. **`Database`** : Puedes tener una base de datos llamada **"shop"** para almacenar información sobre **productos, usuarios y pedidos** y otra **"management"** para procesos internos de la empresa.
3. **`Tables`** : Los datos se almacenan en **tablas**, que tienen nombres únicos.
4. **`Data`** : Los datos son los que se guardan de forma ordenada y estructurada dentro de las tablas.

**`HINT`: Todo esto funciona gracias a un esquema que trabaja "tras bambalinas" llamado `information_schema`.

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/c1165108-d820-4e06-8acf-a582db463a7e)



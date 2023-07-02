# Bases de Datos

- Una base de datos es una forma organizada de almacenar colecciones de datos electrónicamente.
- Una base de datos está controlada por un Sistema de Gestión de Bases de Datos o Data Base Management System (DBMS).

### Tipos principales de DBMS: 

1. Relacionales.
2. No relacionales.

---

<br>

<br>

<br>

## Base de Datos: DBMS Relacional

- Una base de datos relacional es un tipo de base de datos que organiza los datos en tablas con filas y columnas.
- Se llama "relacional" porque establece relaciones entre las tablas utilizando claves primarias y claves externas para mantener la integridad y coherencia de los datos.

---

### DMBS Relacionales _(más comunes)_:

- MySQL
- Microsoft SQL Server
- Access
- PostgreSQL
- SQLite

---

### Estructura de DBMS Relacionales

Dentro de un DBMS, puedes tener múltiples bases de datos, cada una con su propio conjunto de datos relacionados. Esto debido a que las empresas pueden tener bases de datos adicionales para otros fines, como almacenar información del personal o del equipo de cuentas.

**`HINT`: Un `servidor` puede contener muchas `bases de datos`, cada base de datos puede contener muchas `tablas` y cada una de esas tablas puede contener muchos `datos`...**

1. **`Server`** : El servidor físico o virtual que contiene el servicio de la base de datos, por ejemplo un **MySQL** server ejecutándose el cual contiene **una o varias DB** (`database`).
2. **`Database`** : Puedes tener una base de datos llamada **"shop"** para almacenar información sobre **productos, usuarios y pedidos** y otra **"management"** para procesos internos de la empresa.
3. **`Tables`** : Los datos se almacenan en **tablas**, que tienen nombres únicos.
4. **`Data`** : Los datos son los que se guardan de forma ordenada y estructurada dentro de las tablas.

**`HINT`: Todo esto funciona gracias a un esquema que trabaja "tras bambalinas" llamado `information_schema`.

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/c1165108-d820-4e06-8acf-a582db463a7e)

---

### Tablas / `Tables`

- Una tabla(`table`) está compuesta por columnas(`columns`) y filas(`rows`).
- Una forma útil de imaginar una tabla es como una cuadrícula, donde las columnas se encuentran en la parte superior, de izquierda a derecha, y contienen el nombre de cada celda, mientras que las filas van de arriba abajo y contienen los datos reales.

![image](https://github.com/Fz3r0/Fz3r0_-_SQLi/assets/94720207/84aad70c-ee80-4c75-a919-70260711179a)

---

### Columnas AKA Campos / `Columns` AKA `Fields`:

- Cada columna`Columns`, mejor conocida como campo`Fields`, tiene un nombre único por tabla. 
- Al crear una columna, también se establece el tipo de datos que contendrá, siendo comunes los enteros (números), cadenas (texto estándar) o fechas.
- Algunas bases de datos pueden contener datos mucho más complejos, como los geoespaciales, que contienen información de ubicación.
- Establecer el tipo de datos también garantiza que no se almacene información incorrecta, como la cadena "hello world" en una columna destinada a las fechas. Si esto sucede, el servidor de la base de datos generalmente mostrará un mensaje de error.
- Una columna que contiene un número entero también puede tener habilitada la función de **autoincremento**; esto asigna a cada fila de datos un número único que aumenta (se incrementa) con cada fila posterior. Al hacerlo, se crea lo que se llama un **campo clave**, el cual debe ser único para cada fila de datos y se puede utilizar para encontrar esa fila exacta en consultas SQL.

---

### Filas AKA Registros / `Rows` AKA `Records`

- Las filas`Rows` o registros`Records` son lo que contiene las líneas individuales de datos.
- Cuando **agregas datos** a una tabla, se **crea** una nueva `Row/Record`, y cuando **eliminas datos**, se **elimina** una `Row/Record`.


## Base de Datos: DBMS No-Relacional

- Una base de datos no relacional es un tipo de base de datos que NO sigue el modelo relacional de tablas y relaciones.
- En lugar de utilizar tablas con filas y columnas, las bases de datos no relacionales utilizan diferentes estructuras de datos, como documentos, gráficos o clave-valor, para almacenar y organizar la información. Se llaman "no relacionales" porque no establecen relaciones explícitas entre los datos almacenados.
- Estas bases de datos son adecuadas para situaciones donde la estructura y los tipos de datos pueden variar mucho y no se requiere una estructura rígida de tablas. Además, suelen ser escalables y flexibles en términos de almacenamiento y recuperación de datos.
- Es importante destacar que el término "no relacional" no implica que este tipo de base de datos sea inferior o inferior a las bases de datos relacionales, simplemente siguen un enfoque diferente para almacenar y gestionar la información.

---

### DMBS No Relacionales _(más comunes)_:

- MongoDB
- Cassandra
- ElasticSearch

---

### DBMS Relacional VS No-Relacional: Información que cura

- Una base de datos relacional almacena información en tablas y a menudo las tablas tienen información compartida entre ellas. Utilizan columnas para especificar y definir los datos que se almacenan y filas para almacenar realmente los datos. Las tablas suelen contener una columna con un ID único (clave primaria) que se utiliza en otras tablas para hacer referencia a ella y establecer una relación entre las tablas, de ahí el nombre de base de datos relacional.

- Por otro lado, las bases de datos no relacionales, a veces llamadas `NoSQL`, son cualquier tipo de base de datos que no utiliza tablas, columnas y filas para almacenar los datos. No es necesario construir un diseño de base de datos específico, por lo que cada fila de datos puede contener información diferente, lo que proporciona más flexibilidad que una base de datos relacional. Algunas bases de datos populares de este tipo son MongoDB, Cassandra y ElasticSearch.

---

<br>

<br>

<br>

## Recursos

- [THM - SQL Injection](https://tryhackme.com/room/sqlinjectionlm)

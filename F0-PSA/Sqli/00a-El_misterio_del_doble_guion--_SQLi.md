# `SQLi`: el misterio del guion doble en MySQL `--` & `-- -`

## Introducción:

Cuando se realiza una prueba de penetración utilizando un enfoque de caja negra, es posible encontrar una inyección SQL (SQLi) mediante payloads comunes. 

A menos que se revele un error detallado que muestre la consulta SQL original, no se conoce la estructura de la consulta. 

Es posible que la entrada se inyecte al principio de la consulta o varias veces en la consulta, pero no se sabe con certeza. 

- **Para evitar efectos secundarios incontrolados e inesperados en el query, un pentester desea finalizar su payload con un comentario para neutralizar y finalizar la consulta, de modo que el comportamiento sea más predecible.**

## ¿Qué tipo de comentario utilizar?

Algunos sistemas de gestión de bases de datos (DBMS, por sus siglas en inglés) admiten comentarios en línea como `#` o `--`, otros admiten comentarios multilínea `/* */`, y también existen algunas sintaxis más extrañas e inusuales. 

- **Hay muchos DBMS y el soporte de comentarios varía para cada uno de ellos.**

Dado que en un enfoque de caja negra puede resultar difícil saber qué DBMS se está utilizando y cómo detectarlo, un pentester preferiría utilizar la sintaxis más interoperable.

- Tip: No utilizaremos un comentario multilínea sin cerrar, ya que podría comentar demasiado o incluso generar un error si no se cierra.

MySQL (Oracle MySQL, MariaDB, Percona Server), Oracle Database, PostgreSQL, Microsoft SQL Server, SQLite, Apache Ignite, Firebird, IBM DB2, etc., utilizan muchas implementaciones personalizadas diferentes de SQL (Structured Query Language).

- **El único comentario en línea estándar en `SQL` es el guion doble `--`, y también es el único admitido por todos los `otros DBMS`.**

El misterio del guion doble:
Entonces, si -- es admitido por todos los DBMS, ¿por qué vemos que la mayoría de los payloads terminan con -- - o --+ y no solo --?

¡Tenemos que culpar a la sintaxis de MySQL por eso!

Cuando dije que todos los DBMS admiten la sintaxis del guion doble, no es exactamente cierto.

De hecho, MySQL es una excepción. [3] [4]

Desde una secuencia -- hasta el final de la línea. En MySQL, el estilo de comentario -- (doble guion) requiere que el segundo guion sea seguido por al menos un espacio en blanco o un carácter de control (como un espacio, una tabulación, un salto de línea, etc.). Esta sintaxis difiere ligeramente de la sintaxis estándar de comentario SQL, como se discute en la sección 1.8.2.4, "'--' como inicio de un comentario".

Sí, MySQL requiere que los dos guiones sean seguidos por un carácter de espacio en blanco (espacio, tabulación, salto de línea, etc.). Pero la mayoría de las veces, las inyecciones SQL se explotan a través de HTTP desde una aplicación web. Esto significa que los navegadores web, los frameworks

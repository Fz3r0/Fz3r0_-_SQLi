# `SQLi`: el misterio del guion doble en MySQL `--` & `-- -`

## Introducción:

Cuando se realiza una prueba de penetración utilizando un enfoque de caja negra, es posible encontrar una inyección SQL (SQLi) mediante payloads comunes. 

A menos que se revele un error detallado que muestre la consulta SQL original, no se conoce la estructura de la consulta. 

Es posible que la entrada se inyecte al principio de la consulta o varias veces en la consulta, pero no se sabe con certeza. 

- **Para evitar efectos secundarios incontrolados e inesperados en el query, un pentester desea finalizar su payload con un `comentario` para neutralizar y finalizar la consulta/query, de modo que el comportamiento sea más predecible.**

## ¿Qué tipo de comentario utilizar?

Algunos **sistemas de gestión de bases de datos (DBMS)** admiten comentarios en línea como `#` o `--`, otros admiten comentarios multilínea `/* */`, y también existen algunas sintaxis más extrañas e inusuales. 

- **Hay muchos DBMS y el soporte de comentarios varía para cada uno de ellos.**

Dado que en un enfoque de caja negra puede resultar difícil saber qué DBMS se está utilizando y cómo detectarlo, un pentester preferiría utilizar la sintaxis más interoperable y estandarizada entre todos los DBMS. Por ejemplo, no utilizaremos un comentario multilínea sin cerrar, ya que podría comentar demasiado o incluso generar un error si no se cierra.

MySQL (Oracle MySQL, MariaDB, Percona Server), Oracle Database, PostgreSQL, Microsoft SQL Server, SQLite, Apache Ignite, Firebird, IBM DB2, etc., utilizan muchas implementaciones personalizadas diferentes de SQL (Structured Query Language).

- **El único comentario en línea estándar en `SQL` es el guion doble `--`, y también es el único admitido por todos los `otros DBMS`.**

## El misterio del guion doble `-- -`

- **Entonces, si `--` es admitido por todos los DBMS, ¿por qué vemos que la mayoría de los payloads terminan con `-- -` o `--+` o `--+-`... ¡¿y no solo `--`?!**

¡Tenemos que culpar a la **sintaxis de `MySQL`** por eso! Cuando dije que todos los DBMS admiten la sintaxis del guion doble, no es exactamente cierto... De hecho, `MySQL` es una excepción. 

- **`Extracto de instructivo MySQL`**: Desde una secuencia `--` hasta el final de la línea. En MySQL, el estilo de comentario `--` (doble guion) **requiere que el segundo guion sea seguido por al menos un espacio en blanco o un carácter de control** _(como un espacio, una tabulación, un salto de línea, etc.)_. Esta sintaxis difiere ligeramente de la sintaxis estándar de comentario SQL, como se discute en la sección 1.8.2.4, _`'--' como inicio de un comentario`_.

Sí, **MySQL requiere que los dos guiones sean seguidos por un carácter de espacio en blanco _(espacio, tabulación, salto de línea, etc.)_**. Pero la mayoría de las veces, **las inyecciones SQL se explotan a través de HTTP desde una aplicación web**. Esto significa que los navegadores web, los frameworks web, los backends de aplicaciones, los proxies, los lenguajes subyacentes, pueden eliminar los espacios en blanco al final, lo que significa que `--<espacio en blanco>` se transformará en `--` (sin espacio en blanco) y MySQL lo considerará inválido.

Pero MySQL es uno de los DBMS más populares, por lo que necesitamos tener un payload genérico que funcione con él. Por eso a menudo se ve `-- -`, agregando cualquier carácter después del espacio en blanco para que no sea un espacio en blanco final y no se elimine. Esto significa que `-- -` no es diferente de `-- a`, `-- Z` o `-- !`.

- En resumen, **para tener mejor compatibilidad entre todas las DBMS es mejor utilizar `-- -` en lugar de `-- `.** 

### Entonces, ¿por qué existe `--+` y `--+-`? 

Porque en la norma URL, el carácter de espacio se codifica como un signo de más `+`, por ejemplo, en `UTF-8 U+0020 SPACE` se codifica como `U+002B (+)`. Esto significa que al decodificar una URL, el signo `+` se decodificará como un espacio y transformará `--+` en `--<espacio>` (`-- `).

Nota: Por eso `base64url` (también conocido como `base64` seguro para URL y seguro para nombres de archivo) utiliza el guion `-` en lugar del signo de más `+` y el guión bajo `_` en lugar de la barra inclinada `/` _(RFC 4648)_.

Pero si `--+` está codificado (por ejemplo, codificado en URL) como `--%2B`, cuando se decodifique, `--+` no se reconocerá como válido por **MySQL**, por eso es más seguro usar `--<espacio><cualquier_carácter>`, como `-- -`, porque si se codifica en URL como `--%20-`, aún se decodificará como `---`.

- En resumen, **para tener mejor compatibilidad entre todas las DBMS es mejor utilizar `-- -` en lugar de `--+`. Pero una opción también es utilizar `--+-`**

## Conclusión

- **El string `-- -` es el comentario SQL en línea más interoperable y seguro entre todas las BDSM, ya que `--` no funciona con MySQL y `--+` se romperá si se codifica.**
  
- **Ya sea `-- -` o `--+-`, serían las opciones más eficientes para enfrentar la mayoría de DBMS, incluyendo las más comunes como MySQL**

## Recursos

- https://blog.raw.pm/en/sql-injection-mysql-comment/

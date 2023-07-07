## Que es SQLi


## ¿Qué es la inyección SQL o SQLi?

- La inyección de SQL (SQLi) es una vulnerabilidad de seguridad web que permite a un atacante interferir con las consultas que una aplicación realiza a su base de datos.
- La inyección SQL ocurre cuando los datos proporcionados por el usuario se incluyen en una `consulta SQL` de una aplicación web.
- Esto puede llevar a que se ejecuten comandos no deseados o maliciosos en la base de datos o exfiltrar información privada.
- En muchos casos, un atacante puede modificar o eliminar estos datos, lo que causa cambios persistentes en el contenido o comportamiento de la aplicación.
- En algunas situaciones, un atacante puede escalar un ataque de inyección de SQL para comprometer el servidor subyacente u otra infraestructura de back-end, realizar ataques de ejecución de comados remoto (RCE), o llevar a cabo un ataque de denegación de servicio (DOS)

### ¿Cómo se ve?

Tomemos el siguiente escenario: 

- Te encuentras con un blog en línea, y cada entrada del blog tiene un número de identificación único o `id`. Las entradas del blog pueden ser públicas o privadas, dependiendo de si están listas para ser publicadas. 

La URL de cada entrada del blog puede ser algo así:

````py
https://website.thm/blog?id=1
````

En la URL anterior, se puede ver que la entrada del blog seleccionada se obtiene del parámetro `id` en la cadena de consulta. La aplicación web necesita recuperar el artículo de la base de datos y puede usar una declaración SQL que se vea así, nótese ese `WHERE id=1`:

````sql
SELECT * FROM blog WHERE id=1 AND private=0 LIMIT 1;
````

Aquí se puede deducir que la consulta SQL anterior busca en la tabla `blog` un artículo con el número de identificación(id) `1` y la columna `private` establecida en `0`, lo que significa que puede ser visto por el público, y se limita los resultados a solo una coincidencia, es decir, `LIMIT 1`.

La inyección SQL ocurre cuando la entrada del usuario se incorpora directamente a la consulta de la base de datos. En este caso, el parámetro `id` de la cadena de consulta se usa directamente en la consulta SQL.

Ahora, supongamos que el artículo con el identificador 2 sigue bloqueado como privado y no se puede ver en el sitio web. Podríamos llamar a la siguiente URL:

````py
https://website.thm/blog?id=2;--
````

Lo cual produciría la siguiente declaración SQL:

````sql
SELECT * FROM blog WHERE id=2;-- AND private=0 LIMIT 1;
````

El **punto y coma `;`** en la URL indica el final de la declaración SQL, y **los dos guiones hacen que todo lo que sigue se trate como un `comentario`**. Al hacer esto, en realidad estás ejecutando la consulta:

````sql
SELECT * FROM blog WHERE id=2;-- 
````

- **Lo cual devolverá el artículo con un identificador de 2, sin importar si está configurado como público o no.**

Este fue solo un ejemplo de una vulnerabilidad de inyección SQL de un tipo llamado In-Band SQL Injection. 

## Tipos de SQLi

- En total, hay 3 tipos de inyección SQL:

    1. In-Band
    2. Blind
    3. Out Of Band

 ## Recursos

 - [PortSwigger - What is SQL injection (SQLi)?](https://portswigger.net/web-security/sql-injection#what-is-sql-injection-sqli)
 - [PortSwigger - What is SQL injection? - Web Security Academy](https://www.youtube.com/watch?v=wX6tszfgYp4)

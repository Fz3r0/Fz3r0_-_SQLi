## Query 1

### Original

````sql
# Original
SELECT COUNT(*) AS total_juegos_accion FROM juegos WHERE genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción');
````

### Inyección: ` or '1' = '1' LIMIT 0,1`

El payload ` or '1' = '1' LIMIT 0,1` o `+or+'1'+=+'1'+LIMIT+0,1` o `0x2b6f722b2731272b3d2b2731272b4c494d49542b302c31` o 

````

SELECT COUNT(*) AS total_juegos_accion FROM juegos WHERE genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción'+or+'1'+=+'1'+LIMIT+0,1);
````

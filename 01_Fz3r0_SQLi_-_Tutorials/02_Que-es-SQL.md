## SQL

- `SQL (Structured Query Language)` es un lenguaje rico en funciones utilizado para consultar bases de datos.
- Estas `consultas en SQL` o `SQL Querys` se conocen mejor como declaraciones o `statements`.
- Los comandos `CLI` de `SQL` se utilizan principalmente para mostar/seleccionar `SELECT`, actualizar `UPDATE`, insertar `INSERT` y eliminar `DROP` datos.
- Aunque son algo similares, algunos `BDSM` tienen su propia sintaxis y pequeñas variaciones en cómo funcionan las cosas.
- Normalmente los ejemplos y las bases de datos reales son en `MySQL` ya que es el `BDSM` más utilizado.
- La sintaxis de SQL no distingue entre mayúsculas y minúsculas.

## Ejemplos de `statements`

### `select * from usuarios;`

````py
+------------+-------------------+---------------------------------+---------------------------+---------------------------+-------------+--------------------------------+-------------+---------------------+
| usuario_id | username          | password                        | nombre                    | direccion                 | telefono    | email                          | tipo_cuenta | creado_en           |
+------------+-------------------+---------------------------------+---------------------------+---------------------------+-------------+--------------------------------+-------------+---------------------+
|          1 | admin             | admin12345                      | Admin General del Sistema | Fz3r0 Gaming Extravaganza | 666-666-666 | noob_admin@fz3r0_gaming.net    | premium     | 1998-07-11 00:00:00 |
|          2 | Mario             | ItsaMeM@rio!                    | Mario                     | 123 Mushroom Kingdom      | 555-1234    | mario_plumber@nintendo.jp      | premium     | 1985-09-13 00:00:00 |
|          3 | Luigi             | Lu1g1Time!                      | Luigi                     | 456 Mushroom Kingdom      | 555-5678    | luigi_plumber@nintendo.jp      | normal      | 1983-07-14 00:00:00 |
|          4 | Peach             | Pr1nc3ssPeach                   | Princess Peach            | 789 Mushroom Kingdom      | 555-9012    | peach@nintendo.jp              | premium     | 1985-09-13 00:00:00 |
|          5 | Yoshi             | Y0shi123                        | Yoshi                     | 369 Yoshi Island          | 555-3456    | yoshi@nintendo.jp              | normal      | 1990-08-14 00:00:00 |
|          6 | DonkeyKong        | DKC4Life!                       | Donkey Kong               | 147 DK Island             | 555-7890    | donkeykong@nintendo.jp         | premium     | 1981-07-09 00:00:00 |
|          7 | Link              | Hyrul3Warrior                   | Link                      | 741 Hyrule                | 555-2345    | link@nintendo.jp               | normal      | 1986-02-21 00:00:00 |
|          8 | Zelda             | Pr1nc3ssZelda                   | Princess Zelda            | 852 Hyrule Castle         | 555-6789    | zelda@nintendo.jp              | premium     | 1986-02-21 00:00:00 |
|          9 | Samus             | M3troidHunt3r                   | Samus Aran                | 963 Zebes                 | 555-0123    | samus@nintendo.jp              | normal      | 1986-08-06 00:00:00 |
|         10 | Kirby             | P1nkFluff                       | Kirby                     | 369 Dream Land            | 555-4567    | kirby@nintendo.jp              | premium     | 1992-04-27 00:00:00 |
````

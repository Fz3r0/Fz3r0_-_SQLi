## Instalar MySQL Linux

Todo se debe hacer con `root` o `sudo`:

1. **Instalar MySQL**

    - En realidad solo es necesario instalar `mariadb`
 
````sh
sudo apt-get install mariadb-server
````

2. Habiliar `Apache Server` y `MySQL` para visualizar localhost /var/www/html (opcional)

````sh
# - Habilitar Apache y MySQL
service apache2 start && service mysql start  
````

3. Ejecutar `mysql`

````sh
mysql
````

````sh
❯ mysql

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 31
Server version: 10.5.19-MariaDB-0+deb11u2 Debian 11

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
````

## Crear Database: Fz3r0

````sql
-- Creación de la base de datos
CREATE DATABASE IF NOT EXISTS fz3r0_gaming_extravaganza CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Selección de la base de datos
USE fz3r0_gaming_extravaganza;

-- Tabla de usuarios
CREATE TABLE IF NOT EXISTS usuarios (
  usuario_id INT PRIMARY KEY AUTO_INCREMENT,
  username VARCHAR(50) NOT NULL,
  password VARCHAR(255) NOT NULL,
  nombre VARCHAR(100) NOT NULL,
  direccion VARCHAR(200) NOT NULL,
  telefono VARCHAR(20) NOT NULL,
  email VARCHAR(100) NOT NULL,
  tipo_cuenta ENUM('normal', 'premium') NOT NULL,
  creado_en TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  INDEX idx_username (username)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Tabla de géneros
CREATE TABLE IF NOT EXISTS generos (
  genero_id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(50) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Tabla de tipos de juegos
CREATE TABLE IF NOT EXISTS tipos_juegos (
  tipo_id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(50) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Tabla de juegos
CREATE TABLE IF NOT EXISTS juegos (
  juego_id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(100) NOT NULL,
  desarrollador VARCHAR(100) NOT NULL,
  publicador VARCHAR(100) NOT NULL,
  plataforma VARCHAR(50) NOT NULL,
  fecha_lanzamiento DATE NOT NULL,
  genero_id INT NOT NULL,
  tipo_id INT NOT NULL,
  costo DECIMAL(10, 2) NOT NULL,
  en_tienda_desde DATE NOT NULL,
  stock INT NOT NULL,
  FOREIGN KEY (genero_id) REFERENCES generos(genero_id),
  FOREIGN KEY (tipo_id) REFERENCES tipos_juegos(tipo_id),
  INDEX idx_genero_id (genero_id),
  INDEX idx_tipo_id (tipo_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Tabla de consolas
CREATE TABLE IF NOT EXISTS consolas (
  consola_id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(100) NOT NULL,
  fabricante VARCHAR(100) NOT NULL,
  generacion INT NOT NULL,
  codigo VARCHAR(20) NOT NULL,
  fecha_lanzamiento DATE NOT NULL,
  costo DECIMAL(10, 2) NOT NULL,
  en_tienda_desde DATE NOT NULL,
  stock INT NOT NULL,
  INDEX idx_fabricante (fabricante),
  INDEX idx_generacion (generacion)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Tabla de ventas
CREATE TABLE IF NOT EXISTS ventas (
  venta_id INT PRIMARY KEY AUTO_INCREMENT,
  usuario_id INT NOT NULL,
  juego_id INT,
  consola_id INT,
  fecha_venta TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (usuario_id) REFERENCES usuarios(usuario_id),
  FOREIGN KEY (juego_id) REFERENCES juegos(juego_id),
  FOREIGN KEY (consola_id) REFERENCES consolas(consola_id),
  INDEX idx_usuario_id (usuario_id),
  INDEX idx_juego_id (juego_id),
  INDEX idx_consola_id (consola_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;


````





````sql
INSERT INTO usuarios (username, password, name, address, phone, mail, account_type, created_at)
VALUES
('Mario', 'ItsaMeM@rio!', 'Mario', '123 Mushroom Kingdom', '555-1234', 'mario_plumber@nintendo.jp', 'premium', '1985-09-13'),
('Luigi', 'Lu1g1Time!', 'Luigi', '456 Mushroom Kingdom', '555-5678', 'luigi_plumber@nintendo.jp', 'normal', '1983-07-14'),
('Peach', 'Pr1nc3ssPeach', 'Princess Peach', '789 Mushroom Kingdom', '555-9012', 'peach@nintendo.jp', 'premium', '1985-09-13'),
('Yoshi', 'Y0shi123', 'Yoshi', '369 Yoshi Island', '555-3456', 'yoshi@nintendo.jp', 'normal', '1990-08-14'),
('DonkeyKong', 'DKC4Life!', 'Donkey Kong', '147 DK Island', '555-7890', 'donkeykong@nintendo.jp', 'premium', '1981-07-09'),
('Link', 'Hyrul3Warrior', 'Link', '741 Hyrule', '555-2345', 'link@nintendo.jp', 'normal', '1986-02-21'),
('Zelda', 'Pr1nc3ssZelda', 'Princess Zelda', '852 Hyrule Castle', '555-6789', 'zelda@nintendo.jp', 'premium', '1986-02-21'),
('Samus', 'M3troidHunt3r', 'Samus Aran', '963 Zebes', '555-0123', 'samus@nintendo.jp', 'normal', '1986-08-06'),
('Kirby', 'P1nkFluff', 'Kirby', '369 Dream Land', '555-4567', 'kirby@nintendo.jp', 'premium', '1992-04-27'),
('Fox', 'St4rF0x64', 'Fox McCloud', '741 Corneria', '555-8901', 'fox@nintendo.jp', 'normal', '1993-02-21'),
('Ness', 'PSIboii', 'Ness', '852 Onett', '555-2345', 'ness@nintendo.jp', 'premium', '1994-08-27'),
('Crono', 'Ch1ronoTr1gg3r', 'Crono', '147 Guardia', '555-6789', 'crono@squareenix.com', 'normal', '1995-03-11'),
('Cloud', 'Str1f3F1n@l', 'Cloud Strife', '963 Midgar', '555-0123', 'cloud@squareenix.com', 'premium', '1997-01-31'),
('Leon', 'R3s1d3ntEv1l', 'Leon S. Kennedy', '369 Raccoon City', '555-4567', 'leon@capcom.com', 'normal', '1998-01-21'),
('Jill', 'STARS1urv1v0r', 'Jill Valentine', '741 Raccoon City', '555-8901', 'jill@capcom.com', 'premium', '1996-03-22'),
('SolidSnake', 'M3t@lGearS0l1d', 'Solid Snake', '852 Shadow Moses Island', '555-2345', 'snake@konami.com', 'normal', '1998-09-03'),
('Sephiroth', '1nSephiroth', 'Sephiroth', '963 Northern Crater', '555-6789', 'sephiroth@squareenix.com', 'premium', '1997-01-31'),
('MasterChief', 'H@1oSp@rt@n', 'Master Chief', '147 UNSC Infinity', '555-0123', 'chief@microsoft.com', 'normal', '2001-11-15'),
('GordonFreeman', 'H@lfL1f3Exp10s10n', 'Gordon Freeman', '369 Black Mesa', '555-4567', 'gordon@valvesoftware.com', 'premium', '1998-11-19'),
('Ezio', 'Ass@ss1nCre3d', 'Ezio Auditore', '741 Monteriggioni', '555-8901', 'ezio@ubisoft.com', 'normal', '2009-11-17'),
('Altair', 'M3m0ry0fAh0n0r', 'Altair Ibn-LaAhad', '852 Masyaf', '555-2345', 'altair@ubisoft.com', 'premium', '2007-11-13'),
('MarioLemieux', 'L3m13ux66', 'Mario Lemieux', '963 Pittsburgh', '555-6789', 'mario@penguins.com', 'normal', '1984-10-11'),
('Sonic', 'G0tt@GoF@st!', 'Sonic the Hedgehog', '147 Green Hill Zone', '555-0123', 'sonic@sega.com', 'premium', '1991-06-23'),
('Tails', 'M1l3sPr0w3r', 'Miles "Tails" Prower', '369 Mystic Ruins', '555-4567', 'tails@sega.com', 'normal', '1992-10-16'),
('Knuckles', 'KNUCKL35', 'Knuckles the Echidna', '741 Angel Island', '555-8901', 'knuckles@sega.com', 'premium', '1994-10-18'),
('Crash', 'W00B@W00B@', 'Crash Bandicoot', '852 N. Sanity Island', '555-2345', 'crash@activision.com', 'normal', '1996-09-09'),
('Spyro', 'F1r3Br3@th', 'Spyro the Dragon', '963 Artisans World', '555-6789', 'spyro@activision.com', 'premium', '1998-09-10'),
('Lara', 'T0mbRa1d3r', 'Lara Croft', '147 Croft Manor', '555-0123', 'lara@tombraider.com', 'normal', '1996-10-25'),
('Leonardo', 'Turtl3P0w3r', 'Leonardo', '369 New York City', '555-4567', 'leo@ninjaturtles.com', 'premium', '1984-05-01'),
('Donatello', 'B01St@ff', 'Donatello', '741 New York City', '555-8901', 'don@ninjaturtles.com', 'normal', '1984-05-01'),
('Michelangelo', 'C0w@bung@', 'Michelangelo', '852 New York City', '555-2345', 'mikey@ninjaturtles.com', 'premium', '1984-05-01'),
('Raphael', 'S@1@y0w', 'Raphael', '963 New York City', '555-6789', 'raph@ninjaturtles.com', 'normal', '1984-05-01');


````










````sql
## Query: mostrar db 
show databases;

## Query: usar db 
use fz3r0_gaming_extravaganza

## Query: borrar db 
drop database fz3r0_gaming_extravaganza;

## Query: mostrar tablas 
show tables;

## Query: describir tabla en particular
describe usuarios;
describe consolas;
describe juegos;
describe tipos_juegos;
describe generos;
describe ventas;

## Query: mostrar todo(*) de tabla en particular 
select * from usuarios;
select * from consolas;
select * from juegos;
select * from tipos_juegos;
select * from generos;
select * from ventas;
````

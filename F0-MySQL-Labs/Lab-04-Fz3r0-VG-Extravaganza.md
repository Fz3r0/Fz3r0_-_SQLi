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
INSERT INTO usuarios (username, password, nombre, direccion, telefono, email, tipo_cuenta, creado_en)
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
('Raphael', 'S@1@y0w', 'Raphael', '963 New York City', '555-6789', 'raph@ninjaturtles.com', 'normal', '1984-05-01'),
('JohnMcLane', 'Y1p1k@y3y3', 'John McClane', 'Nakatomi Plaza', '555-1234', 'john.mcclane@example.com', 'premium', '1988-07-15'),
('SarahConnor', 'N0F@t3', 'Sarah Connor', 'Los Angeles', '555-5678', 'sarah.connor@example.com', 'normal', '1984-10-26'),
('AlanGrant', 'R@pt0rD1gg3r', 'Alan Grant', 'Jurassic Park', '555-9012', 'alan.grant@example.com', 'premium', '1993-06-11'),
('MartyMcFly', 'FluXCapac1t0r', 'Marty McFly', 'Hill Valley', '555-3456', 'marty.mcfly@example.com', 'normal', '1985-10-26'),
('Terminator', 'IllBeB@ck', 'The Terminator', 'Los Angeles', '555-7890', 'terminator@example.com', 'premium', '1984-10-26'),
('RoboCop', 'D3tr01tJust1c3', 'RoboCop', 'Old Detroit', '555-2345', 'robocop@example.com', 'normal', '1987-07-17'),
('Dutch', 'G3t0T3hCh0pp3r', 'Dutch', 'Val Verde', '555-6789', 'dutch@example.com', 'premium', '1987-06-12'),
('EllenRipley', 'G3tAwayFromH3r!', 'Ellen Ripley', 'USCSS Nostromo', '555-0123', 'ripley@example.com', 'normal', '1979-05-25'),
('JohnSpartan', 'D3m0liti0nM@n', 'John Spartan', 'San Angeles', '555-4567', 'john.spartan@example.com', 'premium', '1993-10-08'),
('SimonPhoenix', 'P@ssw0rd123', 'Simon Phoenix', 'San Angeles', '555-8901', 'simon.phoenix@example.com', 'normal', '1993-10-08'),
('IndianaJones', 'H0lyGr@il', 'Indiana Jones', 'Marshall College', '555-2345', 'indiana.jones@example.com', 'premium', '1981-06-12'),
('EthanHunt', 'M1ss10nImp0ssibl3', 'Ethan Hunt', 'Langley', '555-6789', 'ethan.hunt@example.com', 'normal', '1996-05-22'),
('Neo', 'Th3M@trix', 'Neo', 'Mega City', '555-0123', 'neo@example.com', 'premium', '1999-03-31'),
('Trinity', 'R3dP1ll', 'Trinity', 'Mega City', '555-4567', 'trinity@example.com', 'normal', '1999-03-31'),
('Morpheus', 'F0ll0wTh3Whit3R@bbit', 'Morpheus', 'Mega City', '555-8901', 'morpheus@example.com', 'premium', '1999-03-31'),
('JohnWick', 'B@b@Y@g@', 'John Wick', 'New York City', '555-2345', 'john.wick@example.com', 'normal', '2014-10-24'),
('Léon', 'Th3Pr0fessi0n@l', 'Léon', 'New York City', '555-6789', 'leon@example.com', 'premium', '1994-09-14'),
('SimonTemplar', 'S@1nt', 'Simon Templar', 'London', '555-0123', 'simon.templar@example.com', 'normal', '1997-04-04'),
('AceVentura', 'A11r1ghtyTh3n!', 'Ace Ventura', 'Miami', '555-4567', 'ace.ventura@example.com', 'premium', '1994-02-04'),
('Maximus', 'Ar3Y0uN0t3nt3rt@1n3d?', 'Maximus', 'Rome', '555-8901', 'maximus@example.com', 'normal', '2000-05-01'),
('TylerDurden', 'Th3Rul3s0fF1ghtClub', 'Tyler Durden', 'Wilmington', '555-2345', 'tyler.durden@example.com', 'premium', '1999-10-15'),
('LloydChristmas', 'S@lm0n0fD3nn1s', 'Lloyd Christmas', 'Providence', '555-6789', 'lloyd.christmas@example.com', 'normal', '1994-12-16'),
('HarryDunne', 'Ig0tN3wsF0ry0u', 'Harry Dunne', 'Providence', '555-0123', 'harry.dunne@example.com', 'premium', '1994-12-16'),
('JohnnyUtah', 'R!d3Th3W@v3', 'Johnny Utah', 'Los Angeles', '555-4567', 'johnny.utah@example.com', 'normal', '1991-07-12'),
('Bodhi', 'L1v3L1f3', 'Bodhi', 'Los Angeles', '555-8901', 'bodhi@example.com', 'premium', '1991-07-12'),
('AlanParrish', 'Jum@nj1Jum@nj0', 'Alan Parrish', 'Brantford', '555-2345', 'alan.parrish@example.com', 'normal', '1995-12-15'),
('SarahHarding', 'D1n0D0ct0r', 'Sarah Harding', 'Isla Sorna', '555-6789', 'sarah.harding@example.com', 'premium', '1997-05-23'),
('FrankDrebin', 'P0l1c3Sq33ks!', 'Frank Drebin', 'Los Angeles', '555-0123', 'frank.drebin@example.com', 'normal', '1988-12-02'),
('Darkman', 'F@c3L3ssH3r0', 'Darkman', 'New York City', '555-4567', 'darkman@example.com', 'premium', '1990-08-24'),
('TonyMontana', 'SayH3ll0T0MyL1ttl3Fr13nd', 'Tony Montana', 'Miami', '555-8901', 'tony.montana@example.com', 'normal', '1983-12-09'),
('RickDeckard', '1HuntReplicants', 'Rick Deckard', 'Los Angeles', '555-2345', 'rick.deckard@example.com', 'premium', '1982-06-25'),
('SarahConnor2', 'N3v3rSt0pF1ght1ng', 'Sarah Connor', 'Los Angeles', '555-6789', 'sarah.connor2@example.com', 'normal', '1991-08-29'),
('AxelFoley', 'B3v3rlyH1llsC0p', 'Axel Foley', 'Detroit', '555-0123', 'axel.foley@example.com', 'premium', '1984-11-30'),
('HarryCallahan', 'G0Ahe@dMak3MyD@y', 'Harry Callahan', 'San Francisco', '555-4567', 'harry.callahan@example.com', 'normal', '1971-12-22'),
('DrPeterVenkman', 'Wh0Y0uG0nn@C@ll?', 'Dr. Peter Venkman', 'New York City', '555-8901', 'peter.venkman@example.com', 'premium', '1984-06-08'),
('JohnRambo', 'L!v3F0rN0th1ng0rD13F0rS0m3th1ng', 'John Rambo', 'Hope, Washington', '555-2345', 'john.rambo@example.com', 'normal', '1982-10-22'),
('SnakePlissken', 'Ey3P@tcH3d3d', 'Snake Plissken', 'New York City', '555-6789', 'snake.plissken@example.com', 'premium', '1981-07-10'),
('LisbethSalander', 'H@ck3rW1th@Dr@g0nT@tt00', 'Lisbeth Salander', 'Stockholm', '555-0123', 'lisbeth.salander@example.com', 'normal', '2009-02-27'),
('ShigeruMiyamoto', 'Sup3rM@ri0', 'Shigeru Miyamoto', 'Kyoto', '555-0123', 'shigeru.miyamoto@example.com', 'premium', '1981-07-09'),
('GusRodriguez', 'N1nt3nd0m@n14', 'Gus Rodriguez', 'Mexico City', '555-4567', 'gus.rodriguez@example.com', 'normal', '1995-01-01'),
('HideoKojima', 'M3t@lG34rS0l1d', 'Hideo Kojima', 'Tokyo', '555-8901', 'hideo.kojima@example.com', 'premium', '1986-07-13'),
('YujiNaka', 'S0n1cSp33d', 'Yuji Naka', 'Tokyo', '555-2345', 'yuji.naka@example.com', 'normal', '1991-06-23'),
('GabeNewell', 'H@lfL1f3', 'Gabe Newell', 'Bellevue', '555-6789', 'gabe.newell@example.com', 'premium', '1996-08-24'),
('JohnCarmack', 'IDTechEng1ne', 'John Carmack', 'Mesquite', '555-0123', 'john.carmack@example.com', 'normal', '1990-05-05'),
('SidMeier', 'C1v1l1z@t10n', 'Sid Meier', 'Baltimore', '555-4567', 'sid.meier@example.com', 'premium', '1982-02-01'),
('GordanFreeman', 'H@lfL1f33p1s0d3', 'Gordan Freeman', 'City 17', '555-8901', 'gordan.freeman@example.com', 'normal', '1998-11-19'),
('TimSweeney', 'UnrealEng1ne', 'Tim Sweeney', 'Cary', '555-2345', 'tim.sweeney@example.com', 'premium', '1991-05-20'),
('HironobuSakaguchi', 'F1n@lF@nt@sY', 'Hironobu Sakaguchi', 'Tokyo', '555-6789', 'hironobu.sakaguchi@example.com', 'normal', '1987-12-18'),
('JohnRomero', 'D00M3d!', 'John Romero', 'San Mateo', '555-0123', 'john.romero@example.com', 'premium', '1993-12-10'),
('GabeLogan', 'Syph3rF1lt3r', 'Gabe Logan', 'Washington, D.C.', '555-4567', 'gabe.logan@example.com', 'normal', '1999-02-02'),
('ShuheiYoshida', 'Pl@yst@t10n', 'Shuhei Yoshida', 'Tokyo', '555-8901', 'shuhei.yoshida@example.com', 'premium', '1993-12-03'),
('TetsuyaNomura', 'K1ngd0mH34rts', 'Tetsuya Nomura', 'Tokyo', '555-2345', 'tetsuya.nomura@example.com', 'normal', '1992-04-01'),
('MasahiroSakurai', 'Sup3rSm4shBr0s', 'Masahiro Sakurai', 'Tokyo', '555-6789', 'masahiro.sakurai@example.com', 'premium', '1999-04-26'),
('PhilSpencer', 'Xb0x1s1C0m1ng', 'Phil Spencer', 'Redmond', '555-0123', 'phil.spencer@example.com', 'normal', '1988-11-23'),
('PeterMolyneux', 'G0dB0t', 'Peter Molyneux', 'Guildford', '555-4567', 'peter.molyneux@example.com', 'premium', '1984-01-01'),
('KenKutaragi', 'Pl@ySt@t10n3', 'Ken Kutaragi', 'Tokyo', '555-8901', 'ken.kutaragi@example.com', 'normal', '1993-12-03'),
('SatoruIwata', 'N1nt3nd0D1r3ct', 'Satoru Iwata', 'Kyoto', '555-2345', 'satoru.iwata@example.com', 'premium', '1980-07-01'),
('DavidJaffe', 'Tw1st3dM3t@l', 'David Jaffe', 'San Diego', '555-6789', 'david.jaffe@example.com', 'normal', '1992-09-10'),
('ShinjiMikami', 'R3s1d3nt3v1l', 'Shinji Mikami', 'Tokyo', '555-0123', 'shinji.mikami@example.com', 'premium', '1990-04-22'),
('HidekiKamiya', 'B@y0n3tta', 'Hideki Kamiya', 'Osaka', '555-4567', 'hideki.kamiya@example.com', 'normal', '1998-09-11'),
('SteveWozniak', 'Appl3C0f0und3r', 'Steve Wozniak', 'Los Gatos', '555-8901', 'steve.wozniak@example.com', 'premium', '1976-04-01'),
('CliffBleszinski', 'G3@rS0fW@r', 'Cliff Bleszinski', 'Raleigh', '555-6789', 'cliff.bleszinski@example.com', 'premium', '1993-02-12'),
('DavidPerry', 'E@rthw0rmJ1m', 'David Perry', 'San Francisco', '555-0123', 'david.perry@example.com', 'normal', '1987-06-01');



````

````sql
-- Insertar datos en la tabla tipos_juegos
INSERT INTO tipos_juegos (nombre) VALUES
('Arcade'),
('FPS'),
('RPG'),
('Estrategia'),
('Deportes'),
('Aventura'),
('Plataformas'),
('Puzzle'),
('Simulacion');

-- Insertar datos en la tabla generos
INSERT INTO generos (nombre) VALUES
('Acción'),
('Aventura'),
('Disparos'),
('Estrategia'),
('Rol'),
('Deportes'),
('Plataformas'),
('Puzzle'),
('Simulacion');

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

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

---

<br>

<br>

<br>

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

---

<br>

<br>

<br>

## Insertar Datos

````sql
INSERT INTO usuarios (username, password, nombre, direccion, telefono, email, tipo_cuenta, creado_en)
VALUES
    ('admin', 'admin12345', 'Admin General del Sistema', 'Fz3r0 Gaming Extravaganza', '666-666-666', 'noob_admin@fz3r0_gaming.net', 'premium', '1998-07-11'),
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
    ('DavidPerry', 'E@rthw0rmJ1m', 'David Perry', 'San Francisco', '555-0123', 'david.perry@example.com', 'normal', '1987-06-01'),
    ('Sonic', 'G0tt@GoF@st!', 'Sonic the Hedgehog', '147 Green Hill Zone', '555-0123', 'sonic@sega.com', 'premium', '1991-06-23');

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

-- Insertar juegos de NES
INSERT INTO juegos (nombre, desarrollador, publicador, plataforma, fecha_lanzamiento, genero_id, tipo_id, costo, en_tienda_desde, stock)
VALUES
    ('Super Mario Bros.', 'Nintendo', 'Nintendo', 'NES', '1985-09-13', 1, 7, 29.99, '1985-09-13', 100),
    ('The Legend of Zelda', 'Nintendo', 'Nintendo', 'NES', '1986-02-21', 1, 7, 39.99, '1986-02-21', 50),
    ('Metroid', 'Nintendo', 'Nintendo', 'NES', '1986-08-06', 1, 7, 19.99, '1986-08-06', 75),
    ('Mega Man', 'Capcom', 'Capcom', 'NES', '1987-12-17', 1, 7, 24.99, '1987-12-17', 80),
    ('Castlevania', 'Konami', 'Konami', 'NES', '1986-09-26', 1, 7, 29.99, '1986-09-26', 60),
    ('Final Fantasy', 'Square', 'Square', 'NES', '1987-12-18', 5, 3, 39.99, '1987-12-18', 30),
    ('Donkey Kong', 'Nintendo', 'Nintendo', 'NES', '1983-07-15', 1, 7, 14.99, '1983-07-15', 90),
    ('Punch-Out!!', 'Nintendo', 'Nintendo', 'NES', '1987-11-21', 6, 5, 24.99, '1987-11-21', 70),
    ('Contra', 'Konami', 'Konami', 'NES', '1988-02-09', 1, 2, 29.99, '1988-02-09', 55),
    ('Double Dragon', 'Technos Japan', 'Tradewest', 'NES', '1988-06-02', 1, 2, 19.99, '1988-06-02', 65),
    ('Tetris', 'Nintendo', 'Nintendo', 'NES', '1988-06-14', 8, 8, 19.99, '1988-06-14', 85),
    ('Super Mario Bros. 3', 'Nintendo', 'Nintendo', 'NES', '1988-10-23', 1, 7, 34.99, '1988-10-23', 40),
    ('Zelda II: The Adventure of Link', 'Nintendo', 'Nintendo', 'NES', '1987-01-14', 1, 7, 24.99, '1987-01-14', 60),
    ('Excitebike', 'Nintendo', 'Nintendo', 'NES', '1984-11-30', 6, 1, 14.99, '1984-11-30', 95),
    ('Kid Icarus', 'Nintendo', 'Nintendo', 'NES', '1986-12-19', 1, 7, 24.99, '1986-12-19', 50),
    ('Kirby''s Adventure', 'HAL Laboratory', 'Nintendo', 'NES', '1993-05-01', 1, 7, 29.99, '1993-05-01', 70),
    ('Mega Man 2', 'Capcom', 'Capcom', 'NES', '1988-12-24', 1, 7, 24.99, '1988-12-24', 65),
    ('Super C', 'Konami', 'Konami', 'NES', '1990-02-02', 1, 2, 19.99, '1990-02-02', 80),
    ('Dragon Warrior', 'Chunsoft', 'Nintendo', 'NES', '1989-08-27', 5, 3, 24.99, '1989-08-27', 45),
    ('Mike Tyson''s Punch-Out!!', 'Nintendo', 'Nintendo', 'NES', '1987-11-21', 6, 5, 29.99, '1987-11-21', 60),
    ('Super Mario World', 'Nintendo', 'Nintendo', 'SNES', '1990-11-21', 1, 7, 29.99, '1990-11-21', 100),
    ('The Legend of Zelda: A Link to the Past', 'Nintendo', 'Nintendo', 'SNES', '1991-11-21', 1, 7, 39.99, '1991-11-21', 50),
    ('Super Metroid', 'Nintendo', 'Nintendo', 'SNES', '1994-03-19', 1, 7, 19.99, '1994-03-19', 75),
    ('Chrono Trigger', 'Square', 'Square', 'SNES', '1995-03-11', 5, 3, 49.99, '1995-03-11', 80),
    ('Super Mario Kart', 'Nintendo', 'Nintendo', 'SNES', '1992-08-27', 1, 7, 34.99, '1992-08-27', 60),
    ('Donkey Kong Country', 'Rare', 'Nintendo', 'SNES', '1994-11-21', 1, 7, 29.99, '1994-11-21', 30),
    ('Street Fighter II Turbo', 'Capcom', 'Capcom', 'SNES', '1993-07-11', 6, 2, 24.99, '1993-07-11', 90),
    ('Mega Man X', 'Capcom', 'Capcom', 'SNES', '1993-12-17', 1, 7, 29.99, '1993-12-17', 70),
    ('Final Fantasy VI', 'Square', 'Square', 'SNES', '1994-04-02', 5, 3, 39.99, '1994-04-02', 55),
    ('Secret of Mana', 'Square', 'Square', 'SNES', '1993-08-06', 5, 3, 29.99, '1993-08-06', 65),
    ('Super Mario World 2: Yoshi''s Island', 'Nintendo', 'Nintendo', 'SNES', '1995-08-05', 1, 7, 34.99, '1995-08-05', 85),
    ('Super Street Fighter II', 'Capcom', 'Capcom', 'SNES', '1993-06-25', 6, 2, 24.99, '1993-06-25', 40),
    ('F-Zero', 'Nintendo', 'Nintendo', 'SNES', '1990-11-21', 6, 1, 19.99, '1990-11-21', 60),
    ('Earthbound', 'HAL Laboratory', 'Nintendo', 'SNES', '1994-08-27', 5, 3, 39.99, '1994-08-27', 95),
    ('Super Castlevania IV', 'Konami', 'Konami', 'SNES', '1991-10-31', 1, 7, 29.99, '1991-10-31', 75),
    ('Super Punch-Out!!', 'Nintendo', 'Nintendo', 'SNES', '1994-09-14', 6, 5, 24.99, '1994-09-14', 50),
    ('Star Fox', 'Nintendo', 'Nintendo', 'SNES', '1993-02-21', 1, 7, 29.99, '1993-02-21', 80),
    ('Super Mario RPG: Legend of the Seven Stars', 'Square', 'Nintendo', 'SNES', '1996-03-09', 5, 3, 49.99, '1996-03-09', 60),
    ('Kirby Super Star', 'HAL Laboratory', 'Nintendo', 'SNES', '1996-03-21', 1, 7, 34.99, '1996-03-21', 70),
    ('Super Mario All-Stars', 'Nintendo', 'Nintendo', 'SNES', '1993-07-14', 1, 7, 29.99, '1993-07-14', 90),
    ('Super Mario 64', 'Nintendo', 'Nintendo', 'N64', '1996-06-23', 1, 7, 49.99, '1996-06-23', 100),
    ('The Legend of Zelda: Ocarina of Time', 'Nintendo', 'Nintendo', 'N64', '1998-11-23', 1, 7, 59.99, '1998-11-23', 50),
    ('GoldenEye 007', 'Rare', 'Nintendo', 'N64', '1997-08-25', 6, 2, 39.99, '1997-08-25', 75),
    ('Mario Kart 64', 'Nintendo', 'Nintendo', 'N64', '1996-12-14', 1, 7, 44.99, '1996-12-14', 80),
    ('Super Smash Bros.', 'HAL Laboratory', 'Nintendo', 'N64', '1999-01-21', 1, 7, 49.99, '1999-01-21', 60),
    ('Banjo-Kazooie', 'Rare', 'Nintendo', 'N64', '1998-06-29', 1, 7, 39.99, '1998-06-29', 30),
    ('Pokemon Stadium', 'Nintendo', 'Nintendo', 'N64', '1999-04-30', 1, 7, 49.99, '1999-04-30', 90),
    ('Donkey Kong 64', 'Rare', 'Nintendo', 'N64', '1999-11-22', 1, 7, 49.99, '1999-11-22', 70),
    ('Star Fox 64', 'Nintendo', 'Nintendo', 'N64', '1997-04-27', 1, 7, 39.99, '1997-04-27', 55),
    ('Perfect Dark', 'Rare', 'Nintendo', 'N64', '2000-05-22', 6, 2, 49.99, '2000-05-22', 65),
    ('Diddy Kong Racing', 'Rare', 'Nintendo', 'N64', '1997-11-24', 1, 7, 39.99, '1997-11-24', 85),
    ('Conker''s Bad Fur Day', 'Rare', 'Nintendo', 'N64', '2001-03-05', 1, 7, 59.99, '2001-03-05', 40),
    ('Mario Party', 'Hudson Soft', 'Nintendo', 'N64', '1998-12-18', 1, 7, 44.99, '1998-12-18', 60),
    ('The Legend of Zelda: Majora''s Mask', 'Nintendo', 'Nintendo', 'N64', '2000-04-27', 1, 7, 49.99, '2000-04-27', 60),
    ('Pokemon Snap', 'HAL Laboratory', 'Nintendo', 'N64', '1999-03-21', 1, 7, 39.99, '1999-03-21', 70),
    ('F-Zero X', 'Nintendo', 'Nintendo', 'N64', '1998-07-14', 1, 7, 39.99, '1998-07-14', 50),
    ('Yoshi''s Story', 'Nintendo', 'Nintendo', 'N64', '1997-12-21', 1, 7, 39.99, '1997-12-21', 45),
    ('Paper Mario', 'Intelligent Systems', 'Nintendo', 'N64', '2000-08-11', 5, 3, 49.99, '2000-08-11', 55),
    ('Wave Race 64', 'Nintendo', 'Nintendo', 'N64', '1996-11-01', 1, 7, 34.99, '1996-11-01', 80),
    ('Mega Man 64', 'Capcom', 'Capcom', 'N64', '2001-01-10', 1, 7, 49.99, '2001-01-10', 30),
    ('The Legend of Zelda: Breath of the Wild', 'Nintendo', 'Nintendo', 'Nintendo Switch', '2017-03-03', 1, 7, 59.99, '2017-03-03', 100),
    ('Super Mario Odyssey', 'Nintendo', 'Nintendo', 'Nintendo Switch', '2017-10-27', 1, 7, 59.99, '2017-10-27', 80),
    ('Animal Crossing: New Horizons', 'Nintendo', 'Nintendo', 'Nintendo Switch', '2020-03-20', 5, 3, 59.99, '2020-03-20', 90),
    ('Mario Kart 8 Deluxe', 'Nintendo', 'Nintendo', 'Nintendo Switch', '2017-04-28', 1, 7, 59.99, '2017-04-28', 70),
    ('Splatoon 2', 'Nintendo', 'Nintendo', 'Nintendo Switch', '2017-07-21', 1, 7, 59.99, '2017-07-21', 60),
    ('Sonic the Hedgehog', 'Sega', 'Sega', 'Sega Genesis', '1991-06-23', 1, 7, 49.99, '1991-06-23', 50),
    ('Streets of Rage 2', 'Sega', 'Sega', 'Sega Genesis', '1992-12-20', 1, 2, 39.99, '1992-12-20', 40),
    ('Golden Axe', 'Sega', 'Sega', 'Sega Genesis', '1989-12-22', 1, 2, 29.99, '1989-12-22', 30),
    ('Mortal Kombat II', 'Midway', 'Acclaim', 'Sega Genesis', '1994-04-13', 2, 1, 39.99, '1994-04-13', 50),
    ('Aladdin', 'Virgin Interactive', 'Sega', 'Sega Genesis', '1993-11-11', 3, 7, 49.99, '1993-11-11', 20),
    ('Earthworm Jim', 'Shiny Entertainment', 'Playmates Interactive', 'Sega Genesis', '1994-08-02', 1, 7, 39.99, '1994-08-02', 30),
    ('Castlevania: Bloodlines', 'Konami', 'Konami', 'Sega Genesis', '1994-03-17', 4, 1, 49.99, '1994-03-17', 40),
    ('Ecco the Dolphin', 'Novotrade International', 'Sega', 'Sega Genesis', '1992-07-29', 5, 7, 29.99, '1992-07-29', 20),
    ('Gunstar Heroes', 'Treasure', 'Sega', 'Sega Genesis', '1993-09-10', 1, 2, 39.99, '1993-09-10', 30),
    ('Shining Force II', 'Camelot Software Planning', 'Sega', 'Sega Genesis', '1993-04-02', 6, 2, 49.99, '1993-04-02', 40),
    ('Sonic the Hedgehog 2', 'Sega', 'Sega', 'Sega Genesis', '1992-11-21', 1, 7, 49.99, '1992-11-21', 50),
    ('Mega Man: The Wily Wars', 'Capcom', 'Sega', 'Sega Genesis', '1994-07-16', 1, 2, 39.99, '1994-07-16', 30),
    ('Phantasy Star IV', 'Sega', 'Sega', 'Sega Genesis', '1993-12-17', 7, 1, 49.99, '1993-12-17', 40),
    ('Shinobi III: Return of the Ninja Master', 'Sega', 'Sega', 'Sega Genesis', '1993-07-23', 1, 7, 39.99, '1993-07-23', 30),
    ('Toejam & Earl', 'Johnson Voorsanger Productions', 'Sega', 'Sega Genesis', '1991-03-01', 1, 2, 29.99, '1991-03-01', 20),
    ('Sonic 3 & Knuckles', 'Sega', 'Sega', 'Sega Genesis', '1994-10-17', 1, 7, 49.99, '1994-10-17', 50),
    ('Contra: Hard Corps', 'Konami', 'Konami', 'Sega Genesis', '1994-09-15', 2, 1, 39.99, '1994-09-15', 40),
    ('Street Fighter II: Special Champion Edition', 'Capcom', 'Capcom', 'Sega Genesis', '1993-08-01', 2, 1, 49.99, '1993-08-01', 30),
    ('Mega Turrican', 'Factor 5', 'Data East', 'Sega Genesis', '1994-06-30', 1, 2, 39.99, '1994-06-30', 20),
    ('Rocket Knight Adventures', 'Konami', 'Konami', 'Sega Genesis', '1993-08-05', 1, 2, 29.99, '1993-08-05', 30),
    ('Panzer Dragoon', 'Team Andromeda', 'Sega', 'Sega Saturn', '1995-03-10', 1, 7, 59.99, '1995-03-10', 50),
    ('NiGHTS into Dreams...', 'Sonic Team', 'Sega', 'Sega Saturn', '1996-07-05', 1, 7, 49.99, '1996-07-05', 40),
    ('Virtua Fighter 2', 'Sega AM2', 'Sega', 'Sega Saturn', '1995-08-01', 2, 1, 39.99, '1995-08-01', 30),
    ('Resident Evil', 'Capcom', 'Capcom', 'Sega Saturn', '1997-07-31', 3, 7, 59.99, '1997-07-31', 20),
    ('Sega Rally Championship', 'Sega AM5', 'Sega', 'Sega Saturn', '1995-12-29', 4, 2, 49.99, '1995-12-29', 30),
    ('Guardian Heroes', 'Treasure', 'Sega', 'Sega Saturn', '1996-01-26', 1, 2, 39.99, '1996-01-26', 40),
    ('Panzer Dragoon Saga', 'Team Andromeda', 'Sega', 'Sega Saturn', '1998-01-29', 1, 7, 149.99, '1998-01-29', 20),
    ('Daytona USA', 'Sega AM2', 'Sega', 'Sega Saturn', '1995-11-22', 5, 7, 49.99, '1995-11-22', 30),
    ('Burning Rangers', 'Sonic Team', 'Sega', 'Sega Saturn', '1998-02-26', 1, 7, 79.99, '1998-02-26', 20),
    ('Shining Force III', 'Camelot Software Planning', 'Sega', 'Sega Saturn', '1997-12-11', 6, 2, 59.99, '1997-12-11', 40),
    ('Sonic 3D Blast', 'Travellers Tales', 'Sega', 'Sega Saturn', '1996-11-20', 1, 7, 39.99, '1996-11-20', 50),
    ('Street Fighter Alpha 2', 'Capcom', 'Capcom', 'Sega Saturn', '1996-05-03', 2, 1, 49.99, '1996-05-03', 30),
    ('Dragon Force', 'Sega', 'Sega', 'Sega Saturn', '1996-06-21', 7, 2, 69.99, '1996-06-21', 40),
    ('Shinobi Legions', 'Sega', 'Sega', 'Sega Saturn', '1995-08-04', 1, 2, 39.99, '1995-08-04', 20),
    ('Mega Man 8', 'Capcom', 'Capcom', 'Sega Saturn', '1997-02-28', 2, 1, 59.99, '1997-02-28', 30),
    ('Darius Gaiden', 'Taito', 'Acclaim', 'Sega Saturn', '1995-10-27', 1, 7, 49.99, '1995-10-27', 20),
    ('Panzerspiel', 'Sega', 'Sega', 'Sega Saturn', '1996-03-22', 2, 1, 39.99, '1996-03-22', 30),
    ('Astal', 'Sony Music Entertainment Japan', 'Sega', 'Sega Saturn', '1995-06-30', 1, 2, 49.99, '1995-06-30', 40),
    ('Myst', 'Cyan', 'Sunsoft', 'Sega Saturn', '1995-06-30', 8, 1, 59.99, '1995-06-30', 20),
    ('Clockwork Knight', 'Sega', 'Sega', 'Sega Saturn', '1994-12-16', 1, 2, 29.99, '1994-12-16', 30),
    ('Sonic Adventure', 'Sonic Team', 'Sega', 'Dreamcast', '1998-12-23', 1, 7, 49.99, '1998-12-23', 50),
    ('Resident Evil Code: Veronica', 'Capcom', 'Capcom', 'Dreamcast', '2000-02-03', 3, 7, 59.99, '2000-02-03', 40),
    ('Crazy Taxi', 'Hitmaker', 'Sega', 'Dreamcast', '1999-01-24', 1, 2, 39.99, '1999-01-24', 30),
    ('Shenmue', 'Sega AM2', 'Sega', 'Dreamcast', '1999-12-29', 1, 2, 49.99, '1999-12-29', 20),
    ('Soulcalibur', 'Project Soul', 'Namco', 'Dreamcast', '1999-08-05', 2, 1, 49.99, '1999-08-05', 30),
    ('Jet Set Radio', 'Smilebit', 'Sega', 'Dreamcast', '2000-06-29', 1, 7, 39.99, '2000-06-29', 40),
    ('Grandia II', 'Game Arts', 'Ubisoft', 'Dreamcast', '2000-08-03', 6, 2, 59.99, '2000-08-03', 30),
    ('Skies of Arcadia', 'Overworks', 'Sega', 'Dreamcast', '2000-12-22', 6, 2, 59.99, '2000-12-22', 40),
    ('Marvel vs. Capcom 2: New Age of Heroes', 'Capcom', 'Capcom', 'Dreamcast', '2000-03-30', 2, 1, 59.99, '2000-03-30', 20),
    ('Power Stone', 'Capcom', 'Capcom', 'Dreamcast', '1999-12-21', 1, 2, 39.99, '1999-12-21', 30),
    ('Soul Reaver: Legacy of Kain', 'Crystal Dynamics', 'Eidos Interactive', 'Dreamcast', '1999-08-16', 7, 2, 49.99, '1999-08-16', 40),
    ('Phantasy Star Online', 'Sonic Team', 'Sega', 'Dreamcast', '2000-12-21', 5, 1, 49.99, '2000-12-21', 30),
    ('Crazy Taxi 2', 'Hitmaker', 'Sega', 'Dreamcast', '2001-05-28', 1, 2, 39.99, '2001-05-28', 40),
    ('Street Fighter III: Third Strike', 'Capcom', 'Capcom', 'Dreamcast', '1999-08-30', 2, 1, 49.99, '1999-08-30', 20),
    ('Skies of Arcadia Legends', 'Overworks', 'Sega', 'Dreamcast', '2002-01-27', 6, 2, 59.99, '2002-01-27', 30),
    ('Resident Evil 3: Nemesis', 'Capcom', 'Capcom', 'Dreamcast', '2000-08-24', 3, 7, 59.99, '2000-08-24', 20),
    ('Sonic Adventure 2', 'Sonic Team', 'Sega', 'Dreamcast', '2001-06-23', 1, 7, 49.99, '2001-06-23', 40),
    ('Shenmue II', 'Sega AM2', 'Sega', 'Dreamcast', '2001-09-06', 1, 2, 49.99, '2001-09-06', 30),
    ('Jet Grind Radio', 'Smilebit', 'Sega', 'Dreamcast', '2000-10-30', 1, 7, 39.99, '2000-10-30', 20),
    ('Dead or Alive 2', 'Team Ninja', 'Tecmo', 'Dreamcast', '2000-03-30', 2, 1, 49.99, '2000-03-30', 30),
    ('The Witcher 3: Wild Hunt', 'CD Projekt Red', 'CD Projekt', 'PC', '2015-05-19', 2, 1, 59.99, '2015-05-19', 50),
    ('Grand Theft Auto V', 'Rockstar North', 'Rockstar Games', 'PC', '2015-04-14', 1, 7, 59.99, '2015-04-14', 50),
    ('PlayerUnknown''s Battlegrounds', 'PUBG Corporation', 'PUBG Corporation', 'PC', '2017-12-20', 1, 2, 29.99, '2017-12-20', 50),
    ('Minecraft', 'Mojang Studios', 'Mojang Studios', 'PC', '2011-11-18', 7, 2, 26.95, '2011-11-18', 50),
    ('Fortnite', 'Epic Games', 'Epic Games', 'PC', '2017-07-25', 1, 2, 0, '2017-07-25', 50),
    ('Among Us', 'InnerSloth', 'InnerSloth', 'PC', '2018-11-16', 7, 2, 4.99, '2018-11-16', 50),
    ('Fallout 4', 'Bethesda Game Studios', 'Bethesda Softworks', 'PC', '2015-11-10', 2, 1, 29.99, '2015-11-10', 50),
    ('League of Legends', 'Riot Games', 'Riot Games', 'PC', '2009-10-27', 1, 2, 0, '2009-10-27', 50),
    ('Counter-Strike: Global Offensive', 'Valve Corporation', 'Valve Corporation', 'PC', '2012-08-21', 1, 2, 0, '2012-08-21', 50),
    ('Overwatch', 'Blizzard Entertainment', 'Blizzard Entertainment', 'PC', '2016-05-24', 1, 2, 39.99, '2016-05-24', 50),
    ('The Last of Us', 'Naughty Dog', 'Sony Computer Entertainment', 'PS3', '2013-06-14', 2, 1, 29.99, '2013-06-14', 30),
    ('Uncharted 2: Among Thieves', 'Naughty Dog', 'Sony Computer Entertainment', 'PS3', '2009-10-13', 2, 1, 19.99, '2009-10-13', 30),
    ('Red Dead Redemption', 'Rockstar San Diego', 'Rockstar Games', 'PS3', '2010-05-18', 1, 7, 19.99, '2010-05-18', 30),
    ('Metal Gear Solid 4: Guns of the Patriots', 'Kojima Productions', 'Konami', 'PS3', '2008-06-12', 2, 1, 19.99, '2008-06-12', 30),
    ('God of War III', 'Santa Monica Studio', 'Sony Computer Entertainment', 'PS3', '2010-03-16', 2, 1, 19.99, '2010-03-16', 30),
    ('Batman: Arkham City', 'Rocksteady Studios', 'Warner Bros. Interactive Entertainment', 'PS3', '2011-10-18', 1, 7, 19.99, '2011-10-18', 30),
    ('Uncharted 3: Drake''s Deception', 'Naughty Dog', 'Sony Computer Entertainment', 'PS3', '2011-11-01', 2, 1, 19.99, '2011-11-01', 30),
    ('Journey', 'Thatgamecompany', 'Sony Computer Entertainment', 'PS3', '2012-03-13', 7, 2, 14.99, '2012-03-13', 30),
    ('BioShock', '2K Boston', '2K Games', 'PS3', '2008-08-21', 1, 7, 14.99, '2008-08-21', 30),
    ('Demon''s Souls', 'FromSoftware', 'Sony Computer Entertainment', 'PS3', '2009-02-05', 2, 1, 19.99, '2009-02-05', 30),
    ('The Last of Us Part II', 'Naughty Dog', 'Sony Interactive Entertainment', 'PS4', '2020-06-19', 2, 1, 59.99, '2020-06-19', 40),
    ('God of War', 'Santa Monica Studio', 'Sony Interactive Entertainment', 'PS4', '2018-04-20', 2, 1, 39.99, '2018-04-20', 40),
    ('Marvel''s Spider-Man', 'Insomniac Games', 'Sony Interactive Entertainment', 'PS4', '2018-09-07', 1, 7, 39.99, '2018-09-07', 40),
    ('Red Dead Redemption 2', 'Rockstar Studios', 'Rockstar Games', 'PS4', '2018-10-26', 1, 7, 59.99, '2018-10-26', 40),
    ('Persona 5', 'Atlus', 'Atlus', 'PS4', '2016-09-15', 2, 1, 39.99, '2016-09-15', 40),
    ('Horizon Zero Dawn', 'Guerrilla Games', 'Sony Interactive Entertainment', 'PS4', '2017-02-28', 2, 1, 39.99, '2017-02-28', 40),
    ('Bloodborne', 'FromSoftware', 'Sony Interactive Entertainment', 'PS4', '2015-03-24', 2, 1, 19.99, '2015-03-24', 40),
    ('Uncharted 4: A Thief''s End', 'Naughty Dog', 'Sony Interactive Entertainment', 'PS4', '2016-05-10', 2, 1, 19.99, '2016-05-10', 40),
    ('The Witcher 3: Wild Hunt', 'CD Projekt Red', 'CD Projekt', 'PS4', '2015-05-19', 2, 1, 39.99, '2015-05-19', 40),
    ('Final Fantasy VII Remake', 'Square Enix', 'Square Enix', 'PS4', '2020-04-10', 2, 1, 59.99, '2020-04-10', 40),
    ('Demon''s Souls', 'Bluepoint Games / Japan Studio', 'Sony Interactive Entertainment', 'PS5', '2020-11-12', 2, 1, 69.99, '2020-11-12', 30),
    ('Marvel''s Spider-Man: Miles Morales', 'Insomniac Games', 'Sony Interactive Entertainment', 'PS5', '2020-11-12', 1, 7, 49.99, '2020-11-12', 30),
    ('Ratchet & Clank: Rift Apart', 'Insomniac Games', 'Sony Interactive Entertainment', 'PS5', '2021-06-11', 1, 7, 69.99, '2021-06-11', 30),
    ('Returnal', 'Housemarque', 'Sony Interactive Entertainment', 'PS5', '2021-04-30', 1, 2, 69.99, '2021-04-30', 30),
    ('Assassin''s Creed Valhalla', 'Ubisoft Montreal', 'Ubisoft', 'PS5', '2020-11-12', 1, 2, 59.99, '2020-11-12', 30),
    ('Resident Evil Village', 'Capcom', 'Capcom', 'PS5', '2021-05-07', 1, 7, 59.99, '2021-05-07', 30),
    ('Sackboy: A Big Adventure', 'Sumo Digital', 'Sony Interactive Entertainment', 'PS5', '2020-11-12', 1, 7, 59.99, '2020-11-12', 30),
    ('Destruction AllStars', 'Lucid Games', 'Sony Interactive Entertainment', 'PS5', '2021-02-02', 1, 2, 69.99, '2021-02-02', 30),
    ('Returnal', 'Housemarque', 'Sony Interactive Entertainment', 'PS5', '2021-04-30', 1, 2, 69.99, '2021-04-30', 30),
    ('Hitman 3', 'IO Interactive', 'IO Interactive', 'PS5', '2021-01-20', 1, 2, 59.99, '2021-01-20', 30),
    ('Halo: Combat Evolved', 'Bungie', 'Microsoft Game Studios', 'Xbox', '2001-11-15', 1, 7, 19.99, '2001-11-15', 20),
    ('Fable', 'Big Blue Box Studios', 'Microsoft Game Studios', 'Xbox', '2004-09-14', 2, 1, 19.99, '2004-09-14', 20),
    ('Ninja Gaiden', 'Team Ninja', 'Tecmo', 'Xbox', '2004-03-02', 1, 2, 19.99, '2004-03-02', 20),
    ('Project Gotham Racing 2', 'Bizarre Creations', 'Microsoft Game Studios', 'Xbox', '2003-11-17', 4, 3, 19.99, '2003-11-17', 20),
    ('Star Wars: Knights of the Old Republic', 'BioWare', 'LucasArts', 'Xbox', '2003-07-15', 3, 1, 19.99, '2003-07-15', 20),
    ('Prince of Persia: The Sands of Time', 'Ubisoft Montreal', 'Ubisoft', 'Xbox', '2003-11-18', 2, 1, 19.99, '2003-11-18', 20),
    ('Burnout 3: Takedown', 'Criterion Games', 'EA Games', 'Xbox', '2004-09-07', 4, 3, 19.99, '2004-09-07', 20),
    ('Tom Clancy''s Splinter Cell: Chaos Theory', 'Ubisoft Montreal', 'Ubisoft', 'Xbox', '2005-03-28', 1, 2, 19.99, '2005-03-28', 20),
    ('Forza Motorsport', 'Turn 10 Studios', 'Microsoft Game Studios', 'Xbox', '2005-05-03', 4, 3, 19.99, '2005-05-03', 20),
    ('Elder Scrolls III: Morrowind', 'Bethesda Game Studios', 'Bethesda Softworks', 'Xbox', '2002-06-06', 2, 1, 19.99, '2002-06-06', 20),
    ('Red Dead Redemption 2', 'Rockstar Studios', 'Rockstar Games', 'Xbox One', '2018-10-26', 1, 7, 59.99, '2018-10-26', 40),
    ('Gears 5', 'The Coalition', 'Xbox Game Studios', 'Xbox One', '2019-09-10', 1, 2, 39.99, '2019-09-10', 40),
    ('Forza Horizon 4', 'Playground Games', 'Xbox Game Studios', 'Xbox One', '2018-10-02', 4, 3, 39.99, '2018-10-02', 40),
    ('Halo: The Master Chief Collection', '343 Industries', 'Xbox Game Studios', 'Xbox One', '2014-11-11', 1, 2, 39.99, '2014-11-11', 40),
    ('Minecraft', 'Mojang Studios', 'Microsoft Studios', 'Xbox One', '2014-11-18', 7, 2, 19.99, '2014-11-18', 40),
    ('Titanfall 2', 'Respawn Entertainment', 'Electronic Arts', 'Xbox One', '2016-10-28', 1, 2, 19.99, '2016-10-28', 40),
    ('Ori and the Blind Forest', 'Moon Studios', 'Microsoft Studios', 'Xbox One', '2015-03-11', 2, 1, 19.99, '2015-03-11', 40),
    ('Resident Evil 7: Biohazard', 'Capcom', 'Capcom', 'Xbox One', '2017-01-24', 1, 7, 29.99, '2017-01-24', 40),
    ('Tom Clancy''s Rainbow Six Siege', 'Ubisoft Montreal', 'Ubisoft', 'Xbox One', '2015-12-01', 1, 2, 19.99, '2015-12-01', 40),
    ('The Witcher 3: Wild Hunt', 'CD Projekt Red', 'CD Projekt', 'Xbox One', '2015-05-19', 2, 1, 29.99, '2015-05-19', 40),
    ('Cyberpunk 2077', 'CD Projekt Red', 'CD Projekt', 'Xbox Series X', '2020-12-10', 1, 2, 59.99, '2020-12-10', 30),
    ('Assassin''s Creed Valhalla', 'Ubisoft Montreal', 'Ubisoft', 'Xbox Series X', '2020-11-10', 1, 2, 59.99, '2020-11-10', 30),
    ('Call of Duty: Black Ops Cold War', 'Treyarch / Raven Software', 'Activision', 'Xbox Series X', '2020-11-13', 1, 2, 59.99, '2020-11-13', 30),
    ('FIFA 21', 'EA Vancouver', 'Electronic Arts', 'Xbox Series X', '2020-12-04', 5, 2, 59.99, '2020-12-04', 30),
    ('Hitman 3', 'IO Interactive', 'IO Interactive', 'Xbox Series X', '2021-01-20', 1, 2, 59.99, '2021-01-20', 30),
    ('Yakuza: Like a Dragon', 'Ryu Ga Gotoku Studio', 'Sega', 'Xbox Series X', '2020-11-10', 2, 1, 59.99, '2020-11-10', 30),
    ('Resident Evil Village', 'Capcom', 'Capcom', 'Xbox Series X', '2021-05-07', 1, 7, 59.99, '2021-05-07', 30),
    ('Madden NFL 21', 'EA Tiburon', 'Electronic Arts', 'Xbox Series X', '2020-12-04', 5, 2, 59.99, '2020-12-04', 30),
    ('Watch Dogs: Legion', 'Ubisoft Toronto', 'Ubisoft', 'Xbox Series X', '2020-10-29', 1, 2, 59.99, '2020-10-29', 30),
    ('Marvel''s Avengers', 'Crystal Dynamics', 'Square Enix', 'Xbox Series X', '2020-09-04', 1, 2, 59.99, '2020-09-04', 30);

-- Insertar datos en la tabla consolas
INSERT INTO consolas (nombre, fabricante, generacion, codigo, fecha_lanzamiento, costo, en_tienda_desde, stock) VALUES
    ('Nintendo Entertainment System', 'Nintendo', 3, 'NES', '1983-07-15', 199.99, '1983-07-15', 50),
    ('Super Nintendo Entertainment System', 'Nintendo', 4, 'SNES', '1990-11-21', 249.99, '1990-11-21', 40),
    ('Nintendo 64', 'Nintendo', 5, 'N64', '1996-06-23', 199.99, '1996-06-23', 30),
    ('Nintendo Switch', 'Nintendo', 8, 'Switch', '2017-03-03', 299.99, '2017-03-03', 20),
    ('Sega Genesis', 'Sega', 4, 'Genesis', '1988-10-29', 189.99, '1988-10-29', 40),
    ('Sega Saturn', 'Sega', 5, 'Saturn', '1994-11-22', 399.99, '1994-11-22', 30),
    ('Sega Dreamcast', 'Sega', 6, 'Dreamcast', '1998-11-27', 199.99, '1998-11-27', 20),
    ('PC', 'Varios', 8, 'PC', '2000-01-01', 999.99, '2000-01-01', 10),
    ('PlayStation 3', 'Sony', 7, 'PS3', '2006-11-11', 299.99, '2006-11-11', 25),
    ('PlayStation 4', 'Sony', 8, 'PS4', '2013-11-15', 399.99, '2013-11-15', 20),
    ('PlayStation 5', 'Sony', 9, 'PS5', '2020-11-12', 499.99, '2020-11-12', 15),
    ('Xbox', 'Microsoft', 6, 'Xbox', '2001-11-15', 299.99, '2001-11-15', 25),
    ('Xbox 360', 'Microsoft', 7, 'Xbox360', '2005-11-22', 299.99, '2005-11-22', 20),
    ('Xbox One', 'Microsoft', 8, 'XboxOne', '2013-11-22', 499.99, '2013-11-22', 15),
    ('Xbox One X', 'Microsoft', 8, 'XboxOneX', '2017-11-07', 499.99, '2017-11-07', 10),
    ('Xbox Series X', 'Microsoft', 9, 'XboxSeriesX', '2020-11-10', 499.99, '2020-11-10', 10),
    ('Nintendo Game Boy', 'Nintendo', 4, 'GameBoy', '1989-04-21', 89.99, '1989-04-21', 30),
    ('Sony PlayStation', 'Sony', 5, 'PS1', '1994-12-03', 299.99, '1994-12-03', 25),
    ('Nintendo GameCube', 'Nintendo', 6, 'GameCube', '2001-09-14', 199.99, '2001-09-14', 20),
    ('Nintendo Wii', 'Nintendo', 7, 'Wii', '2006-11-19', 249.99, '2006-11-19', 15),
    ('Nintendo Wii U', 'Nintendo', 8, 'WiiU', '2012-11-18', 299.99, '2012-11-18', 10),
    ('Nintendo 3DS', 'Nintendo', 8, '3DS', '2011-02-26', 199.99, '2011-02-26', 10),
    ('Nintendo DS', 'Nintendo', 7, 'DS', '2004-11-21', 149.99, '2004-11-21', 15),
    ('Sony PlayStation 2', 'Sony', 6, 'PS2', '2000-03-04', 299.99, '2000-03-04', 20),
    ('Sony PlayStation Portable', 'Sony', 7, 'PSP', '2004-12-12', 199.99, '2004-12-12', 15),
    ('Sony PlayStation Vita', 'Sony', 8, 'PSVita', '2011-12-17', 249.99, '2011-12-17', 10),
    ('Microsoft Xbox One S', 'Microsoft', 8, 'XboxOneS', '2016-08-02', 299.99, '2016-08-02', 15),
    ('Microsoft Xbox Series S', 'Microsoft', 9, 'XboxSeriesS', '2020-11-10', 299.99, '2020-11-10', 10),
    ('Sega Game Gear', 'Sega', 4, 'GameGear', '1990-10-06', 149.99, '1990-10-06', 20),
    ('Atari 2600', 'Atari', 2, 'Atari2600', '1977-09-11', 199.99, '1977-09-11', 30),
    ('Neo Geo', 'SNK', 4, 'NeoGeo', '1990-04-26', 649.99, '1990-04-26', 10),
    ('Commodore 64', 'Commodore', 3, 'C64', '1982-08-01', 595.99, '1982-08-01', 5);

COMMIT;


````

## Creador de Ventas

- El script genera registros de venta aleatorios en la tabla "ventas".
- Cada registro tiene un ID de usuario aleatorio y una fecha de venta aleatoria.
- Selecciona aleatoriamente un ID de juego o un ID de consola (pero no ambos) y los asigna a las columnas correspondientes en la tabla de ventas.
- Elimina los registros donde tanto el ID de juego como el ID de consola son nulos.
- Esto garantiza que al menos una de las columnas tenga un valor no nulo en cada registro de venta.

````sql
-- Creador de ventas automatizado

INSERT INTO ventas (usuario_id, juego_id, consola_id, fecha_venta)
SELECT
    FLOOR(RAND() * 96) + 1 AS usuario_id,
    IF(FLOOR(RAND() * 2) = 0, (SELECT juego_id FROM juegos ORDER BY RAND() LIMIT 1), NULL) AS juego_id,
    IF(FLOOR(RAND() * 2) = 0, (SELECT consola_id FROM consolas ORDER BY RAND() LIMIT 1), NULL) AS consola_id,
    DATE_ADD('2020-01-01', INTERVAL FLOOR(RAND() * 1300) DAY) AS fecha_venta
FROM
    information_schema.tables AS t1,
    information_schema.tables AS t2
WHERE
    ((SELECT COUNT(*) FROM juegos) > 0 OR (SELECT COUNT(*) FROM consolas) > 0)
LIMIT 500;

DELETE FROM ventas
WHERE juego_id IS NULL AND consola_id IS NULL;

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





````sql
-- Buscar todos usuarios con username que contenga el string "admin"
SELECT * FROM usuarios WHERE username LIKE '%admin%';

-- Buscar todos usuarios con username = "admin"
SELECT * FROM usuarios WHERE username = 'admin';

-- Consulta: Obtener el nombre y la dirección de todos los usuarios
SELECT username,password,nombre,direccion FROM usuarios;

-- Consulta: Contar la cantidad de juegos de acción
SELECT COUNT(*) AS total_juegos_accion FROM juegos WHERE genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción');

-- Consulta: Filtrar las consolas de última generación
SELECT * FROM consolas WHERE generacion = (SELECT MAX(generacion) FROM consolas);

-- Consulta: Obtener el juego más reciente por fecha de lanzamiento
SELECT * FROM juegos ORDER BY fecha_lanzamiento DESC LIMIT 1;

-- Consulta: Calcular el precio máximo de los juegos
SELECT MAX(costo) AS precio_maximo FROM juegos;

-- Consulta: Obtener el nombre y el stock de las consolas ordenadas por nombre de forma ascendente
SELECT nombre, stock FROM consolas ORDER BY nombre ASC;

-- Consulta: Filtrar los juegos publicados por un desarrollador específico
SELECT * FROM juegos WHERE desarrollador = 'Nombre del desarrollador';

-- Consulta: Obtener la fecha de lanzamiento más antigua de todas las consolas
SELECT MIN(fecha_lanzamiento) AS fecha_lanzamiento_mas_antigua FROM consolas;

-- Consulta: Contar la cantidad de usuarios con cuenta premium
SELECT COUNT(*) AS total_usuarios_premium FROM usuarios WHERE tipo_cuenta = 'premium';

-- Consulta: Filtrar los juegos con stock agotado
SELECT * FROM juegos WHERE stock = 0;

-- Consulta: Promedio de precio de los juegos
SELECT AVG(costo) AS promedio_precios FROM juegos;


````

---

````sql
-- Buscar todos los juegos de "rol" 
SELECT j.*
FROM juegos AS j
INNER JOIN generos AS g ON j.genero_id = g.genero_id
WHERE g.nombre = 'Rol';

-- Obtener todas las ventas junto con los detalles del juego y el usuario
SELECT v.*, j.nombre AS juego, u.username AS usuario
FROM ventas AS v
LEFT JOIN juegos AS j ON v.juego_id = j.juego_id
INNER JOIN usuarios AS u ON v.usuario_id = u.usuario_id;

-- Todos los juegos de rol comprados
SELECT j.nombre AS juego
FROM juegos j
JOIN ventas v ON j.juego_id = v.juego_id
WHERE j.genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Rol');

-- Todos los juegos de rol comprados por el usuario "JohnCarmack"
SELECT j.nombre AS juego
FROM juegos j
JOIN ventas v ON j.juego_id = v.juego_id
JOIN usuarios u ON v.usuario_id = u.usuario_id
WHERE j.genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Rol')
  AND u.username = 'JohnCarmack';

-- Número total de juegos de disparos comprados por cada usuario
SELECT u.username, COUNT(*) AS total_juegos_disparos
FROM juegos j
JOIN ventas v ON j.juego_id = v.juego_id
JOIN usuarios u ON v.usuario_id = u.usuario_id
WHERE j.genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Disparos')
GROUP BY u.username;

-- Juegos más caros de cada género
SELECT g.nombre AS genero, j.nombre AS juego, j.costo
FROM juegos j
JOIN generos g ON j.genero_id = g.genero_id
WHERE j.costo = (SELECT MAX(costo) FROM juegos WHERE genero_id = g.genero_id);

-- Total gastado por cada usuario en juegos de acción
SELECT u.username, SUM(j.costo) AS total_gastado
FROM juegos j
JOIN ventas v ON j.juego_id = v.juego_id
JOIN usuarios u ON v.usuario_id = u.usuario_id
WHERE j.genero_id = (SELECT genero_id FROM generos WHERE nombre = 'Acción')
GROUP BY u.username;

-- Juegos con stock <= 10 y disponibles desde hace más de 1 año
SELECT nombre
FROM juegos
WHERE stock <= 10 AND en_tienda_desde <= DATE_SUB(NOW(), INTERVAL 1 YEAR);

-- Usuarios que han comprado juegos de aventura y estrategia
SELECT u.nombre
FROM usuarios u
JOIN ventas v ON u.usuario_id = v.usuario_id
JOIN juegos j ON v.juego_id = j.juego_id
JOIN generos g ON j.genero_id = g.genero_id
WHERE g.nombre IN ('Aventura', 'Estrategia');

-- Juegos publicados y desarrollados por la misma empresa
SELECT nombre
FROM juegos
WHERE desarrollador = publicador;

-- Cantidad total de juegos vendidos por consola
SELECT c.nombre AS consola, SUM(IFNULL(v.juego_id, 0) + IFNULL(v.consola_id, 0)) AS total_juegos_vendidos
FROM consolas c
LEFT JOIN ventas v ON c.consola_id = v.consola_id
GROUP BY c.consola_id;

-- Juegos lanzados antes de la fecha de lanzamiento promedio de todos los juegos
SELECT nombre
FROM juegos
WHERE fecha_lanzamiento < (SELECT AVG(fecha_lanzamiento) FROM juegos);

````

---

````sql
-- Top 5 usuarios que han gastado más en juegos
SELECT u.username, SUM(j.costo) AS total_gastado
FROM usuarios u
JOIN ventas v ON u.usuario_id = v.usuario_id
JOIN juegos j ON v.juego_id = j.juego_id
GROUP BY u.usuario_id
ORDER BY total_gastado DESC
LIMIT 5;

-- Cantidad promedio de juegos vendidos por usuario
SELECT AVG(cantidad_juegos) AS promedio_juegos_vendidos
FROM (SELECT COUNT(*) AS cantidad_juegos
      FROM ventas
      GROUP BY usuario_id) AS subquery;

-- Juegos que han estado en tienda por más de 6 meses y todavía tienen stock
SELECT nombre
FROM juegos
WHERE en_tienda_desde <= DATE_SUB(NOW(), INTERVAL 6 MONTH)
  AND stock > 0;

-- Cantidad de juegos vendidos por género y mes
SELECT g.nombre AS genero, MONTH(v.fecha_venta) AS mes, COUNT(*) AS cantidad_juegos_vendidos
FROM generos g
JOIN juegos j ON g.genero_id = j.genero_id
JOIN ventas v ON j.juego_id = v.juego_id
GROUP BY g.genero_id, MONTH(v.fecha_venta)
ORDER BY g.nombre, mes;

-- Total de ventas por año y mes
SELECT YEAR(fecha_venta) AS anio, MONTH(fecha_venta) AS mes, COUNT(*) AS total_ventas
FROM ventas
GROUP BY anio, mes
ORDER BY anio, mes;

-- Juegos con un precio superior al promedio de todos los juegos
SELECT nombre, costo
FROM juegos
WHERE costo > (SELECT AVG(costo) FROM juegos);

-- Número de ventas mensuales para cada consola en el año 2022
SELECT c.nombre AS consola, MONTH(v.fecha_venta) AS mes, COUNT(*) AS total_ventas
FROM consolas c
JOIN ventas v ON c.consola_id = v.consola_id
WHERE YEAR(v.fecha_venta) = 2022
GROUP BY c.consola_id, mes
ORDER BY c.nombre, mes;

-- Total de ingresos por mes en el año 2021
SELECT MONTH(fecha_venta) AS mes, SUM(j.costo) AS total_ingresos
FROM ventas v
JOIN juegos j ON v.juego_id = j.juego_id
WHERE YEAR(fecha_venta) = 2021
GROUP BY mes
ORDER BY mes;

-- Top 5 juegos más vendidos de todos los tiempos
SELECT j.nombre AS juego, COUNT(*) AS total_ventas
FROM juegos j
JOIN ventas v ON j.juego_id = v.juego_id
GROUP BY j.juego_id
ORDER BY total_ventas DESC
LIMIT 5;

-- Usuarios que han comprado todos los juegos de un género específico
SELECT u.username
FROM usuarios u
JOIN (SELECT usuario_id, COUNT(DISTINCT juego_id) AS total_juegos
      FROM ventas
      GROUP BY usuario_id) AS subquery ON u.usuario_id = subquery.usuario_id
WHERE total_juegos = (SELECT COUNT(*) FROM juegos WHERE genero_id = 1);

-- Cálculo del costo promedio de los juegos por género
SELECT g.nombre AS genero, AVG(j.costo) AS costo_promedio
FROM generos g
JOIN juegos j ON g.genero_id = j.genero_id
GROUP BY g.genero_id
ORDER BY costo_promedio DESC;

-- Consulta de los juegos más populares basados en el número de ventas
SELECT j.nombre AS juego, COUNT(*) AS total_ventas
FROM juegos j
JOIN ventas v ON j.juego_id = v.juego_id
GROUP BY j.juego_id
ORDER BY total_ventas DESC
LIMIT 5;

-- Consulta de los usuarios con mayor número de compras
SELECT u.username, COUNT(*) AS total_compras
FROM usuarios u
JOIN ventas v ON u.usuario_id = v.usuario_id
GROUP BY u.usuario_id
ORDER BY total_compras DESC
LIMIT 5;

-- Consulta de los juegos que tienen el mayor stock disponible
SELECT j.nombre AS juego, j.stock
FROM juegos j
ORDER BY j.stock DESC
LIMIT 5;

-- Consulta de los juegos más recientes lanzados por cada desarrollador
SELECT j.nombre AS juego, j.desarrollador, j.fecha_lanzamiento
FROM juegos j
JOIN (
    SELECT desarrollador, MAX(fecha_lanzamiento) AS ultima_fecha
    FROM juegos
    GROUP BY desarrollador
) AS ultimos ON j.desarrollador = ultimos.desarrollador AND j.fecha_lanzamiento = ultimos.ultima_fecha;


````


---

## Complejos

### Cálculo Analítico

- Este query calcula el promedio de gasto por usuario en juegos vendidos, considerando el stock de cada juego.
- También incluye otras columnas como el nombre de usuario, el total de ventas, el total de stock y el nivel de stock (alto o bajo) basado en un límite de 100.
- Los resultados están ordenados por promedio de gasto descendente y solo se incluyen los usuarios con más de 5 ventas.

````sql
SELECT
    CONCAT(u.nombre, ' (', u.username, ')') AS usuario,
    COUNT(DISTINCT v.venta_id) AS total_ventas,
    SUM(j.stock) AS total_stock,
    IF(SUM(j.stock) > 100, 'Alto', 'Bajo') AS nivel_stock,
    CASE
        WHEN u.tipo_cuenta = 'premium' THEN 'VIP'
        ELSE 'Normal'
    END AS tipo_cuenta,
    ROUND(SUM(j.costo * j.stock) / COUNT(DISTINCT v.venta_id), 2) AS promedio_gasto
FROM
    usuarios u
JOIN
    ventas v ON u.usuario_id = v.usuario_id
JOIN
    juegos j ON v.juego_id = j.juego_id
GROUP BY
    u.usuario_id
HAVING
    total_ventas > 5
ORDER BY
    promedio_gasto DESC;

````

---

### Calculo 2 

- Este query busca usuarios que hayan realizado ventas de juegos del género con ID 1 y que hayan comprado consolas del fabricante "Sony". Se agrupan los resultados por usuario y se calcula el total de ventas, el total gastado y el promedio de gasto.
- Luego, se filtran aquellos usuarios cuyo total gastado sea mayor a 100 y se ordenan los resultados por el total de ventas en orden descendente.

````sql
SELECT
    u.nombre AS usuario,
    COUNT(DISTINCT v.venta_id) AS total_ventas,
    SUM(j.costo) AS total_gastado,
    AVG(j.costo) AS promedio_gasto
FROM
    usuarios u
    LEFT JOIN ventas v ON u.usuario_id = v.usuario_id
    LEFT JOIN juegos j ON v.juego_id = j.juego_id
    LEFT JOIN consolas c ON v.consola_id = c.consola_id
WHERE
    j.genero_id = 1
    AND c.fabricante = 'Sony'
GROUP BY
    u.usuario_id
HAVING
    total_gastado > 100
ORDER BY
    total_ventas DESC;

````

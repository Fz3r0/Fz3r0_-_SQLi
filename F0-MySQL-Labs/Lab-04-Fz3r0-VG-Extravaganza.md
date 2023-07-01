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
-- Inserción de datos de prueba en la tabla 'usuarios'
INSERT INTO usuarios (username, password, name, address, phone, mail, subscription_type, created_at)
VALUES
  ('ItsaMeMario', 'M4r10Br0s', 'Mario Mario', '123 Mushroom Kingdom', '555-1234', 'mario_plumber@nintendo.jp', 'premium', '1985-09-13'),
  ('GottaGoFast', 'S0n1cH3dg3h0g', 'Sonic Hedgehog', 'Green Hill Zone', '555-5678', 'sonic@sega.com', 'premium', '1991-06-23'),
  ('MasterSword', 'Hyrul3', 'Link Hyrule', 'Kakariko Village', '555-9012', 'link@zelda.com', 'premium', '1986-02-21'),
  ('PowerSuit', 'Hunt3rX', 'Samus Aran', 'Zebes', '555-3456', 'samus@metroid.com', 'premium', '1986-08-06'),
  ('BlueBomber', 'R0ckmanX', 'Mega Man Light', 'Dr. Light Labs', '555-7890', 'megaman@capcom.com', 'premium', '1987-12-17'),
  ('BananaMan', 'JungleK1ng', 'Donkey Kong Kong', 'DK Island', '555-2345', 'dkong@nintendo.jp', 'premium', '1981-07-09'),
  ('WakaWaka', 'Gh0stlyPursu1t', 'Pac-Man Man', 'Pac-Maze', '555-6789', 'pacman@namco.com', 'premium', '1980-05-22'),
  ('TombRaider', 'Unchart3d', 'Lara Croft Croft', 'Croft Manor', '555-0123', 'lara@tombraider.com', 'premium', '1996-10-25'),
  ('HailToTheKing', 'Duk3Nuk3mF0r3v3r', 'Duke Nukem Nukem', 'Los Angeles', '555-4567', 'duke@3drealms.com', 'premium', '1991-07-01'),
  ('HalfLifeHero', 'GManConsp1racy', 'Gordon Freeman Freeman', 'City 17', '555-8901', 'gordon@valvesoftware.com', 'premium', '1998-11-19'),
  ('StealthEspionage', 'L1qu1dSnak3', 'Solid Snake Snake', 'Shadow Moses Island', '555-2345', 'snake@konami.com', 'premium', '1987-07-13'),
  ('MakoReact', 'SwordOfDestr0y', 'Cloud Strife Strife', 'Midgar', '555-6789', 'cloud@square-enix.com', 'premium', '1997-01-31'),
  ('GodOfWar', 'SpartanRage', 'Kratos Godofwar', 'Sparta', '555-0123', 'kratos@godofwar.com', 'premium', '2005-03-22'),
  ('ShadowClaw', 'Sh0ryuken!', 'Ryu Streetfighter', 'Japan', '555-4567', 'ryu@capcom.com', 'premium', '1987-08-30'),
  ('MysticNinja', 'GanbareGoem0n', 'Goemon Ishikawa', 'Edo', '555-8901', 'goemon@konami.com', 'premium', '1986-08-19'),
  ('TimeLord', 'Tim3ywim3y', 'Doctor Who Who', 'TARDIS', '555-2345', 'doctor@bbc.co.uk', 'premium', '1963-11-23'),
  ('OneRingBearer', 'M0rdorAdventures', 'Frodo Baggins', 'The Shire', '555-6789', 'frodo@lotr.com', 'premium', '1954-07-29'),
  ('CapedCrusader', 'B@tSign@l', 'Bruce Wayne', 'Wayne Manor', '555-0123', 'batman@dc.com', 'premium', '1939-05-01'),
  ('ManOfSteel', 'Krypt0n1teF0e', 'Clark Kent', 'Metropolis', '555-4567', 'superman@dc.com', 'premium', '1938-06-01'),
  ('WebSlinger', 'WithGreatP0wer', 'Peter Parker', 'New York City', '555-8901', 'spiderman@marvel.com', 'premium', '1962-08-10'),
  ('MutantHero', 'C0wabung4', 'Leonardo Hamato', 'Sewers', '555-2345', 'leonardo@tmnt.com', 'premium', '1984-05-01'),
  ('CapAm', 'AvengersAssemble', 'Steve Rogers', 'Brooklyn', '555-6789', 'captainamerica@marvel.com', 'premium', '1941-03-01'),
  ('MutantNinja', 'Turtl3P0w3r!', 'Michelangelo Hamato', 'Sewers', '555-0123', 'michelangelo@tmnt.com', 'premium', '1984-05-01'),
  ('DarkKnight', 'TheNightIsD@rk', 'Bruce Wayne', 'Gotham City', '555-4567', 'batman@dc.com', 'premium', '1939-05-01'),
  ('JadeEmpress', 'AncientW4rrior', 'Kitana Edenia', 'Outworld', '555-8901', 'kitana@netherrealm.com', 'premium', '1993-10-08'),
  ('HeadshotMaster', 'Sn1p3rElit3', 'Tom Berenger', 'Vietnam', '555-2345', 'thomas@platoon.com', 'premium', '1986-12-19'),
  ('EctoplasmicHero', 'WhoYaGonnaC@ll?', 'Peter Venkman', 'New York City', '555-6789', 'peter@ghostbusters.com', 'premium', '1984-06-08'),
  ('DetectiveMode', 'Th3W0rldN3eds', 'Sherlock Holmes', '221B Baker Street', '555-0123', 'sherlock@bakerstreet.com', 'premium', '1887-11-01'),
  ('Dragonborn', 'FusR0dah!', 'Dovahkiin Skyrim', 'Whiterun', '555-4567', 'dovahkiin@bethesda.com', 'premium', '2011-11-11'),
  ('Revenger', 'Vengeance1sMine', 'Eric Draven', 'Detroit', '555-8901', 'eric@thecrow.com', 'premium', '1989-05-13'),
  ('Agent47', 'SilentAss4ssin', 'Rupert Friend', 'Various Locations', '555-2345', 'agent47@hitman.com', 'premium', '2000-11-19'),
  ('DragonShout', 'FusRoDah!', 'Paarthurnax', 'Throat of the World', '555-6789', 'paarthurnax@skyrim.com', 'premium', '2011-11-11'),
  ('SpaceExplorer', 'T0Inf1n1ty@ndB3y0nd', 'Buzz Lightyear', 'Andy\'s Room', '555-0123', 'buzz@pixar.com', 'premium', '1995-11-22'),
  ('ClownPrince', 'H@H@H@H@H@', 'Joker Joker', 'Gotham City', '555-4567', 'joker@dc.com', 'premium', '1940-04-01'),
  ('ElderScrolls', 'Skelet0nK1ng', 'Mannimarco Necromancer', 'Tamriel', '555-8901', 'mannimarco@bethesda.com', 'premium', '1994-03-25'),
  ('BrickBreaker', 'SmashItAll!', 'Mario Arkanoid', 'Arkanoid World', '555-2345', 'mario@taito.com', 'premium', '1986-06-10'),
  ('MetalGear', 'Snak3Eater', 'Solid Snake Snake', 'Shadow Moses Island', '555-6789', 'snake@konami.com', 'premium', '1987-07-13'),
  ('StellarKnight', 'GalacticH3ro', 'Alex Rogan', 'The Last Starfighter', '555-0123', 'alex@starfighter.com', 'premium', '1984-07-13'),
  ('TimeTraveler', 'GreatSc0tt!', 'Marty McFly', 'Hill Valley', '555-4567', 'marty@mcfly.com', 'premium', '1985-07-03'),
  ('IronMan', 'H3artOfSt33l', 'Tony Stark', 'Malibu', '555-8901', 'tony@starkindustries.com', 'premium', '1963-03-01'),
  ('BlueShell', 'Ult1mateTroll', 'Koopa Troopa', 'Bowser\'s Castle', '555-2345', 'koopa@nintendo.jp', 'premium', '1985-09-13'),
  ('SaiyanPrince', 'Over9000', 'Vegeta Vegeta', 'Planet Vegeta', '555-6789', 'vegeta@dbz.com', 'premium', '1984-11-20'),
  ('KingOfKombat', 'FlawlessVictory', 'Shang Tsung Tsung', 'Outworld', '555-0123', 'shangtsung@netherrealm.com', 'premium', '1992-10-08'),
  ('Archaeologist', 'H0lyGr@il', 'Indiana Jones', 'Various Locations', '555-4567', 'indiana@archaeology.com', 'premium', '1981-06-12'),
  ('GoldenEye', 'Lic3nse2Kill', 'James Bond', 'London', '555-8901', 'bond@mi6.gov', 'premium', '1953-04-13'),
  ('GalacticHero', 'MayTheF0rce', 'Luke Skywalker', 'Tatooine', '555-2345', 'luke@starwars.com', 'premium', '1977-05-25'),
  ('ShadowThief', 'Master0fShadows', 'Garrett', 'The City', '555-6789', 'garrett@thief.com', 'premium', '1998-11-30'),
  ('BountyHunter', 'N3verT3llM3Th30dds', 'Bobba Fett', 'Kamino', '555-0123', 'bobba@starwars.com', 'premium', '1980-05-17'),
  ('PixelPainter', '8BitM4estro', 'Shigeru Miyamoto', 'Kyoto', '555-4567', 'miyamoto@nintendo.jp', 'premium', '1952-11-16'),
  ('SnakeEater', 'B1gB0ss', 'Naked Snake Snake', 'Various Locations', '555-8901', 'snakes@konami.com', 'premium', '1998-09-03'),
  ('SwordMaster', 'Mast3rSw0rd!', 'Hidemaro Fujibayashi', 'Kyoto', '555-2345', 'hidemaro@nintendo.jp', 'premium', '1970-12-31'),
  ('RetroGamer', 'PacManFever', 'Billy Mitchell', 'Florida', '555-6789', 'billy@mitchell.com', 'premium', '1965-07-16'),
  ('ConsoleWizard', 'G4m3rK1ng', 'John Carmack', 'Texas', '555-0123', 'john@carmack.com', 'premium', '1970-08-20'),
  ('WarCraft', '4z3roth', 'Arthas Menethil', 'Lordaeron', '555-4567', 'arthas@blizzard.com', 'premium', '1994-02-01'),
  ('FalconPunch', 'ShowMeY0urM0v3s', 'Captain Falcon', 'Mute City', '555-8901', 'falcon@fzero.com', 'premium', '1990-11-21'),
  ('GalagaMaster', 'S3rialSh0oter', 'Namco Galaga', 'Galaxy', '555-2345', 'galaga@namco.com', 'premium', '1981-10-01'),
  ('CandyCrusher', 'Sw33tV1ct0ry!', 'Tiffi Toffee', 'Candy Kingdom', '555-6789', 'tiffi@candycrush.com', 'premium', '2012-11-14'),
  ('NostalgiaGamer', '8BitMemories', 'Retro Ray', 'Pixel Land', '555-0123', 'retro@nostalgia.com', 'premium', '1980-01-01'),
  ('TechGuru', 'G4dgetM4niac', 'Bill Gates', 'Washington', '555-4567', 'bill@microsoft.com', 'premium', '1975-04-04'),
  ('VirtualHero', 'V1rtualW0rld', 'Hideo Kojima', 'Tokyo', '555-8901', 'kojima@kojimaproductions.jp', 'premium', '1963-08-24');

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

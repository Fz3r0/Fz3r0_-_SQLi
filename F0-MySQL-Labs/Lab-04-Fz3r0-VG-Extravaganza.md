
````sql
-- Creación de la base de datos
CREATE DATABASE IF NOT EXISTS Fz3r0_Gaming_Extravaganza CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Selección de la base de datos
USE Fz3r0_Gaming_Extravaganza;

-- Creación de la tabla 'usuarios'
CREATE TABLE usuarios (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50) NOT NULL,
  password VARCHAR(255) NOT NULL,
  name VARCHAR(100) NOT NULL,
  address VARCHAR(200) NOT NULL,
  phone VARCHAR(20) NOT NULL,
  mail VARCHAR(100) NOT NULL,
  subscription_type ENUM('basic', 'premium') NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  UNIQUE INDEX idx_username (username)
) ENGINE=InnoDB;

-- Creación de la tabla 'proveedores'
CREATE TABLE proveedores (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre_empresa VARCHAR(100) NOT NULL,
  direccion VARCHAR(200) NOT NULL,
  telefono VARCHAR(20) NOT NULL,
  correo_electronico VARCHAR(100) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) ENGINE=InnoDB;

-- Creación de la tabla 'desarrolladores'
CREATE TABLE desarrolladores (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre_empresa VARCHAR(100) NOT NULL,
  direccion VARCHAR(200) NOT NULL,
  telefono VARCHAR(20) NOT NULL,
  correo_electronico VARCHAR(100) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) ENGINE=InnoDB;

-- Creación de la tabla 'consolas'
CREATE TABLE consolas (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  descripcion TEXT,
  fabricante VARCHAR(100) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  INDEX idx_fabricante (fabricante)
) ENGINE=InnoDB;

-- Creación de la tabla 'categorias'
CREATE TABLE categorias (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  descripcion TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) ENGINE=InnoDB;

-- Creación de la tabla 'productos'
CREATE TABLE productos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  descripcion TEXT,
  precio DECIMAL(10, 2) NOT NULL,
  stock INT NOT NULL,
  proveedor_id INT,
  desarrollador_id INT,
  consola_id INT,
  categoria_id INT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  INDEX idx_proveedor_id (proveedor_id),
  INDEX idx_desarrollador_id (desarrollador_id),
  INDEX idx_consola_id (consola_id),
  INDEX idx_categoria_id (categoria_id),
  FOREIGN KEY (proveedor_id) REFERENCES proveedores(id),
  FOREIGN KEY (desarrollador_id) REFERENCES desarrolladores(id),
  FOREIGN KEY (consola_id) REFERENCES consolas(id),
  FOREIGN KEY (categoria_id) REFERENCES categorias(id)
) ENGINE=InnoDB;

-- Creación de la tabla 'ventas'
CREATE TABLE ventas (
  id INT AUTO_INCREMENT PRIMARY KEY,
  fecha_venta DATETIME NOT NULL,
  total DECIMAL(10, 2) NOT NULL,
  usuario_id INT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  INDEX idx_usuario_id (usuario_id),
  FOREIGN KEY (usuario_id) REFERENCES usuarios(id)
) ENGINE=InnoDB;

-- Creación de la tabla 'detalles_venta'
CREATE TABLE detalles_venta (
  venta_id INT,
  producto_id INT,
  cantidad INT NOT NULL,
  precio_unitario DECIMAL(10, 2) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  INDEX idx_venta_id (venta_id),
  INDEX idx_producto_id (producto_id),
  FOREIGN KEY (venta_id) REFERENCES ventas(id),
  FOREIGN KEY (producto_id) REFERENCES productos(id)
) ENGINE=InnoDB;

-- Creación de la tabla 'pedidos'
CREATE TABLE pedidos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  fecha_pedido DATETIME NOT NULL,
  total DECIMAL(10, 2) NOT NULL,
  usuario_id INT,
  direccion_entrega VARCHAR(200) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  INDEX idx_usuario_id (usuario_id),
  FOREIGN KEY (usuario_id) REFERENCES usuarios(id)
) ENGINE=InnoDB;

-- Creación de la tabla 'detalles_pedido'
CREATE TABLE detalles_pedido (
  pedido_id INT,
  producto_id INT,
  cantidad INT NOT NULL,
  precio_unitario DECIMAL(10, 2) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  INDEX idx_pedido_id (pedido_id),
  INDEX idx_producto_id (producto_id),
  FOREIGN KEY (pedido_id) REFERENCES pedidos(id),
  FOREIGN KEY (producto_id) REFERENCES productos(id)
) ENGINE=InnoDB;

-- Creación de la tabla 'juegos_retro'
CREATE TABLE juegos_retro (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  descripcion TEXT,
  precio DECIMAL(10, 2) NOT NULL,
  stock INT NOT NULL,
  proveedor_id INT,
  consola_id INT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  INDEX idx_proveedor_id (proveedor_id),
  INDEX idx_consola_id (consola_id),
  FOREIGN KEY (proveedor_id) REFERENCES proveedores(id),
  FOREIGN KEY (consola_id) REFERENCES consolas(id)
) ENGINE=InnoDB;

````





````sql
INSERT INTO usuarios (username, password, name, address, phone, mail, subscription_type)
VALUES
  ('Mario', 'ItsaMeM@rio!', 'Mario', '123 Mushroom Kingdom', '555-1234', 'mario@example.com', 'premium'),
  ('Luigi', 'Lu1g1Mansion!', 'Luigi', '456 Mushroom Kingdom', '555-5678', 'luigi@example.com', 'basic'),
  ('Link', 'Hyrul3H3r0!', 'Link', '789 Hyrule', '555-9012', 'link@example.com', 'premium'),
  ('Zelda', 'Pr1nc3ss0fW1sdom!', 'Princess Zelda', '789 Hyrule', '555-3456', 'zelda@example.com', 'premium'),
  ('MasterChief', 'Spart4n117!', 'Master Chief', '456 UNSC Headquarters', '555-7890', 'masterchief@example.com', 'basic'),
  ('Geralt', 'Witch3r@R1v1a!', 'Geralt of Rivia', '789 Kaer Morhen', '555-2345', 'geralt@example.com', 'premium'),
  ('Ezio', 'Ass4ssinCr33d!', 'Ezio Auditore', '123 Monteriggioni', '555-6789', 'ezio@example.com', 'basic'),
  ('Samus', 'M3tR0!dHunt3r!', 'Samus Aran', '456 Zebes', '555-0123', 'samus@example.com', 'premium'),
  ('Kratos', 'G0d0fW@r!', 'Kratos', '789 Sparta', '555-4567', 'kratos@example.com', 'basic'),
  ('Aloy', 'Hunt3r0fTh3N0r@!', 'Aloy', '123 Nora Tribe', '555-8901', 'aloy@example.com', 'premium'),
  ('NathanDrake', 'Unch@rt3dTr34sur3!', 'Nathan Drake', '456 Uncharted Street', '555-2345', 'nathandrake@example.com', 'basic'),
  ('Trevor', 'GTA5Ph!llips!', 'Trevor Phillips', '789 San Andreas Avenue', '555-6789', 'trevorphillips@example.com', 'premium'),
  ('Snake', 'S0lidSn@ke!', 'Solid Snake', '123 Shadow Moses Island', '555-0123', 'solidsnake@example.com', 'basic'),
  ('LaraCroft', 'T0mbRa1d3r!', 'Lara Croft', '456 Croft Manor', '555-4567', 'laracroft@example.com', 'premium'),
  ('Joel', 'L3gacy0fU5!', 'Joel Miller', '789 Jackson County', '555-8901', 'joelmiller@example.com', 'basic'),
  ('GusRodriguez', 'N1nt3nd0m@n14!', 'Gus Rodruguez', '789 Mexico City', '555-2345', 'gus@example.com', 'premium'),
  ('Miyamoto', 'Sup3rM@rio64!', 'Shigeru Miyamoto', '123 Kyoto', '555-6789', 'miyamoto@example.com', 'basic'),
  ('HideoKojima', 'K0j1m@Sn@k3!', 'Hideo Kojima', '456 Tokyo', '555-0123', 'kojima@example.com', 'premium'),
  ('Tidus', 'F1n4lF@nt4syX!', 'Tidus', '789 Zanarkand', '555-4567', 'tidus@example.com', 'basic'),
  ('Yuna', 'S3ndM3t0th3F@rpl@n3t!', 'Yuna', '123 Besaid Island', '555-8901', 'yuna@example.com', 'premium'),
  ('Sonic', 'G0ttag0f4st!', 'Sonic the Hedgehog', '456 Green Hill Zone', '555-2345', 'sonic@example.com', 'basic'),
  ('Tifa', 'F1n4lF@nt4syVII!', 'Tifa Lockhart', '789 Midgar', '555-6789', 'tifa@example.com', 'premium'),
  ('Cloud', 'BusterSw0rd!', 'Cloud Strife', '123 Nibelheim', '555-0123', 'cloud@example.com', 'basic'),
  ('JoannaDark', 'P3rf3ctD@rk!', 'Joanna Dark', '456 Carrington Institute', '555-4567', 'joannadark@example.com', 'premium'),
  ('Leon', 'R3sid3nt3v1l!', 'Leon S. Kennedy', '789 Raccoon City', '555-8901', 'leon@example.com', 'basic'),
  ('Jill', 'ST@R5!', 'Jill Valentine', '123 Racoon City', '555-2345', 'jill@example.com', 'premium'),
  ('MarcusFenix', 'G3@rs0fW@r!', 'Marcus Fenix', '456 Jacinto City', '555-6789', 'marcusfenix@example.com', 'basic'),
  ('Ellie', 'L4st0fU5!', 'Ellie Williams', '789 Jackson County', '555-0123', 'ellie@example.com', 'premium'),
  ('Doomguy', 'R1pAndT3ar!', 'Doomguy', '123 Mars', '555-4567', 'doomguy@example.com', 'basic'),
  ('Aloy', 'Zer0D@wn!', 'Aloy', '456 Nora Tribe', '555-8901', 'aloy@example.com', 'premium'),
  ('ArthurMorgan', 'RedD3@dR3d3mpt10n!', 'Arthur Morgan', '789 Van Horn', '555-2345', 'arthurmorgan@example.com', 'basic'),
  ('NikoBellic', 'L1b3rtyC1ty!', 'Niko Bellic', '123 Broker', '555-6789', 'nikobellic@example.com', 'premium'),
  ('CJ', 'Gr0v3Str33t4Life!', 'CJ', '456 Los Santos', '555-0123', 'cj@example.com', 'basic'),
  ('Agent47', 'S1l3ntAss@ss1n!', 'Agent 47', '789 ICA Training Facility', '555-4567', 'agent47@example.com', 'premium'),
  ('Bayek', 'Ass4ss1nsCr33d!', 'Bayek of Siwa', '123 Siwa Oasis', '555-8901', 'bayek@example.com', 'basic'),
  ('Eivor', 'Vik1ngS4g4!', 'Eivor', '456 Ravensthorpe', '555-2345', 'eivor@example.com', 'premium'),
  ('CommanderShepard', 'M4ssEff3ct!', 'Commander Shepard', '789 Citadel', '555-6789', 'shepard@example.com', 'basic'),
  ('GordonFreeman', 'H@lfL1f3!', 'Gordon Freeman', '123 City 17', '555-0123', 'freeman@example.com', 'premium'),
  ('MaxCaulfield', 'L1f3IsStr4ng3!', 'Max Caulfield', '456 Arcadia Bay', '555-4567', 'max@example.com', 'basic'),
  ('Chell', 'P0rt4l!', 'Chell', '789 Aperture Science', '555-8901', 'chell@example.com', 'premium'),
  ('Geralt', 'Th3Witch3r!', 'Geralt of Rivia', '123 Kaer Morhen', '555-2345', 'geralt@example.com', 'basic'),
  ('Ryu', 'Str33tF1ght3r!', 'Ryu', '456 Japan', '555-6789', 'ryu@example.com', 'premium'),
  ('ChunLi', 'Sp1nn1ngBirdK1ck!', 'Chun-Li', '789 China', '555-0123', 'chunli@example.com', 'basic'),
  ('Joel', 'L0v3T0T3ll!', 'Joel Miller', '123 Jackson County', '555-4567', 'joelmiller@example.com', 'premium'),
  ('Ellie', 'P4rtII!', 'Ellie Williams', '456 Seattle', '555-8901', 'ellie@example.com', 'basic'),
  ('Snake', 'M3t4lG3arS0l1d!', 'Solid Snake', '789 Shadow Moses Island', '555-2345', 'solidsnake@example.com', 'premium'),
  ('LaraCroft', 'Tr3asur3Hunt3r!', 'Lara Croft', '123 Croft Manor', '555-6789', 'laracroft@example.com', 'basic'),
  ('Aloy', 'H0r1z0nZ3r0Dawn!', 'Aloy', '456 Meridian', '555-0123', 'aloy@example.com', 'premium'),
  ('Kratos', 'G0d0fW@r!', 'Kratos', '789 Greece', '555-4567', 'kratos@example.com', 'basic'),
  ('Ezio', 'Ass4ss1nsCr33d!', 'Ezio Auditore', '123 Italy', '555-8901', 'ezio@example.com', 'premium'),
  ('Samus', 'M3tR0idHunt3r!', 'Samus Aran', '456 Zebes', '555-2345', 'samus@example.com', 'basic'),
  ('JohnCarmack', 'DOOMMast3r!', 'John Carmack', '123 Texas', '555-0123', 'jcarmack@example.com', 'premium'),
  ('ShigeruMiyamoto', 'MushroomK1ng!', 'Shigeru Miyamoto', '456 Kyoto', '555-4567', 'miyamoto@example.com', 'basic'),
  ('HideoKojima', 'K0j1m@Sn@k3!', 'Hideo Kojima', '789 Tokyo', '555-8901', 'kojima@example.com', 'premium'),
  ('SidMeier', 'Civ1l1z4t10n!', 'Sid Meier', '123 Maryland', '555-2345', 'smeier@example.com', 'basic'),
  ('GabeNewell', 'H@lfL1f33p3!', 'Gabe Newell', '456 Washington', '555-6789', 'gaben@example.com', 'premium'),
  ('ToddHoward', 'Skyr1m4Life!', 'Todd Howard', '789 Maryland', '555-0123', 'toddhoward@example.com', 'basic'),
  ('TimSweeney', 'Unr34lEng1n3!', 'Tim Sweeney', '123 North Carolina', '555-4567', 'timsweeney@example.com', 'premium'),
  ('ShuheiYoshida', 'Pl4yst4t10n!', 'Shuhei Yoshida', '456 Tokyo', '555-8901', 'syoshida@example.com', 'basic'),
  ('PhilSpencer', 'Xb0xG@m3r!', 'Phil Spencer', '789 Washington', '555-2345', 'philspencer@example.com', 'premium'),
  ('GabeLogan', 'Syph0nF1lt3r!', 'Gabe Logan', '123 Virginia', '555-6789', 'gabelogan@example.com', 'basic'),
  ('JordanMechner', 'Pr1nce0fP3r5!', 'Jordan Mechner', '456 California', '555-0123', 'jmechner@example.com', 'premium'),
  ('CliffBleszinski', 'G34r5', 'Cliff Bleszinski', '789 California', '555-4567', 'cliffb@example.com', 'basic'),
  ('YvesGuillemot', 'Ub1s0ftC3o!', 'Yves Guillemot', '123 France', '555-8901', 'yvesg@example.com', 'premium'),
  ('GarryNewman', 'G4rrysM0d!', 'Garry Newman', '456 United Kingdom', '555-2345', 'garrynewman@example.com', 'basic'),
  ('MarkusPersson', 'N0tch!', 'Markus Persson', '789 Sweden', '555-6789', 'notch@example.com', 'premium'),
  ('DavidBraben', 'El1t3D@ng3r0us!', 'David Braben', '123 United Kingdom', '555-0123', 'braben@example.com', 'basic'),
  ('PeterMolyneux', 'G0dS1mul4t10n!', 'Peter Molyneux', '456 United Kingdom', '555-4567', 'pmolyneux@example.com', 'premium'),
  ('KenKutaragi', 'F4th3r0fPl4yst4t10n!', 'Ken Kutaragi', '789 Tokyo', '555-8901', 'kkutaragi@example.com', 'basic'),
  ('HironobuSakaguchi', 'F1n4lF4nt4sypapa!', 'Hironobu Sakaguchi', '123 Tokyo', '555-2345', 'hsakaguchi@example.com', 'premium'),
  ('YujiNaka', 'Sp33dH0g!', 'Yuji Naka', '456 Japan', '555-6789', 'ynaka@example.com', 'basic'),
  ('ToruIwatani', 'PacM4nFath3r!', 'Toru Iwatani', '789 Japan', '555-0123', 'iwatani@example.com', 'premium'),
  ('GordonWalton', 'Ult1m4Onl1n3!', 'Gordon Walton', '123 California', '555-4567', 'gwalton@example.com', 'basic'),
  ('KojiIgarashi', 'Bl00dst41n3d!', 'Koji Igarashi', '456 Japan', '555-8901', 'kojiigarashi@example.com', 'premium'),
  ('TimSchafer', 'P0intAndCl1ck!', 'Tim Schafer', '789 California', '555-2345', 'tschafer@example.com', 'basic'),
  ('ShinjiMikami', 'R3s1d3nt3v1l!', 'Shinji Mikami', '123 Japan', '555-6789', 'smikami@example.com', 'premium'),
  ('AmyHennig', 'Unch4rt3dSt0ry!', 'Amy Hennig', '456 California', '555-0123', 'ahennig@example.com', 'basic'),
  ('DavidJones', 'Gr4ndTh3ft3r!', 'David Jones', '789 United Kingdom', '555-4567', 'djones@example.com', 'premium'),
  ('TimCain', 'F4ll0utCr34t0r!', 'Tim Cain', '123 California', '555-8901', 'tcain@example.com', 'basic'),
  ('JohnRomero', 'D00MEvil!', 'John Romero', '456 Ireland', '555-2345', 'jromero@example.com', 'premium'),
  ('TetsuyaMizuguchi', 'RezOn4!', 'Tetsuya Mizuguchi', '789 Japan', '555-6789', 'tmizuguchi@example.com', 'basic');

-- Inserción de datos de prueba en la tabla 'proveedores'
INSERT INTO proveedores (nombre_empresa, direccion, telefono, correo_electronico)
VALUES
  ('Nintendo', '123 Nintendo Street', '1234567890', 'info@nintendo.com'),
  ('Sony', '456 Sony Street', '1234567890', 'info@sony.com'),
  ('Rockstar Games', '789 Rockstar Street', '1234567890', 'info@rockstar.com'),
  ('CD Projekt Red', '123 CD Projekt Street', '1234567890', 'info@cdprojekt.com'),
  ('Ubisoft', '456 Ubisoft Street', '1234567890', 'info@ubisoft.com'),
  ('Electronic Arts', '789 EA Street', '1234567890', 'info@ea.com');

-- Inserción de datos de prueba en la tabla 'consolas'
INSERT INTO consolas (nombre, fabricante, lanzamiento)
VALUES
  ('Nintendo Switch', 'Nintendo', '2017-03-03'),
  ('PlayStation 5', 'Sony', '2020-11-12'),
  ('Xbox Series X', 'Microsoft', '2020-11-10'),
  ('PC', 'Varios', NULL),
  ('PlayStation 4', 'Sony', '2013-11-15'),
  ('Xbox One', 'Microsoft', '2013-11-22'),
  ('Nintendo 3DS', 'Nintendo', '2011-02-26'),
  ('PlayStation Vita', 'Sony', '2011-12-17'),
  ('Wii U', 'Nintendo', '2012-11-18'),
  ('Xbox 360', 'Microsoft', '2005-11-22'),
  ('PlayStation 3', 'Sony', '2006-11-11'),
  ('Wii', 'Nintendo', '2006-11-19'),
  ('Nintendo DS', 'Nintendo', '2004-11-21'),
  ('PlayStation Portable', 'Sony', '2004-12-12'),
  ('Xbox', 'Microsoft', '2001-11-15'),
  ('GameCube', 'Nintendo', '2001-09-14'),
  ('PlayStation 2', 'Sony', '2000-03-04'),
  ('Game Boy Advance', 'Nintendo', '2001-03-21'),
  ('Dreamcast', 'Sega', '1998-11-27'),
  ('Nintendo 64', 'Nintendo', '1996-06-23');

-- Inserción de datos de prueba en la tabla 'productos'
INSERT INTO productos (nombre, descripcion, precio, stock, proveedor_id)
VALUES
  ('Super Mario Odyssey', 'Join Mario on a massive, globe-trotting 3D adventure!', 49.99, 100, 1),
  ('The Legend of Zelda: Breath of the Wild', 'Discover Hyrule like never before in this open-world masterpiece.', 59.99, 50, 1),
  ('God of War', 'Embark on a journey as Kratos, the Spartan warrior, in this epic action game.', 39.99, 75, 2),
  ('Uncharted 4: A Thief''s End', 'Join Nathan Drake on his final adventure filled with danger and treasure.', 29.99, 80, 2),
  ('Red Dead Redemption 2', 'Experience the Wild West in this critically acclaimed open-world game.', 49.99, 60, 3),
  ('Grand Theft Auto V', 'Step into the shoes of three criminals in this action-packed crime game.', 19.99, 120, 3),
  ('Assassin''s Creed Valhalla', 'Become a Viking warrior and lead your clan to glory in this historical adventure.', 54.99, 70, 4),
  ('Cyberpunk 2077', 'Immerse yourself in a futuristic city in this highly anticipated RPG.', 39.99, 30, 4),
  ('Super Smash Bros. Ultimate', 'Fight with your favorite Nintendo characters in this ultimate crossover game.', 59.99, 90, 1),
  ('Pokémon Sword', 'Embark on a journey to become the Champion in the Galar region.', 49.99, 100, 1),
  ('Marvel''s Spider-Man', 'Swing through New York City as the iconic web-slinger in this thrilling adventure.', 39.99, 60, 2),
  ('The Last of Us Part II', 'Survive in a post-apocalyptic world filled with infected and desperate survivors.', 49.99, 40, 2),
  ('Animal Crossing: New Horizons', 'Create your perfect island life in this charming and relaxing game.', 59.99, 80, 1),
  ('Splatoon 2', 'Team up with friends and compete in colorful ink-based battles.', 39.99, 70, 1),
  ('Super Mario Kart 8 Deluxe', 'Race against your friends and family in this classic kart racing game.', 49.99, 100, 1),
  ('FIFA 21', 'Take to the pitch and experience the excitement of professional soccer.', 29.99, 120, 5),
  ('Madden NFL 21', 'Take control of your favorite NFL team and lead them to victory.', 29.99, 100, 5),
  ('Call of Duty: Black Ops Cold War', 'Engage in thrilling multiplayer and intense Cold War-era campaign.', 59.99, 50, 6),
  ('Halo Infinite', 'Return to the iconic Halo series with Master Chief in this next-gen installment.', 59.99, 30, 7),
  ('The Legend of Zelda: Ocarina of Time', 'Experience an epic adventure in one of the greatest games of all time.', 19.99, 25, 1);

-- Inserción de datos de prueba en la tabla 'categorias'
INSERT INTO categorias (nombre, descripcion)
VALUES
  ('Acción', 'Juegos llenos de emoción y combate'),
  ('Aventura', 'Explora mundos y resuelve misterios'),
  ('Plataformas', 'Salta y corre a través de niveles desafiantes'),
  ('RPG', 'Vive historias épicas y mejora a tu personaje'),
  ('Deportes', 'Participa en emocionantes competiciones'),
  ('Shooter', 'Dispara y combate en emocionantes enfrentamientos'),
  ('Estrategia', 'Planifica y conquista en juegos de estrategia'),
  ('Simulación', 'Simula la vida o situaciones realistas'),
  ('Puzzle', 'Resuelve desafiantes acertijos y rompecabezas'),
  ('Indie', 'Descubre joyas independientes y originales');

-- Inserción de datos de prueba en la tabla 'pedidos'
INSERT INTO pedidos (usuario_id, fecha, total)
VALUES
  (1, '2023-06-01', 99.99),
  (2, '2023-06-02', 49.99),
  (3, '2023-06-03', 29.99),
  (4, '2023-06-04', 79.99),
  (5, '2023-06-05', 39.99),
  (6, '2023-06-06', 59.99),
  (7, '2023-06-07', 69.99),
  (8, '2023-06-08', 89.99),
  (9, '2023-06-09', 19.99),
  (10, '2023-06-10', 129.99),
  (11, '2023-06-11', 49.99),
  (12, '2023-06-12', 79.99),
  (13, '2023-06-13', 39.99),
  (14, '2023-06-14', 59.99),
  (15, '2023-06-15', 69.99),
  (16, '2023-06-16', 89.99),
  (17, '2023-06-17', 19.99),
  (18, '2023-06-18', 129.99),
  (19, '2023-06-19', 99.99),
  (20, '2023-06-20', 49.99);

-- Inserción de datos de prueba en la tabla 'detalles_pedido'
INSERT INTO detalles_pedido (pedido_id, producto_id, cantidad)
VALUES
  (1, 1, 1),
  (1, 2, 1),
  (2, 3, 1),
  (2, 4, 1),
  (3, 5, 1),
  (3, 6, 1),
  (4, 7, 1),
  (4, 8, 1),
  (5, 9, 1),
  (5, 10, 1),
  (6, 11, 1),
  (6, 12, 1),
  (7, 13, 1),
  (7, 14, 1),
  (8, 15, 1),
  (8, 16, 1),
  (9, 17, 1),
  (9, 18, 1),
  (10, 19, 1),
  (10, 20, 1),
  (11, 1, 1),
  (11, 2, 1),
  (12, 3, 1),
  (12, 4, 1),
  (13, 5, 1),
  (13, 6, 1),
  (14, 7, 1),
  (14, 8, 1),
  (15, 9, 1),
  (15, 10, 1),
  (16, 11, 1),
  (16, 12, 1),
  (17, 13, 1),
  (17, 14, 1),
  (18, 15, 1),
  (18, 16, 1),
  (19, 17, 1),
  (19, 18, 1),
  (20, 19, 1),
  (20, 20, 1);

-- Inserción de datos de prueba en la tabla 'juegos_retro'
INSERT INTO juegos_retro (nombre, descripcion, precio, stock, consola_id)
VALUES
  ('Super Mario Bros.', 'Join Mario on his classic adventure to rescue Princess Peach.', 9.99, 50, 1),
  ('The Legend of Zelda', 'Embark on a legendary quest to defeat Ganon and rescue Princess Zelda.', 14.99, 30, 1),
  ('Pac-Man', 'Guide Pac-Man through mazes and gobble up all the dots while avoiding ghosts.', 4.99, 100, 2),
  ('Tetris', 'Arrange falling blocks to complete rows and achieve high scores.', 6.99, 80, 2),
  ('Donkey Kong', 'Help Mario save Pauline from the clutches of the giant ape.', 7.99, 60, 1),
  ('Space Invaders', 'Defend the Earth from a relentless alien invasion in this iconic shooter.', 3.99, 120, 2),
  ('Street Fighter II', 'Engage in intense martial arts battles against a variety of opponents.', 9.99, 40, 3),
  ('Mega Man', 'Control the blue robotic hero as you battle against evil robots.', 6.99, 50, 1),
  ('Sonic the Hedgehog', 'Run and spin through colorful levels as the speedy blue hedgehog.', 7.99, 70, 4),
  ('Final Fantasy VI', 'Immerse yourself in a rich fantasy world and embark on an epic quest.', 12.99, 20, 5),
  ('Metroid', 'Explore alien worlds and uncover the secrets of the Metroids and Space Pirates.', 8.99, 30, 1),
  ('Castlevania', 'Vanquish Dracula and his minions in this action-packed vampire-hunting adventure.', 9.99, 40, 1),
  ('Contra', 'Join the elite soldiers as they battle against an alien invasion in this intense shooter.', 7.99, 50, 3),
  ('The Legend of Zelda: A Link to the Past', 'Experience another epic journey in the land of Hyrule.', 14.99, 25, 1),
  ('Super Metroid', 'Take on the role of Samus Aran in her quest to rescue the baby Metroid.', 12.99, 30, 1),
  ('Chrono Trigger', 'Travel through time and save the world in this beloved RPG.', 12.99, 20, 5),
  ('Super Castlevania IV', 'Whip your way through Dracula''s castle in this classic vampire-hunting adventure.', 9.99, 25, 1),
  ('Super Mario World', 'Join Mario and Luigi on their quest to save the Mushroom Kingdom.', 9.99, 60, 1),
  ('Mega Man X', 'Control the new Mega Man X and fight against powerful rogue Reploids.', 8.99, 35, 1),
  ('Earthbound', 'Embark on a quirky and humorous RPG adventure in a modern-day setting.', 12.99, 15, 1),
  ('Mortal Kombat II', 'Engage in brutal battles against a variety of fighters in this iconic fighting game.', 7.99, 45, 3),
  ('Super Mario Kart', 'Race against your friends or the computer in this classic kart racing game.', 9.99, 55, 1),
  ('Golden Axe', 'Choose your hero and embark on a quest to defeat the evil Death Adder.', 6.99, 30, 6),
  ('Streets of Rage', 'Team up with friends to clean up the streets and take down crime syndicates.', 6.99, 40, 6),
  ('Metal Gear Solid', 'Infiltrate enemy territory and complete stealth missions as Solid Snake.', 14.99, 20, 7),
  ('Resident Evil', 'Survive a nightmarish zombie outbreak and uncover the mysteries of Raccoon City.', 12.99, 25, 7),
  ('Super Street Fighter II', 'Continue the intense battles with new characters and moves.', 9.99, 35, 3),
  ('Ninja Gaiden', 'Take on the role of Ryu Hayabusa and avenge your clan in this challenging action game.', 8.99, 30, 1),
  ('Punch-Out!!', 'Step into the ring as Little Mac and work your way up to become the boxing champion.', 7.99, 50, 1),
  ('Castlevania: Symphony of the Night', 'Explore the gothic castle as Alucard and defeat Dracula in this iconic Metroidvania.', 12.99, 15, 1),
  ('Super Street Fighter II Turbo', 'Experience the ultimate edition of the classic fighting game with new features and speed.', 9.99, 30, 3),
  ('The Legend of Zelda: Link''s Awakening', 'Embark on a mysterious adventure on the Koholint Island.', 12.99, 25, 1),
  ('Final Fantasy IV', 'Join Cecil and his allies on a quest to save the world from the clutches of darkness.', 12.99, 20, 5),
  ('Street Fighter Alpha 2', 'Unleash powerful special moves and combos in this classic Street Fighter game.', 8.99, 30, 3),
  ('Super Bomberman', 'Strategically place bombs to take out opponents and clear the levels.', 7.99, 40, 2),
  ('Super Smash Bros.', 'Engage in frenetic battles with a roster of Nintendo characters.', 14.99, 15, 1),
  ('Teenage Mutant Ninja Turtles IV: Turtles in Time', 'Join the Ninja Turtles in a time-traveling adventure to defeat Shredder.', 9.99, 25, 1),
  ('Castlevania III: Dracula''s Curse', 'Join Trevor Belmont on his quest to defeat Dracula and save Transylvania.', 9.99, 30, 1),
  ('Super Mario Bros. 3', 'Embark on an epic platforming adventure to save the Mushroom Kingdom from Bowser.', 9.99, 60, 1),
  ('Double Dragon', 'Fight your way through the streets as Billy and Jimmy Lee in this classic beat em up.', 6.99, 50, 6),
  ('Ninja Turtles: The Hyperstone Heist', 'Battle against Shredder and the Foot Clan to rescue April and stop their evil plans.', 7.99, 40, 1),
  ('Secret of Mana', 'Discover a world of magic and adventure in this beloved action RPG.', 12.99, 20, 5),
  ('Kirby''s Adventure', 'Help Kirby defeat the evil King Dedede and restore Dream Land.', 8.99, 30, 1),
  ('Super Street Fighter II: The New Challengers', 'Take on new challengers and master their unique fighting styles.', 9.99, 35, 3),
  ('Sonic the Hedgehog 2', 'Join Sonic and Tails in their quest to stop Dr. Robotnik.', 7.99, 50, 4),
  ('Super Mario All-Stars', 'Experience enhanced versions of the classic Mario games in one collection.', 9.99, 40, 1),
  ('Mega Man 2', 'Take on the evil Dr. Wily and his robot masters in this challenging platformer.', 6.99, 50, 1),
  ('Final Fight', 'Clean up the streets of Metro City as one of the street fighters.', 7.99, 45, 6),
  ('Super Ghouls n Ghosts', 'Guide Arthur on his quest to rescue Princess Prin Prin from the clutches of evil.', 9.99, 35, 1),
  ('Mortal Kombat', 'Engage in intense battles and finish your opponents with brutal fatalities.', 7.99, 40, 3),
  ('Super Mario Bros. 2', 'Join Mario and his friends on a unique adventure in the dream world of Subcon.', 9.99, 30, 1),
  ('Mega Man 3', 'Continue the battle against Dr. Wily and his robot masters in this iconic platformer.', 6.99, 45, 1),
  ('Super Contra', 'Take on the alien forces once again in this challenging run-and-gun game.', 7.99, 50, 3),
  ('Mega Man X2', 'Control the new Mega Man X and defeat a new threat of rogue Reploids.', 8.99, 30, 1),
  ('Super Mario RPG: Legend of the Seven Stars', 'Join Mario and his friends on a hilarious and epic RPG adventure.', 12.99, 20, 1),
  ('Final Fantasy V', 'Embark on a journey to restore the four elemental crystals in this classic RPG.', 12.99, 25, 5),
  ('Aladdin', 'Relive the magic of the Disney film as Aladdin on his quest to rescue Princess Jasmine.', 7.99, 40, 1),
  ('Super Street Fighter II Turbo: Hyper Fighting', 'Fight against a roster of powerful fighters in this enhanced edition of Street Fighter II.', 9.99, 30, 3),
  ('Super Mario World 2: Yoshi''s Island', 'Guide Yoshi through colorful levels to rescue Baby Mario from the clutches of Baby Bowser.', 9.99, 25, 1);

COMMIT;


````

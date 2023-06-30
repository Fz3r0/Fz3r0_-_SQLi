

## Script

````sql
-- Creación de la base de datos
CREATE DATABASE IF NOT EXISTS Fz3r0_Corporations CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Selección de la base de datos
USE Fz3r0_Corporations;

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

-- Creación de la tabla 'productos'
CREATE TABLE productos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  descripcion TEXT,
  precio DECIMAL(10, 2) NOT NULL,
  stock INT NOT NULL,
  proveedor_id INT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  INDEX idx_proveedor_id (proveedor_id),
  FOREIGN KEY (proveedor_id) REFERENCES proveedores(id)
) ENGINE=InnoDB;

-- Creación de la tabla 'categorias'
CREATE TABLE categorias (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  descripcion TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
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

-- Creación de la tabla 'producto_categoria'
CREATE TABLE producto_categoria (
  producto_id INT,
  categoria_id INT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  INDEX idx_categoria_id (categoria_id),
  FOREIGN KEY (producto_id) REFERENCES productos(id),
  FOREIGN KEY (categoria_id) REFERENCES categorias(id)
) ENGINE=InnoDB;


````

### Agregar datos de prueba

````sql
-- Inserción de datos en la tabla 'usuarios'
INSERT INTO usuarios (username, password, name, address, phone, mail, subscription_type)
VALUES
  ('doomguy', 'doom123', 'Doomguy', 'Mars', '1234567890', 'doomguy@example.com', 'premium'),
  ('cloud', 'cloud123', 'Cloud Strife', 'Midgar', '9876543210', 'cloud@example.com', 'basic'),
  ('snake', 'snake123', 'Solid Snake', 'Shadow Moses Island', '4567890123', 'snake@example.com', 'premium'),
  ('mario', 'mario123', 'Mario', 'Mushroom Kingdom', '8901234567', 'mario@example.com', 'basic'),
  ('luigi', 'luigi123', 'Luigi', 'Mushroom Kingdom', '3210987654', 'luigi@example.com', 'premium'),
  ('geralt', 'geralt123', 'Geralt of Rivia', 'Kaer Morhen', '6789012345', 'geralt@example.com', 'basic'),
  ('sora', 'sora123', 'Sora', 'Destiny Islands', '2345678901', 'sora@example.com', 'premium'),
  ('ryu', 'ryu123', 'Ryu', 'Japan', '5678901234', 'ryu@example.com', 'basic'),
  ('ezio', 'ezio123', 'Ezio Auditore', 'Florence', '4321098765', 'ezio@example.com', 'premium'),
  ('jillvalentine', 'jillvalentine123', 'Jill Valentine', 'Raccoon City', '8765432109', 'jillvalentine@example.com', 'basic'),
  ('mariokart', 'mariokart123', 'Mario Kart', 'Rainbow Road', '1098765432', 'mariokart@example.com', 'premium'),
  ('alyxvance', 'alyxvance123', 'Alyx Vance', 'City 17', '5432109876', 'alyxvance@example.com', 'basic');

-- Inserción de datos en la tabla 'proveedores'
INSERT INTO proveedores (nombre_empresa, direccion, telefono, correo_electronico)
VALUES
  ('Nintendo', 'Kyoto, Japón', '1234567890', 'contact@nintendo.com'),
  ('Sega', 'Tokio, Japón', '9876543210', 'contact@sega.com'),
  ('Capcom', 'Osaka, Japón', '4567890123', 'contact@capcom.com'),
  ('Blizzard', 'Irvine, California, EE. UU.', '8901234567', 'contact@blizzard.com'),
  ('Atari', 'Sunnyvale, California, EE. UU.', '3210987654', 'contact@atari.com'),
  ('Square Enix', 'Tokio, Japón', '6543210987', 'contact@squareenix.com'),
  ('Konami', 'Tokio, Japón', '0123456789', 'contact@konami.com'),
  ('Electronic Arts', 'Redwood City, California, EE. UU.', '9876543210', 'contact@ea.com');

-- Inserción de datos en la tabla 'productos'
INSERT INTO productos (nombre, descripcion, precio, stock, proveedor_id)
VALUES
  ('Super Mario Bros.', 'Plataforma clásica de Nintendo', 19.99, 50, 1),
  ('Final Fantasy VII Remake', 'RPG de Square Enix', 59.99, 20, 6),
  ('The Legend of Zelda: Breath of the Wild', 'Aventura de mundo abierto de Nintendo', 49.99, 30, 1),
  ('Sonic the Hedgehog', 'Juego de plataformas de Sega', 9.99, 100, 2),
  ('Resident Evil 2', 'Survival horror de Capcom', 29.99, 15, 3),
  ('DOOM', 'Shooter de id Software', 19.99, 40, 4),
  ('Street Fighter II', 'Juego de lucha de Capcom', 14.99, 60, 3),
  ('Final Fantasy X', 'RPG de Square Enix', 29.99, 25, 6),
  ('Metal Gear Solid', 'Acción y sigilo de Konami', 9.99, 80, 7),
  ('The Elder Scrolls V: Skyrim', 'RPG de mundo abierto de Bethesda', 39.99, 10, 4),
  ('Resident Evil 4', 'Survival horror de Capcom', 24.99, 20, 3),
  ('Chrono Trigger', 'RPG de Square Enix', 19.99, 30, 6),
  ('Super Mario World', 'Plataforma clásica de Nintendo', 14.99, 60, 1),
  ('The Legend of Zelda: A Link to the Past', 'Aventura de acción de Nintendo', 24.99, 35, 1),
  ('Super Metroid', 'Acción y aventura de Nintendo', 19.99, 25, 1),
  ('Mega Man X', 'Plataforma de Capcom', 14.99, 40, 3),
  ('Super Castlevania IV', 'Aventura de Konami', 19.99, 20, 7),
  ('Street Fighter II Turbo', 'Juego de lucha de Capcom', 14.99, 50, 3),
  ('Secret of Mana', 'RPG de Square Enix', 29.99, 15, 6),
  ('Sonic the Hedgehog 2', 'Juego de plataformas de Sega', 9.99, 80, 2),
  ('Streets of Rage 2', 'Juego de lucha de Sega', 14.99, 30, 5),
  ('Super Street Fighter II', 'Juego de lucha de Capcom', 19.99, 25, 3),
  ('Final Fantasy VI', 'RPG de Square Enix', 29.99, 10, 6),
  ('Duke Nukem 3D', 'Shooter de 3D Realms', 9.99, 60, 8),
  ('Commander Keen', 'Plataforma clásica de id Software', 9.99, 50, 8);

-- Inserción de datos en la tabla 'ventas'
INSERT INTO ventas (fecha_venta, total, usuario_id)
VALUES
  ('2023-06-01 10:23:45', 39.98, 1),
  ('2023-06-02 15:45:12', 74.97, 2),
  ('2023-06-03 09:18:36', 54.97, 3),
  ('2023-06-04 14:55:21', 29.99, 1),
  ('2023-06-05 11:30:48', 34.98, 4),
  ('2023-06-06 16:40:15', 24.99, 5),
  ('2023-06-07 12:15:32', 44.97, 6),
  ('2023-06-08 09:48:57', 19.99, 7),
  ('2023-06-09 15:23:10', 49.98, 2),
  ('2023-06-10 13:10:25', 29.99, 3),
  ('2023-06-11 10:05:39', 59.97, 4),
  ('2023-06-12 14:35:42', 34.98, 5),
  ('2023-06-13 11:20:58', 39.98, 6),
  ('2023-06-14 09:15:04', 24.99, 7),
  ('2023-06-15 15:50:19', 29.99, 1),
  ('2023-06-16 13:45:27', 19.99, 2),
  ('2023-06-17 10:10:32', 44.97, 3),
  ('2023-06-18 08:05:46', 49.98, 4),
  ('2023-06-19 14:30:51', 54.97, 5),
  ('2023-06-20 12:25:03', 29.99, 6),
  ('2023-06-21 09:50:16', 19.99, 7),
  ('2023-06-22 15:15:28', 39.98, 1),
  ('2023-06-23 13:10:40', 24.99, 2),
  ('2023-06-24 10:35:52', 29.99, 3),
  ('2023-06-25 08:30:03', 59.97, 4),
  ('2023-06-26 14:55:14', 34.98, 5),
  ('2023-06-27 12:50:25', 44.97, 6),
  ('2023-06-28 10:15:36', 49.98, 7),
  ('2023-06-29 15:40:47', 24.99, 1);

-- Inserción de datos en la tabla 'detalles_venta'
INSERT INTO detalles_venta (venta_id, producto_id, cantidad, precio_unitario)
VALUES
  (1, 1, 2, 19.99),
  (1, 4, 1, 9.99),
  (2, 2, 1, 59.99),
  (2, 5, 1, 29.99),
  (2, 8, 1, 14.99),
  (3, 3, 1, 49.99),
  (3, 6, 1, 19.99),
  (4, 1, 1, 19.99),
  (5, 2, 1, 59.99),
  (5, 7, 1, 14.99),
  (6, 3, 1, 49.99),
  (7, 4, 1, 9.99),
  (7, 6, 1, 19.99),
  (7, 8, 1, 14.99),
  (8, 1, 1, 19.99),
  (8, 3, 1, 49.99),
  (9, 2, 1, 59.99),
  (9, 5, 1, 29.99),
  (9, 8, 1, 14.99),
  (10, 1, 1, 19.99),
  (10, 4, 1, 9.99),
  (10, 6, 1, 19.99),
  (11, 2, 1, 59.99),
  (11, 5, 1, 29.99),
  (11, 8, 1, 14.99),
  (12, 1, 1, 19.99),
  (13, 3, 1, 49.99),
  (13, 6, 1, 19.99),
  (13, 8, 1, 14.99),
  (14, 1, 1, 19.99),
  (15, 2, 1, 59.99),
  (15, 5, 1, 29.99),
  (16, 1, 1, 19.99),
  (16, 3, 1, 49.99),
  (16, 6, 1, 19.99),
  (17, 2, 1, 59.99),
  (17, 5, 1, 29.99),
  (17, 8, 1, 14.99),
  (18, 1, 1, 19.99),
  (18, 4, 1, 9.99),
  (18, 6, 1, 19.99),
  (18, 8, 1, 14.99),
  (19, 2, 1, 59.99),
  (19, 5, 1, 29.99),
  (20, 1, 1, 19.99),
  (20, 3, 1, 49.99),
  (20, 6, 1, 19.99),
  (21, 2, 1, 59.99),
  (21, 5, 1, 29.99),
  (21, 8, 1, 14.99),
  (22, 1, 1, 19.99),
  (22, 4, 1, 9.99),
  (22, 6, 1, 19.99);


````


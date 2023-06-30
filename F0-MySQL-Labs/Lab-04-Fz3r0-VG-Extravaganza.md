
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
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
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
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  INDEX idx_proveedor_id (proveedor_id),
  INDEX idx_desarrollador_id (desarrollador_id),
  INDEX idx_consola_id (consola_id),
  FOREIGN KEY (proveedor_id) REFERENCES proveedores(id),
  FOREIGN KEY (desarrollador_id) REFERENCES desarrolladores(id),
  FOREIGN KEY (consola_id) REFERENCES consolas(id)
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
  plataforma VARCHAR(50) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  INDEX idx_proveedor_id (proveedor_id),
  FOREIGN KEY (proveedor_id) REFERENCES proveedores(id)
) ENGINE=InnoDB;

````





````sql


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

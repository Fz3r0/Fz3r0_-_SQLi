
## Base de Datos `Fz3r0_Store`

- Una pequeña y bonita base de datos que contiene las siguientes tablas:

### Tabla de `usuarios`:

- Almacena la información básica de los usuarios, como su nombre de usuario, contraseña y suscripción.
- También incluye campos adicionales como nombre completo, dirección y número de teléfono directamente en esta tabla.
- Esta estructura permite almacenar todos los datos relacionados con un usuario en una sola entidad.

### Tabla de `pedidos`:

- Registra los pedidos realizados por los usuarios.
- Cada pedido se relaciona con un usuario específico a través de la clave externa (foreign key) "user_id".
- Incluye información sobre el nombre del producto y la cantidad solicitada.

### Tabla de `productos`:

- Almacena los detalles de los productos disponibles.
- Incluye campos como nombre, descripción y precio.
- Esta tabla permite mantener un catálogo de productos para su uso en los pedidos.

### Tabla de `categorías`:

- Contiene las categorías a las que pertenecen los productos.
- Proporciona una clasificación organizada para los productos.
- Cada categoría tiene un nombre único.

### Tabla de relaciones entre `productos` y `categorías`:

- Esta tabla permite establecer una relación muchos a muchos entre productos y categorías.
- Un producto puede pertenecer a múltiples categorías y una categoría puede tener múltiples productos.
- Utiliza las claves externas (foreign keys) "product_id" y "category_id" para referenciar los productos y categorías respectivamente.
- La clave primaria compuesta (primary key) "product_id, category_id" garantiza la unicidad de las relaciones.
- La estructura de la base de datos creada busca simplificar el diseño al combinar información relacionada en la tabla de usuarios y proporcionar una estructura para manejar pedidos, productos y categorías de manera eficiente y coherente.

## Crear DB

````sql
-- Crear DB
create database Fz3r0_Store;

-- Usar DB
use Fz3r0_Store
````

## Crear Tablas en DB

````sql
-- Tabla de usuarios
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(32),
  password VARCHAR(32),
  subscription VARCHAR(32),
  full_name VARCHAR(64),
  address VARCHAR(128),
  phone_number VARCHAR(16)
);

-- Tabla de pedidos
CREATE TABLE orders (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT,
  product_name VARCHAR(64),
  quantity INT,
  order_date DATE,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Tabla de productos
CREATE TABLE products (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(64),
  description VARCHAR(256),
  price DECIMAL(10,2)
);

-- Tabla de categorías
CREATE TABLE categories (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(64)
);

-- Tabla de relaciones entre productos y categorías (tabla de muchos a muchos). No era necesario agregar los strings de nombres, pero es para hacerlo más comprensible.
CREATE TABLE product_categories (
  product_id INT,
  category_id INT,
  product_name VARCHAR(50),
  category_name VARCHAR(50),
  FOREIGN KEY (product_id) REFERENCES products(id),
  FOREIGN KEY (category_id) REFERENCES categories(id),
  PRIMARY KEY (product_id, category_id)
);
````

## Insertar Datos en Tablas de DB

````sql
-- Insertar datos en la tabla de usuarios
INSERT INTO users (username, password, subscription, full_name, address, phone_number)
VALUES
  ('john.doe', 'password123', 'premium', 'John Doe', '123 Main St', '555-1234'),
  ('jane.smith', 'password456', 'basic', 'Jane Smith', '456 Elm St', '555-5678'),
  ('mike.johnson', 'password789', 'premium', 'Mike Johnson', '789 Oak St', '555-9012'),
  ('sara.wilson', 'passwordabc', 'basic', 'Sara Wilson', '321 Pine St', '555-3456'),
  ('chris.brown', 'passworddef', 'premium', 'Chris Brown', '654 Maple St', '555-7890'),
  ('emily.davis', 'passwordeg1', 'basic', 'Emily Davis', '987 Cedar St', '555-2345'),
  ('alex.miller', 'passwordeg2', 'premium', 'Alex Miller', '159 Birch St', '555-6789'),
  ('lisa.thomas', 'passwordeg3', 'basic', 'Lisa Thomas', '753 Walnut St', '555-0123'),
  ('ryan.hall', 'passwordeg4', 'premium', 'Ryan Hall', '852 Sycamore St', '555-4567'),
  ('kate.clark', 'passwordeg5', 'basic', 'Kate Clark', '369 Fir St', '555-8901');

-- Insertar datos en la tabla de pedidos
INSERT INTO orders (user_id, product_id, quantity, order_date)
VALUES
  (1, 1, 2, '2023-06-27 10:15:00'),
  (2, 3, 1, '2023-06-27 11:30:00'),
  (1, 6, 3, '2023-06-27 14:45:00'),
  (3, 4, 1, '2023-06-27 16:20:00'),
  (2, 8, 2, '2023-06-27 18:05:00');

-- Insertar datos en la tabla de productos
INSERT INTO products (name, description, price)
VALUES
  ('Manzana', 'Manzana fresca y jugosa', 1.99),
  ('Martillo', 'Martillo de acero resistente', 9.99),
  ('Camiseta', 'Camiseta de algodón suave', 14.99),
  ('Teléfono móvil', 'Teléfono inteligente de última generación', 499.99),
  ('Pera', 'Pera madura y dulce', 1.49),
  ('Destornillador', 'Destornillador magnético', 4.99),
  ('Jeans', 'Pantalones vaqueros de estilo moderno', 29.99),
  ('Portátil', 'Ordenador portátil de alto rendimiento', 999.99),
  ('Naranja', 'Naranja jugosa y refrescante', 1.29),
  ('Taladro', 'Taladro inalámbrico de gran potencia', 49.99);

-- Insertar datos en la tabla de categorías
INSERT INTO categories (name)
VALUES
  ('Frutas'),
  ('Herramientas'),
  ('Ropa'),
  ('Electrónicos');

-- Insertar datos en la tabla de relaciones entre productos y categorías
INSERT INTO product_categories (product_id, category_id, product_name, category_name)
VALUES
  (1, 1, 'Manzana', 'Frutas'),
  (2, 2, 'Martillo', 'Herramientas'),
  (3, 3, 'Camiseta', 'Ropa'),
  (4, 4, 'Teléfono móvil', 'Electrónicos'),
  (5, 1, 'Pera', 'Frutas'),
  (6, 2, 'Destornillador', 'Herramientas'),
  (7, 3, 'Jeans', 'Ropa'),
  (8, 4, 'Portátil', 'Electrónicos'),
  (9, 1, 'Naranja', 'Frutas'),
  (10, 2, 'Taladro', 'Herramientas');
````

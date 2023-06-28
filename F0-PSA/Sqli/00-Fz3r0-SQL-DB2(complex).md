
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

## Insertar Datos en DB

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
INSERT INTO orders (user_id, product_name, quantity)
VALUES
  (1, 'Product A', 2),
  (1, 'Product B', 1),
  (2, 'Product C', 3),
  (2, 'Product A', 2),
  (3, 'Product B', 1),
  (3, 'Product C', 4),
  (4, 'Product A', 3),
  (4, 'Product B', 2),
  (5, 'Product C', 1),
  (5, 'Product A', 2);

-- Insertar datos en la tabla de productos
INSERT INTO products (name, description, price)
VALUES
  ('Product A', 'Description of Product A', 9.99),
  ('Product B', 'Description of Product B', 14.99),
  ('Product C', 'Description of Product C', 19.99),
  ('Product D', 'Description of Product D', 24.99),
  ('Product E', 'Description of Product E', 29.99),
  ('Product F', 'Description of Product F', 34.99),
  ('Product G', 'Description of Product G', 39.99),
  ('Product H', 'Description of Product H', 44.99),
  ('Product I', 'Description of Product I', 49.99),
  ('Product J', 'Description of Product J', 54.99);

-- Insertar datos en la tabla de categorías
INSERT INTO categories (name)
VALUES
  ('Category 1'),
  ('Category 2'),
  ('Category 3'),
  ('Category 4'),
  ('Category 5'),
  ('Category 6'),
  ('Category 7'),
  ('Category 8'),
  ('Category 9'),
  ('Category 10');

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

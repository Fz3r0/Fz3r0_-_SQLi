
## Base de Datos `Fz3r0_Store`

- Una pequeña y bonita base de datos que contiene las siguientes tablas:

````py
MariaDB [Fz3r0_Store]> show tables;
+-----------------------+
| Tables_in_Fz3r0_Store |
+-----------------------+
| categories            |
| orders                |
| product_categories    |
| products              |
| users                 |
+-----------------------+
5 rows in set (0.000 sec)
````

### Tabla de `usuarios`:

- Almacena la información básica de los usuarios, como su nombre de usuario, contraseña y suscripción.
- También incluye campos adicionales como nombre completo, dirección y número de teléfono directamente en esta tabla.
- Esta estructura permite almacenar todos los datos relacionados con un usuario en una sola entidad.

````py
MariaDB [Fz3r0_Store]> describe users;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| id           | int(11)      | NO   | PRI | NULL    | auto_increment |
| username     | varchar(32)  | YES  |     | NULL    |                |
| password     | varchar(32)  | YES  |     | NULL    |                |
| subscription | varchar(32)  | YES  |     | NULL    |                |
| full_name    | varchar(64)  | YES  |     | NULL    |                |
| address      | varchar(128) | YES  |     | NULL    |                |
| phone_number | varchar(16)  | YES  |     | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
7 rows in set (0.001 sec)

MariaDB [Fz3r0_Store]> select * from users;
+----+--------------+-------------+--------------+--------------+-----------------+--------------+
| id | username     | password    | subscription | full_name    | address         | phone_number |
+----+--------------+-------------+--------------+--------------+-----------------+--------------+
|  1 | john.doe     | password123 | premium      | John Doe     | 123 Main St     | 555-1234     |
|  2 | jane.smith   | password456 | basic        | Jane Smith   | 456 Elm St      | 555-5678     |
|  3 | mike.johnson | password789 | premium      | Mike Johnson | 789 Oak St      | 555-9012     |
|  4 | sara.wilson  | passwordabc | basic        | Sara Wilson  | 321 Pine St     | 555-3456     |
|  5 | chris.brown  | passworddef | premium      | Chris Brown  | 654 Maple St    | 555-7890     |
|  6 | emily.davis  | passwordeg1 | basic        | Emily Davis  | 987 Cedar St    | 555-2345     |
|  7 | alex.miller  | passwordeg2 | premium      | Alex Miller  | 159 Birch St    | 555-6789     |
|  8 | lisa.thomas  | passwordeg3 | basic        | Lisa Thomas  | 753 Walnut St   | 555-0123     |
|  9 | ryan.hall    | passwordeg4 | premium      | Ryan Hall    | 852 Sycamore St | 555-4567     |
| 10 | kate.clark   | passwordeg5 | basic        | Kate Clark   | 369 Fir St      | 555-8901     |
+----+--------------+-------------+--------------+--------------+-----------------+--------------+
10 rows in set (0.000 sec)
````

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

-- Tabla de categorías con ID alfanumérico
CREATE TABLE categories (
  category_id VARCHAR(10) PRIMARY KEY,
  category_name VARCHAR(50)
);

-- Tabla de productos con ID alfanumérico
CREATE TABLE products (
  product_id VARCHAR(10) PRIMARY KEY,
  product_name VARCHAR(50),
  category_id VARCHAR(10),
  FOREIGN KEY (category_id) REFERENCES categories(category_id)
);

-- Tabla de relaciones entre productos y categorías con ID de pedido incremental
CREATE TABLE product_categories (
  product_category_id INT AUTO_INCREMENT PRIMARY KEY,
  product_id VARCHAR(10),
  category_id VARCHAR(10),
  product_name VARCHAR(50),
  category_name VARCHAR(50),
  FOREIGN KEY (product_id) REFERENCES products(product_id),
  FOREIGN KEY (category_id) REFERENCES categories(category_id)
);

-- Tabla de pedidos con ID de pedido incremental y prefijo
CREATE TABLE orders (
  order_id INT AUTO_INCREMENT PRIMARY KEY,
  order_number VARCHAR(20),
  user_id INT,
  product_category_id INT,
  quantity INT,
  order_date DATETIME,
  FOREIGN KEY (user_id) REFERENCES users(id),
  FOREIGN KEY (product_category_id) REFERENCES product_categories(product_category_id)
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

-- Inserción de datos en la tabla de categorías
INSERT INTO categories (category_id, category_name)
VALUES
  ('CAT001', 'Frutas'),
  ('CAT002', 'Herramientas'),
  ('CAT003', 'Ropa'),
  ('CAT004', 'Electrónicos');

-- Inserción de datos en la tabla de productos
INSERT INTO products (product_id, product_name, category_id)
VALUES
  ('PRD001', 'Manzana', 'CAT001'),
  ('PRD002', 'Martillo', 'CAT002'),
  ('PRD003', 'Camiseta', 'CAT003'),
  ('PRD004', 'Teléfono móvil', 'CAT004');

-- Inserción de datos en la tabla de relaciones entre productos y categorías
INSERT INTO product_categories (product_id, category_id)
VALUES
  ('PRD001', 'CAT001'),
  ('PRD002', 'CAT002'),
  ('PRD003', 'CAT003'),
  ('PRD004', 'CAT004');

-- Inserción de datos en la tabla de pedidos
INSERT INTO orders (order_number, user_id, product_category_id, quantity, order_date)
VALUES
  ('ORD001', 1, 1, 2, '2023-06-27 10:15:00'),
  ('ORD002', 2, 3, 1, '2023-06-27 11:30:00'),
  ('ORD003', 1, 4, 3, '2023-06-27 14:45:00'),
  ('ORD004', 3, 2, 1, '2023-06-27 16:20:00'),
  ('ORD005', 2, 4, 2, '2023-06-27 18:05:00');


````



## Script

````sql
-- Creación de la base de datos
CREATE DATABASE Fz3r0_Corporations CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

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
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

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
  FOREIGN KEY (proveedor_id) REFERENCES proveedores(id)
);

-- Creación de la tabla 'proveedores'
CREATE TABLE proveedores (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre_empresa VARCHAR(100) NOT NULL,
  direccion VARCHAR(200) NOT NULL,
  telefono VARCHAR(20) NOT NULL,
  correo_electronico VARCHAR(100) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Creación de la tabla 'ventas'
CREATE TABLE ventas (
  id INT AUTO_INCREMENT PRIMARY KEY,
  fecha_venta DATETIME NOT NULL,
  total DECIMAL(10, 2) NOT NULL,
  usuario_id INT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (usuario_id) REFERENCES usuarios(id)
);

-- Creación de la tabla 'detalles_venta'
CREATE TABLE detalles_venta (
  venta_id INT,
  producto_id INT,
  cantidad INT NOT NULL,
  precio_unitario DECIMAL(10, 2) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (venta_id, producto_id),
  FOREIGN KEY (venta_id) REFERENCES ventas(id),
  FOREIGN KEY (producto_id) REFERENCES productos(id)
);

-- Creación de la tabla 'categorias'
CREATE TABLE categorias (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  descripcion TEXT,

````

### Agregar datos de prueba

````sql
-- Inserción de datos en la tabla 'usuarios'
INSERT INTO usuarios (username, password, name, address, phone, mail, subscription_type)
VALUES
    ('mario', 'mushroom1', 'Mario Plumber', '123 Pipe St', '555-1234', 'mario@example.com', 'premium'),
    ('luigi', 'green456', 'Luigi Bro', '456 Mansion Ave', '555-5678', 'luigi@example.com', 'basic'),
    ('link', 'master123', 'Link Hero', '789 Hyrule Rd', '555-9876', 'link@example.com', 'basic'),
    ('sonic', 'gottagofast', 'Sonic Hedgehog', '321 Speedy Ln', '555-2468', 'sonic@example.com', 'premium'),
    ('megaman', 'bluebomber', 'Mega Man', '654 Pixel St', '555-1357', 'megaman@example.com', 'basic'),
    ('samus', 'powersuit7', 'Samus Aran', '987 Bounty Rd', '555-7890', 'samus@example.com', 'basic'),
    ('cloud', 'busterblade', 'Cloud Strife', '159 Mako Blvd', '555-3690', 'cloud@example.com', 'premium');

-- Inserción de datos en la tabla 'proveedores'
INSERT INTO proveedores (nombre_empresa, direccion, telefono, correo_electronico)
VALUES
    ('ACME Corp', '42 Main St', '555-1111', 'info@acmecorp.com'),
    ('Stark Industries', '10880 Malibu Point', '555-2222', 'info@stark.com'),
    ('Wayne Enterprises', '1007 Mountain Drive', '555-3333', 'info@wayneenterprises.com'),
    ('Umbrella Corporation', '13 Raccoon St', '555-4444', 'info@umbrella.com'),
    ('Aperture Science', '742 Evergreen Terrace', '555-5555', 'info@aperturescience.com'),
    ('Weyland-Yutani Corp', '1401 Elm St', '555-6666', 'info@weyland-yutani.com'),
    ('Wonka Industries', '16 Chocolate Factory', '555-7777', 'info@wonkaindustries.com');

-- Inserción de datos en la tabla 'productos'
INSERT INTO productos (nombre, descripcion, precio, stock, proveedor_id)
VALUES
    ('Super Mushroom', 'Grow in size with this power-up!', 10.99, 100, 1),
    ('Master Sword', 'The legendary blade of evil''s bane', 99.99, 50, 2),
    ('Plasma Blaster', 'Extraterrestrial energy weapon', 499.99, 10, 3),
    ('T-Rex DNA Sample', 'Jurassic Park genetic material', 1999.99, 5, 4),
    ('Portal Gun', 'Device that creates portals for teleportation', 299.99, 20, 5),
    ('Lightsaber', 'Elegant weapon for a more civilized age', 499.99, 15, 6),
    ('Nuka-Cola', 'The refreshing taste of the post-apocalypse', 1.99, 200, 7);

-- Inserción de datos en la tabla 'ventas'
INSERT INTO ventas (fecha_venta, total, usuario_id)
VALUES
    ('2023-06-01 10:30:00', 50.99, 1),
    ('2023-06-02 14:45:00', 199.99, 2),
    ('2023-06-03 09:15:00', 499.99, 1),
    ('2023-06-04 11:30:00', 299.99, 3),
    ('2023-06-05 15:20:00', 10.99, 4),
    ('2023-06-06 16:45:00', 99.99, 5),
    ('2023-06-07 14:10:00', 1.99, 6);

-- Inserción de datos en la tabla 'detalles_venta'
INSERT INTO detalles_venta (venta_id, producto_id, cantidad, precio_unitario)
VALUES
    (1, 1, 3, 10.99),
    (1, 4, 1, 1999.99),
    (2, 3, 1, 499.99),
    (2, 5, 2, 299.99),
    (3, 1, 2, 10.99),
    (3, 6, 1, 99.99),
    (4, 2, 1, 199.99),
    (5, 4, 1, 1999.99),
    (5, 7, 5, 1.99),
    (6, 3, 1, 499.99),
    (7, 1, 1, 10.99),
    (7, 5, 1, 299.99);

````

### Programa de Python para agregar datos coherentemente

````py
# Título del programa
print("Fz3r0 - Generador de consultas para base de datos empresarial")

# Solicitar la opción al usuario
print("Seleccione una opción:")
print("1. Agregar Usuarios")
print("2. Agregar Productos")
print("3. Realizar una Venta")
opcion = input("Ingrese el número de la opción deseada: ")

# Según la opción seleccionada, ejecutar la operación correspondiente
if opcion == "1":
    # Solicitar información del usuario
    username = input("Ingrese el nombre de usuario: ")
    password = input("Ingrese la contraseña: ")
    name = input("Ingrese el nombre completo: ")
    address = input("Ingrese la dirección: ")
    phone = input("Ingrese el número de teléfono: ")
    email = input("Ingrese la dirección de correo electrónico: ")
    subscription_type = input("Ingrese el tipo de suscripción: ")

    # Generar el query para insertar los datos del usuario
    query = f"INSERT INTO usuarios (username, password, name, address, phone, mail, subscription_type) " \
            f"VALUES ('{username}', '{password}', '{name}', '{address}', '{phone}', '{email}', '{subscription_type}')"

    # Imprimir el query generado
    print("Query generado:")
    print(query)

elif opcion == "2":
    # Solicitar información del producto
    nombre = input("Ingrese el nombre del producto: ")
    descripcion = input("Ingrese la descripción del producto: ")
    precio = float(input("Ingrese el precio del producto: "))
    stock = int(input("Ingrese la cantidad en stock: "))
    proveedor_id = int(input("Ingrese el ID del proveedor: "))

    # Generar el query para insertar los datos del producto
    query = f"INSERT INTO productos (nombre, descripcion, precio, stock, proveedor_id) " \
            f"VALUES ('{nombre}', '{descripcion}', {precio}, {stock}, {proveedor_id})"

    # Imprimir el query generado
    print("Query generado:")
    print(query)

elif opcion == "3":
    # Solicitar información de la venta
    fecha_venta = input("Ingrese la fecha de la venta: ")
    total = float(input("Ingrese el monto total de la venta: "))
    usuario_id = int(input("Ingrese el ID del usuario: "))

    # Generar el query para insertar los datos de la venta
    query = f"INSERT INTO ventas (fecha_venta, total, usuario_id) " \
            f"VALUES ('{fecha_venta}', {total}, {usuario_id})"

    # Imprimir el query generado
    print("Query generado:")
    print(query)

else:
    print("Opción inválida. Por favor, seleccione una opción válida.")

````

## Descripción

La base de datos que hemos creado es un ejemplo de una base de datos para una empresa, con el propósito de gestionar usuarios, productos, proveedores y ventas. A continuación, te describo cómo funciona y su posible aplicación:

Usuarios:

Esta tabla almacena la información de los usuarios registrados en el sistema de la empresa.
Los usuarios pueden iniciar sesión utilizando su nombre de usuario y contraseña.
La tabla permite almacenar información personal de los usuarios, como su nombre, dirección, número de teléfono, correo electrónico y tipo de suscripción (básica o premium).
Los usuarios pueden tener distintos privilegios o funcionalidades según su tipo de suscripción.
La tabla utiliza un identificador único (id) como clave primaria para identificar a cada usuario.
Productos:

Esta tabla almacena información sobre los productos que la empresa ofrece.
Cada producto tiene un nombre, una descripción, un precio y un stock disponible.
Se registra el proveedor asociado a cada producto a través de la clave externa proveedor_id.
La tabla utiliza un identificador único (id) como clave primaria para identificar cada producto.
Los productos pueden estar asociados a una o varias categorías (a través de la tabla producto_categoria).
Proveedores:

Esta tabla almacena información sobre los proveedores que suministran productos a la empresa.
Se registra el nombre de la empresa, la dirección, el número de teléfono y el correo electrónico de cada proveedor.
La tabla utiliza un identificador único (id) como clave primaria para identificar a cada proveedor.
Ventas:

Esta tabla registra las ventas realizadas por la empresa.
Cada venta tiene una fecha y hora de realización, un total (monto) y se asocia a un usuario que la ha realizado.
La tabla utiliza un identificador único (id) como clave primaria para identificar cada venta.
Se registra el usuario asociado a cada venta a través de la clave externa usuario_id.
Detalles de venta:

Esta tabla guarda los detalles de cada venta, incluyendo los productos vendidos y las cantidades correspondientes.
Cada registro en esta tabla se asocia a una venta (a través de venta_id) y a un producto (a través de producto_id).
Se registra la cantidad de productos vendidos y el precio unitario en cada venta.
La combinación de venta_id y producto_id forma la clave primaria compuesta que identifica cada registro en esta tabla.

### Indices

¿Qué es un índice?

Un índice es una estructura que se crea en una o más columnas de una tabla para acelerar la búsqueda y recuperación de datos.
Un índice crea una copia ordenada de los valores de las columnas seleccionadas, lo que facilita la búsqueda rápida y eficiente de registros específicos.

¿Por qué se utilizan los índices?

Los índices mejoran el rendimiento de las consultas, ya que permiten que el motor de la base de datos encuentre los registros deseados de manera más eficiente.
Al utilizar un índice, la base de datos no tiene que realizar una búsqueda secuencial completa en la tabla, sino que puede saltar directamente a los registros relevantes.

Índices en nuestra base de datos:

Hemos agregado varios índices en nuestra base de datos para mejorar el rendimiento en las consultas comunes.
Por ejemplo, hemos agregado índices en los campos proveedor_id, usuario_id, producto_id, venta_id y categoria_id, ya que estas columnas son comúnmente utilizadas en consultas de búsqueda y relacionadas con otras tablas.
Los índices aceleran la búsqueda de registros que coinciden con los valores específicos en estas columnas, reduciendo el tiempo necesario para ejecutar las consultas.

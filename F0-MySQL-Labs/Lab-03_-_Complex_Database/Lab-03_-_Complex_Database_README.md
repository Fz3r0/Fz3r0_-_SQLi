

## Script

````sql
-- Creación de la base de datos
CREATE DATABASE mi_empresa CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Selección de la base de datos
USE mi_empresa;

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
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Creación de la tabla 'producto_categoria'
CREATE TABLE producto_categoria (
  producto_id INT,
  categoria_id INT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (producto_id, categoria_id),
  FOREIGN KEY (producto_id) REFERENCES productos(id),
  FOREIGN KEY (categoria_id) REFERENCES categorias(id)
);

-- Creación de índices
ALTER TABLE productos ADD INDEX idx_proveedor_id (proveedor_id);
ALTER TABLE ventas ADD INDEX idx_usuario_id (usuario_id);
ALTER TABLE detalles_venta ADD INDEX idx_producto_id (producto_id);
ALTER TABLE detalles_venta ADD INDEX idx_venta_id (venta_id);
ALTER TABLE producto_categoria ADD INDEX idx_categoria_id (categoria_id);

-- Creación de índice único en el campo 'username' de la tabla 'usuarios'
ALTER TABLE usuarios ADD UNIQUE INDEX idx_username (username);

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

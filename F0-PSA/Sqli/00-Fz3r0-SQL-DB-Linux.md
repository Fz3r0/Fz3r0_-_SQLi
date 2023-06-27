
## Instalar MySQL Linux

1. **Instalar MySQL**

    - Esto es necesario para hostear el Web server del Captive Portal (**en realidad solo es necesario instalar `mariadb`**)
    - [MySQL Install error fix](https://stackoverflow.com/questions/20259036/mysql-package-mysql-server-has-no-installation-candidate)
 
````sh
sudo apt-get install mariadb-server
````

2. Habiliar `Apache Server` y `MySQL` para visualizar localhost /var/www/html

````sh
# 1. Habilitar Apache y MySQL
service apache2 start && service mysql start  

# 2. Ahora abrir un firefox (super+shift+f) y navegar a localhost
localhost

    # - Ahora ya se debe tener un portal con 2 campos de texto, pero marcan error si se ingresa cualquier cosa, es porque se necesita una DB MYSQL
    # - Esto se hace con el archivo dbconnect.php muy útil para editar en caso de que se quieran más datos en la DB o hacerlo mas custom ;) 
    # - HAcer un car dbconnect.php dice mas que mil palabras, en la parte superior está el nombre de la DB y las variables que se están guardando!!!!
````

## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es **/var/lib/mysql**

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?

Nada, está vacía.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
```
docker run -d --name mysql-db --network net-wp -e MYSQL_ROOT_PASSWORD=root_password -e MYSQL_DATABASE=wordpress_db -e MYSQL_USER=wp_user -e MYSQL_PASSWORD=wp_password -v "C:\Users\Sofia\Documents\Sexto semestre\Construccion y Evolucion de Software\Practica3\ejercicio3\db"/db:/var/lib/mysql mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?

Se pueden observar los archivos y datos que crea mysql para almacenar la base de datos wordpress_db.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es **/var/www/html**

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
```
docker run -d --name wordpress-site --network net-wp -p 9500:80 -e WORDPRESS_DB_HOST=mysql-db -e WORDPRESS_DB_USER=wp_user -e WORDPRESS_DB_PASSWORD=wp_password -e WORDPRESS_DB_NAME=wordpress_db -v "C:\Users\Sofia\Documents\Sexto semestre\Construccion y Evolucion de Software\Practica3\ejercicio3"/var/www/html wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/cec5ba30-d761-4845-94f6-fda5b4099620" />

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

La configuracion y personalización agregada al blog de wordpress se mantiene por el volumen ya wue se almacenan en la dirección del host y los datos de wordpress tambien se guardan en la base de datos de msql.

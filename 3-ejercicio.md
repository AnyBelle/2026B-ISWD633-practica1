## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
docker network create -d bridge net-wp
#

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
En el esquema del ejercicio carpeta del contenedor (a) es /var/lib/mysql
Ruta carpeta host: C:/Users/User/Documents/Universidad/6 semestre/Evolución/Prácticas/P_1/ejercicio3/db
#

### ¿Qué contiene la carpeta db del host?
Inicialmente, la carpeta db del host está vacía, porque todavía no se ha creado e inicializado el contenedor de MySQL con el montaje correspondiente.
#

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
docker run -d --name mysql --network net-wp -v "C:/Users/User/Documents/Universidad/6 semestre/Evolución/Prácticas/P_1/ejercicio3/db:/var/lib/mysql" -e MYSQL_ROOT_PASSWORD=12345 -e MYSQL_DATABASE=wordpress -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin123 mysql:8
#

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
Después de crear e inicializar el contenedor de MySQL, la carpeta db contiene archivos y subcarpetas correspondientes a las bases de datos y al funcionamiento interno de MySQL. Estos archivos aparecen en mi computador gracias al bind mount y permite conservar la información.
# 

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html

Ruta carpeta host: C:/Users/User/Document/Universidad/6 semestre/Evolución/Prácticas/P_1/ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
docker run -d --name wordpress --network net-wp -p 9500:80 -v "C:/Users/User/Documents/Universidad/6 semestre/Evolución/Prácticas/P_1/ejercicio3/www:/var/www/html" -e WORDPRESS_DB_HOST=mysql:3306 -e WORDPRESS_DB_USER=admin -e WORDPRESS_DB_PASSWORD=admin123 -e WORDPRESS_DB_NAME=wordpress wordpress
# 

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
Al eliminar y crear nuevamente el contenedor de WordPress, se conservan la configuración del sitio, el tema activado y la entrada publicada. Esto sucede porque los archivos de WordPress permanecen en la carpeta www del host y el contenido del sitio continúa almacenado en MySQL. El nuevo contenedor utiliza los mismos archivos y se conecta a la misma base de datos, por lo que no es necesario instalar WordPress nuevamente.
#


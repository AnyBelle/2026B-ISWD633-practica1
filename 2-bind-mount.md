# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)

docker run -d --name nginx -p 8080:80 --mount "type=bind,source=C:/Users/User/Documents/Universidad/6 semestre/Evolución/Prácticas/P_1/nginx/html,target=/usr/share/nginx/html" nginx:alpine
#

### ¿Qué sucede al ingresar al servidor de nginx?
Al ingresar a http://localhost:8080, aparece el mensaje 403 Forbidden, esto se debe a que la carpeta html de mi computador está vacía y no contiene un archivo index.html que Nginx pueda mostrar.
#

### ¿Qué pasa con el archivo index.html del contenedor?
El archivo index.html original del contenedor queda oculto por el bind mount. No se elimina ni se copia al computador ya que al montar mi carpeta html en /usr/share/nginx/html, Nginx accede al contenido de mi carpeta.
#

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
Al ingresar nuevamente a http://localhost:8080, se muestra la página web del template descargado. Gracias al bind mount, Nginx accede a los archivos que descomprimí en mi carpeta html y los muestra sin necesidad de recrear el contenedor.
#

### Eliminar el contenedor
docker rm nginx
#

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
Al crear nuevamente el contenedor con el mismo bind mount e ingresar a http://localhost:8080, se muestra otra vez la página del template. Esto ocurre porque los archivos permanecen guardados en la carpeta html de mi computador y no se eliminan al borrar el contenedor. El nuevo contenedor accede a esos mismos archivos mediante el montaje.
#


#

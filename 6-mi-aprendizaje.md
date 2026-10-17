# COMPLETAR  
Comparando sus conocimientos antes de hacer la práctica con sus conocimientos después de hacer la tarea, explicar los principales aprendizajes logrados para beneficio de su formación profesional.  
Si solucionó un problema presentado o utilizó otros comandos que no se mencionan al realizar la práctica también se debe documentar.

### Principales aprendizajes logrados
Antes de realizar la práctica, tenía conocimientos básicos sobre Docker, pero no comprendía claramente cómo conservar la información de los contenedores ni cómo conectar varios servicios. Después de realizar los ejercicios, aprendí a crear, detener y eliminar contenedores, configurar variables de entorno y publicar puertos para acceder a las aplicaciones desde el navegador.

También aprendí a diferenciar los bind mounts, los volúmenes nombrados y los volúmenes anónimos. Con los bind mounts comprobé que un contenedor puede utilizar archivos de una carpeta de mi computador.Mientras que con los volúmenes nombrados comprendí cómo Docker administra el almacenamiento sin que sea necesario indicar una ruta del host. Además, identifiqué que los volúmenes anónimos reciben un identificador generado por Docker.

Otro aprendizaje fue la comunicación entre contenedores mediante redes de tipo bridge. Configuré WordPress con MySQL y Drupal con PostgreSQL, utilizando los nombres de los contenedores para establecer las conexiones. Al eliminar y recrear el contenedor de WordPress, comprobé que el sitio, el tema y la entrada se conservaban gracias al almacenamiento persistente.

Estos conocimientos aportan a mi formación profesional porque me permiten preparar entornos de desarrollo con varios servicios y comprender la relación entre aplicaciones, bases de datos, redes y almacenamiento.

### Problemas y ajustes documentados
Durante la práctica, ajusté los comandos de montaje colocando entre comillas las rutas de Windows que contenían espacios ya que no se reconocían caracteres especiales sin comillas, por ejemplo: docker run -d --name nginx -p 8080:80 --mount "type=bind,source=C:/Users/User/Documents/Universidad/6 semestre/Evolución/Prácticas/P_1/nginx/html,target=/usr/share/nginx/html" nginx:alpin

También comprendí que montar una carpeta vacía sobre el directorio de Nginx oculta su contenido original, lo que provocó el mensaje 403 Forbidden. 

Aprendí que varios contenedores pueden utilizar el mismo puerto interno, como el 80, siempre que se publiquen en puertos diferentes del computador ya que se usó el puerto 80 tanto en Nginx y WordPress. Para utilizar el puerto 9500 con pgAdmin, detuve previamente WordPress, que tenía asignado ese puerto.

Además, utilicé docker stop para detener los contenedores antes de eliminarlos con docker rm, sin recurrir a una eliminación forzada. 

Por úlitmo, durante la configuración de Drupal, utilicé server-postgres como nombre del servidor de base de datos, en lugar de localhost, para conectarlo con PostgreSQL mediante la red Docker.

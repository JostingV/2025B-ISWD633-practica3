## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
docker network create net-wp

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es: C:\Users\Josti\Desktop\ejercicio3\db

Ruta carpeta host: C:\Users\Josti\Desktop\ejercicio3\db

### ¿Qué contiene la carpeta db del host?
Está carpeta diseñada para contener los archivos de datos de la base de datos MySQL (tablas, índices, logs, etc.), asegurando que la información de la base de datos sea persistente incluso si el contenedor MySQL es eliminado y recreado.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
C:\Users\Josti>docker run -d --name contenedor-mysql --network net-wp -v /c/Users/Josti/Desktop/ejercicio3/db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=wordpress_db -e MYSQL_USER=wp_user -e MYSQL_PASSWORD=wppassword mysql:8

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
La carpeta db del host contendrá ahora una estructura de directorios y archivos propia de MySQL. Estos archivos son creados por el contenedor MySQL al iniciarse por primera vez para inicializar su base de datos.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es: C:\Users\Josti\Desktop\ejercicio3\www

Ruta carpeta host: C:\Users\Josti\Desktop\ejercicio3\www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
C:\Users\Josti>docker run -d --name contenedor-wordpress --network net-wp -p 9500:80 -v /c/Users/Josti/Desktop/ejercicio3/www:/var/www/html -e WORDPRESS_DB_HOST=contenedor-mysql -e WORDPRESS_DB_USER=wp_user -e WORDPRESS_DB_PASSWORD=wppassword -e WORDPRESS_DB_NAME=wordpress_db wordpress

<img width="1919" height="1030" alt="image" src="https://github.com/user-attachments/assets/dda34771-a526-43df-94e3-ce6cefa9b696" />

### Personalizar la apariencia de wordpress y agregar una entrada
<img width="1919" height="1029" alt="image" src="https://github.com/user-attachments/assets/6467f1fa-8296-4df7-8318-dcfb4fcc753f" />

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
<img width="834" height="67" alt="image" src="https://github.com/user-attachments/assets/6357ff41-330e-4758-a1a7-4213711f5ca6" />

Aunque que se elimine el contener de Docker, tenemos persistencia de Archivos y contenido debido a que estos se almacen de maneral local en las carpetas creadas anteriomente.


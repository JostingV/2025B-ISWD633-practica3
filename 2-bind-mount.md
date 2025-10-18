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

docker run -d --name mi-nginx -p 8080:80 -v /c/Users/Josti/Desktop/nginx/html:/usr/share/nginx/html nginx:alpine
<img width="1464" height="149" alt="image" src="https://github.com/user-attachments/assets/299b9596-aa8d-4ee2-b51b-41ca88a66dea" />

### ¿Qué sucede al ingresar al servidor de nginx?
<img width="1919" height="1031" alt="image" src="https://github.com/user-attachments/assets/9b2007e7-a186-4d7a-a623-eabf44a2ed48" />

Al ingresar al servidor se muestra un directorio vacio con un mensaje de error "403 Forbidden" esto significa que la carpeta nginx/html en el host está vacía y no tiene un archivo index.html.

### ¿Qué pasa con el archivo index.html del contenedor?
Como ejecutamos el comando con el volumen -v, el archivo original se ocualta, entonces antes del montaje la imagen viene con un archivo html por defecto,
cuando realizo el montaje la calpeta local que cree, se sobre poner sobre /usr/share/nginx/html por ello el contenido original del contenedor queda oculto y solo muestra el contenido de mi carpeta local.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
Sigue mostrando un directorio vacio con el mensaje de error nombrado anteriormente.

### Eliminar el contenedor
docker rm -f mi-nginx

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
<img width="1461" height="130" alt="image" src="https://github.com/user-attachments/assets/1b14e1fe-f39a-4768-be66-b1193256bfaa" />
<img width="1919" height="1036" alt="image" src="https://github.com/user-attachments/assets/abf29f9d-cd74-4033-a78a-9baa0efecffb" />
El servidor de Nginx muestra el template web descargado y descomprimido ya que los archivos se encuentran en la carpeta local nginx/html.



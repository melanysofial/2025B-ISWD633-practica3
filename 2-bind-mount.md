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

```
docker run -d --name nginx -p 8080:80 -v "C:\Users\Sofia\Documents\Sexto semestre\Construccion y Evolucion de Software\nginx\html":/usr/share/nginx/html nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?

La pagina con el puerto mapeado de 8080 se presenta mostrando el error 403, ya que la carpeta html está vacía.


### ¿Qué pasa con el archivo index.html del contenedor?

Al realizar el volúmen se está usando mi carpeta y no la carpeta del contenedor, por lo que el index.html de nginx ya no se usa.


### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?

Se carga el index del template que se descargó ya que esta dentro de la carpeta html.

### Eliminar el contenedor
```
docker rm -f nginx
```

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?

Se vuelve a mostrar el contenido del template descargado ya que se guardó en la carpeta html de mi computadora (host). Esto demuestra que con el volumen, los datos permanecen incluso si el contenedor se borra.

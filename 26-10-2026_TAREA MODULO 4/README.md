# Tarea 4.2

## 1. Crear los siguientes volúmenes con la orden docker:

- **volumen_datos**

  **docker volume create volumen_datos**

  ![](/IMAGENES/image1.jpg)

- **volumen_web**

  **docker volume create volumen_web**

## 2. Una vez creados estos contenedores:

- **Arrancar un contenedor llamado c1 sobre la imagen php:7.4-apache que monte el volumen_web en la ruta /var/www/html**

  **docker run -d --name c1 -v volumen_web:/var/www/html php:7.4-apache**

  ![](/IMAGENES/image2.jpg)

- **Arrancar un contenedor llamado c2 sobre la imagen mariadb que monte el volumen_datos en la ruta /var/lib/mysql y cuya contraseña de root sea admin.**

  **docker run -d --name c2 -v volumen_datos:/var/lib/mysql -e MARIADB_ROOT_PASSWORD=admin mariadb**

  ![](/IMAGENES/image3.jpg)

Comprobamos los contenedores:

**docker ps -a**

## 3.- Parar y borrar el contenedor c2 y tras ello borrar el volumen volumen_datos.

### 1. Parar el contenedor c2

**docker stop c2**

![](/IMAGENES/image4.jpg)

### 2. Borrar el contenedor c2

**docker rm c2**

![](/IMAGENES/image5.jpg)

### 3. Borrar el volumen volumen_datos

**docker volume rm volumen_datos**

![](/IMAGENES/image6.jpg)

### 4. Comprobación final

**docker ps -a**

![](/IMAGENES/image7.jpg)

**docker volume ls**

![](/IMAGENES/image8.jpg)

---

# Tarea 4.3

## 1.- Crea una carpeta llamada saludo y dentro de ella crea un fichero llamado index.html con el siguiente contenido:

`<h1>HOLA SOY XXXXXX</h1>`

Deberás sustituir ese XXXXX por tu nombre.

![](/IMAGENES/image9.jpg)

![](/IMAGENES/image10.jpg)

## 2.- Una vez hecho esto arrancar dos contenedores basados en la imagen php:7.4-apache que hagan un bind mount de la carpeta saludo en la carpeta /var/www/html del contenedor.

**docker run -d --name c1 -p 8181:80 -v "${PWD}\saludo:/var/www/html" php:7.4-apache**

![](/IMAGENES/image11.jpg)

**docker run -d --name c2 -p 8282:80 -v "${PWD}\saludo:/var/www/html" php:7.4-apache**

![](/IMAGENES/image12.jpg)

Comprobar que funcionan:

**docker ps**

![](/IMAGENES/image13.jpg)

Comprobamos desde el navegador:

![](/IMAGENES/image14.jpg)

![](/IMAGENES/image15.jpg)

---

# Tarea 4.4

Creamos la carpeta y el archivo

![](/IMAGENES/image16.jpg)

Creamos Dockerfile:

![](/IMAGENES/image17.jpg)

Construimos la imagen:

**docker build -t php-debug**

![](/IMAGENES/image18.jpg)

Arrancamos el contenedor:

**docker run -d --name debugPHP -p 8585:80 -p 9003:9003 -v "${PWD}\debug:/var/www/html" php-debug**

![](/IMAGENES/image19.jpg)

Comprobamos desde terminal:

![](/IMAGENES/image20.jpg)

Comprobamos desde navegador:

![](/IMAGENES/image21.jpg)

Vemos el bind mount:

![](/IMAGENES/image22.jpg)

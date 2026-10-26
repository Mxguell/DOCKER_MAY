# Tarea 4.2

## 1. Crear los siguientes volúmenes con la orden docker volume:

**volumen_datos**
```bash
docker volume create volumen_datos
```
  ![Imagen 1](IMAGENES/image1.png)

**volumen_web**

```bash
docker volume create volumen_web
```
  ![Imagen 1](IMAGENES/image2.png)

## 2. Una vez creados estos contenedores:

**Arrancar un contenedor llamado c1 sobre la imagen php:7.4-apache que monte el volumen_web en la ruta /var/www/html**

```bash
docker run -d --name c1 -v volumen_web:/var/www/html php:7.4-apache
```

  ![Imagen 2](IMAGENES/image3.png)

**Arrancar un contenedor llamado c2 sobre la imagen mariadb que monte el volumen_datos en la ruta /var/lib/mysql y cuya contraseña de root sea admin.**

```bash
docker run -d --name c2 -v volumen_datos:/var/lib/mysql -e MARIADB_ROOT_PASSWORD=admin mariadb
```

  ![Imagen 3](IMAGENES/image4.png)

Comprobamos los contenedores:

```bash
docker ps -a
```
  ![Imagen 3](IMAGENES/image5.png)

## 3.- Parar y borrar el contenedor c2 y tras ello borrar el volumen volumen_datos.

### 1. Parar el contenedor c2

```bash
docker stop c2
```

![Imagen 4](IMAGENES/image6.png)

### 2. Borrar el contenedor c2

```bash
docker rm c2
```

![Imagen 5](IMAGENES/image7.png)

### 3. Borrar el volumen volumen_datos

```bash
docker volume rm volumen_datos
```

![Imagen 6](IMAGENES/image8.png)

### 4. Comprobación final

```bash
docker ps -a
```

![Imagen 7](IMAGENES/image9.png)

```bash
docker volume ls
```

![Imagen 8](IMAGENES/image10.png)

---

# Tarea 4.3

## 1. Crea una carpeta llamada saludo y dentro de ella crea un fichero llamado index.html con el siguiente contenido:

`<h1>HOLA SOY XXXXXX</h1>`

Deberás sustituir ese XXXXX por tu nombre.

![Imagen 9](IMAGENES/image11.png)

![Imagen 10](IMAGENES/image12.png)

## 2. Una vez hecho esto arrancar dos contenedores basados en la imagen php:7.4-apache que hagan un bind mount de la carpeta saludo en la carpeta /var/www/html del contenedor.

```bash
docker run -d --name c1 -p 8181:80 -v "${PWD}\saludo:/var/www/html" php:7.4-apache
```

![Imagen 11](IMAGENES/image13.png)

```bash
docker run -d --name c2 -p 8282:80 -v "${PWD}\saludo:/var/www/html" php:7.4-apache
```

![Imagen 12](IMAGENES/image14.png)

Comprobar que funcionan:

```bash
docker ps
```

![Imagen 13](IMAGENES/image15.png)

Comprobamos desde el navegador:

![Imagen 14](IMAGENES/image16.png)

![Imagen 15](IMAGENES/image17.png)

---

# Tarea 4.4

Creamos la carpeta y el archivo

![Imagen 16](IMAGENES/image18.png)

Creamos Dockerfile:

![Imagen 17](IMAGENES/image19.png)

Construimos la imagen:

```bash
docker build -t php-debug
```

![Imagen 18](IMAGENES/image20.png)

Arrancamos el contenedor:

```bash
docker run -d --name debugPHP -p 8585:80 -p 9003:9003 -v "${PWD}\debug:/var/www/html" php-debug
```

![Imagen 19](IMAGENES/image21.png)

Comprobamos desde terminal:

![Imagen 20](IMAGENES/image22.png)

Comprobamos desde navegador:

![Imagen 21](IMAGENES/image23.png)

Vemos el bind mount:

![Imagen 22](IMAGENES/image24.png)

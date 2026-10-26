
# Tarea 4.2

## 1. Creación de volúmenes Docker

Creamos los siguientes volúmenes con la orden Docker:

### Volumen `volumen_datos`

```bash
docker volume create volumen_datos
```

![Creación del volumen volumen_datos](IMAGENES/image1.png)

### Volumen `volumen_web`

```bash
docker volume create volumen_web
```

## 2. Creación y configuración de contenedores

### Arranque del contenedor `c1`

Arrancamos un contenedor llamado `c1` sobre la imagen `php:7.4-apache` que monte el volumen `volumen_web` en la ruta `/var/www/html`.

```bash
docker run -d --name c1 -v volumen_web:/var/www/html php:7.4-apache
```

![Creación del contenedor c1](IMAGENES/image2.png)

### Arranque del contenedor `c2`

Arrancamos un contenedor llamado `c2` sobre la imagen `mariadb` que monte el volumen `volumen_datos` en la ruta `/var/lib/mysql` y cuya contraseña de root sea `admin`.

```bash
docker run -d --name c2 -v volumen_datos:/var/lib/mysql -e MARIADB_ROOT_PASSWORD=admin mariadb
```

![Creación del contenedor c2](IMAGENES/image3.png)

### Comprobación de los contenedores

Comprobamos los contenedores:

```bash
docker ps -a
```

## 3. Eliminación del contenedor `c2` y del volumen `volumen_datos`

### 3.1. Parar el contenedor `c2`

```bash
docker stop c2
```

![Parada del contenedor c2](IMAGENES/image4.png)

### 3.2. Borrar el contenedor `c2`

```bash
docker rm c2
```

![Eliminación del contenedor c2](IMAGENES/image5.png)

### 3.3. Borrar el volumen `volumen_datos`

```bash
docker volume rm volumen_datos
```

![Eliminación del volumen volumen_datos](IMAGENES/image6.png)

### 3.4. Comprobación final

Comprobamos los contenedores existentes:

```bash
docker ps -a
```

![Comprobación final de los contenedores](IMAGENES/image7.png)

Comprobamos los volúmenes existentes:

```bash
docker volume ls
```

![Comprobación final de los volúmenes](IMAGENES/image8.png)

---

# Tarea 4.3

## 1. Creación de la carpeta y del archivo HTML

Crea una carpeta llamada `saludo` y dentro de ella crea un fichero llamado `index.html` con el siguiente contenido:

```html
<h1>HOLA SOY XXXXXX</h1>
```

Deberás sustituir ese XXXXX por tu nombre.

![Creación de la carpeta saludo](IMAGENES/image9.png)

![Creación del archivo index.html](IMAGENES/image10.png)

## 2. Arranque de dos contenedores con bind mount

Una vez hecho esto, arrancamos dos contenedores basados en la imagen `php:7.4-apache` que hagan un bind mount de la carpeta `saludo` en la carpeta `/var/www/html` del contenedor.

### Contenedor `c1`

```powershell
docker run -d --name c1 -p 8181:80 -v "${PWD}\saludo:/var/www/html" php:7.4-apache
```

![Arranque del contenedor c1](IMAGENES/image11.png)

### Contenedor `c2`

```powershell
docker run -d --name c2 -p 8282:80 -v "${PWD}\saludo:/var/www/html" php:7.4-apache
```

![Arranque del contenedor c2](IMAGENES/image12.png)

### Comprobación de los contenedores

Comprobar que funcionan:

```bash
docker ps
```

![Comprobación de los contenedores en ejecución](IMAGENES/image13.png)

### Comprobación desde el navegador

Comprobamos desde el navegador:

![Comprobación del primer contenedor desde el navegador](IMAGENES/image14.png)

![Comprobación del segundo contenedor desde el navegador](IMAGENES/image15.png)

---

# Tarea 4.4

## 1. Creación de la carpeta y del archivo

Creamos la carpeta y el archivo.

![Creación de la carpeta y del archivo](IMAGENES/image16.png)

## 2. Creación del Dockerfile

Creamos Dockerfile:

![Creación del Dockerfile](IMAGENES/image17.png)

## 3. Construcción de la imagen Docker

Construimos la imagen:

```bash
docker build -t php-debug
```

![Construcción de la imagen php-debug](IMAGENES/image18.png)

## 4. Arranque del contenedor

Arrancamos el contenedor:

```powershell
docker run -d --name debugPHP -p 8585:80 -p 9003:9003 -v "${PWD}\debug:/var/www/html" php-debug
```

![Arranque del contenedor debugPHP](IMAGENES/image19.png)

## 5. Comprobaciones

### Comprobación desde la terminal

Comprobamos desde terminal:

![Comprobación desde la terminal](IMAGENES/image20.png)

### Comprobación desde el navegador

Comprobamos desde navegador:

![Comprobación desde el navegador](IMAGENES/image21.png)

### Comprobación del bind mount

Vemos el bind mount:

![Comprobación del bind mount](IMAGENES/image22.png)

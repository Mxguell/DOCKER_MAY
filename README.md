# Tarea módulo 2: Ejecutando y gestionando contenedores

## 1. Instalación de imágenes

Instalamos los siguientes servicios mediante el comando `docker pull`:

    docker pull ubuntu:18.04

![Ubuntu Instalado](IMAGENES/image1.png)

    docker pull centos:8

![CentOS Instalado](IMAGENES/image2.png)

    docker pull debian:9

![Debian Instalado](IMAGENES/image3.png)

    docker pull mariadb:latest

![MariaDB Instalado](IMAGENES/image4.png)

    docker pull mysql:5.7

![MySQL Instalado](IMAGENES/image5.png)

Ejecutamos `docker images` para comprobar que se han descargado correctamente:

    docker images

![Imágenes Docker](IMAGENES/image6.png)

## 1.2. Arrancar un contenedor

### 1.2.1. Salir del contenedor y comprobar que se ha parado

    docker run -it --name ubuntu ubuntu:18.04

![Contenedor Ubuntu Arrancado](IMAGENES/image7.png)

Dentro del contenedor, salimos con:

    exit

Comprobamos que el contenedor se ha parado:

    docker ps -a

![Contenedor Ubuntu Parado](IMAGENES/image8.png)

### 1.2.2. Rearrancar el contenedor desde el equipo

    docker start ubuntu

    docker ps

![Contenedor Ubuntu Funcionando](IMAGENES/image9.png)

### 1.2.3. Mostrar `/etc/os-release` sin entrar en el contenedor

    docker exec ubuntu cat /etc/os-release

![Información del Sistema Ubuntu](IMAGENES/image10.png)

## 1.3. Ejecutando servicios desde contenedores

### 1.3.1. Arrancar un servidor web Apache con PHP

Arrancamos un contenedor llamado `web` con la imagen `php:7.3-apache`, accesible desde el equipo por el puerto `8181`.

    docker run -d --name web -p 8181:80 php:7.3-apache

![Servidor Web Apache Arrancado](IMAGENES/image11.png)

Comprobamos que está funcionando:

    docker ps

![Contenedor Web Funcionando](IMAGENES/image12.png)

### 1.3.2. Copiar `index.html` al directorio raíz del servidor web

![Archivo index.html](IMAGENES/image13.png)

    docker cp index.html web:/var/www/html/index.html

![Archivo index.html Copiado](IMAGENES/image14.png)

### 1.3.3. Copiar `index.php` al directorio raíz del servidor web
![Archivo index.php Copiado](IMAGENES/image15.png)

    docker cp index.php web:/var/www/html/index.php

![Archivo index.php Copiado](IMAGENES/image16.png)

### 1.3.3.1 Probamos a entrar desde el navegador

![Archivo index.Desde el navegador](IMAGENES/image22.png)
![Archivo php.Desde el navegador](IMAGENES/image23.png)

### 1.3.4. Arrancar una base de datos MariaDB

Arrancamos un contenedor llamado `bbdd` con la imagen `mariadb:latest`, accesible desde el puerto `3336`.

- Contraseña de `root`: `root`.
- Base de datos creada automáticamente: `prueba`.
- Usuario: `invitado`.
- Contraseña del usuario: `invitado`.

      docker run -d --name bbdd -p 3336:3306 -e MARIADB_ROOT_PASSWORD=root -e MARIADB_DATABASE=prueba
      -e MARIADB_USER=invitado -e MARIADB_PASSWORD=invitado mariadb:latest

![Base de Datos MariaDB Arrancada](IMAGENES/image17.png)

Probamos desde Docker primero:
![Probamos a entrar desde docker a la BDD](IMAGENES/image25.png)

Entramos desde un cliente (DBeaver)
![Entramos desde DBeaver a la BBDD](IMAGENES/image24.png)

## 1.4. Obtener información de los contenedores

### Dirección IP del contenedor web

    docker inspect web | findstr "Ip"

![Dirección IP del Contenedor Web](IMAGENES/image18.png)

### Redirección de puertos del contenedor web

    docker port web

![Puertos del Contenedor Web](IMAGENES/image19.png)

### Dirección IP del contenedor bbdd

    docker inspect bbdd | findstr "Ip"

![Dirección IP del Contenedor MariaDB](IMAGENES/image20.png)

### Redirección de puertos del contenedor bbdd

    docker port bbdd

![Puertos del Contenedor MariaDB](IMAGENES/image21.png)

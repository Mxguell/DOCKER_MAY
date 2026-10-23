
# Práctica 3. Gestión de imágenes y contenedores en Docker

## 1. Descargar la imagen de Ubuntu 20.04

En primer lugar, descargamos la imagen oficial de Ubuntu 20.04 desde Docker Hub mediante el siguiente comando:

```bash
docker pull ubuntu:20.04
```

**1.1** Descarga de la imagen de Ubuntu 20.04.

![image1.png](IMAGENES/image1.png)

Una vez finalizada la descarga, comprobamos que la imagen se encuentra disponible en nuestro sistema local:

```bash
docker images
```

**1.2** Verificación de la imagen descargada.

![image2.png](IMAGENES/image2.png)

## 2. Obtener la información de la imagen

Para consultar las características y la configuración de la imagen, utilizamos el comando `docker image inspect`. Redirigimos la salida a un archivo llamado `info.txt` para conservar toda la información obtenida.

```bash
docker image inspect ubuntu:20.04 > info.txt
```

A continuación, mostramos el contenido del archivo para comprobar que la información se ha guardado correctamente:

```bash
cat info.txt
```

**2.1** Obtención y visualización de la información de la imagen.

![image3.png](IMAGENES/image3.png)

## 3. Crear un contenedor llamado `modulo3`

A partir de la imagen descargada, creamos un contenedor con el nombre `modulo3` mediante el siguiente comando:

```bash
docker create --name modulo3 ubuntu:20.04
```

Este comando crea el contenedor, pero no lo inicia.

**3.1** Creación del contenedor `modulo3`.

![image4.png](IMAGENES/image4.png)

Para comprobar que el contenedor se ha creado correctamente, mostramos todos los contenedores del sistema, incluidos los que están detenidos:

```bash
docker ps -a
```

**3.2** Verificación de la creación del contenedor.

![image5.png](IMAGENES/image5.png)

## 4. Intentar eliminar la imagen de Ubuntu 20.04

Intentamos eliminar la imagen mediante el siguiente comando:

```bash
docker rmi ubuntu:20.04
```

**4.1** Intento de eliminación de la imagen.

![image6.png](IMAGENES/image6.png)

### Explicación del resultado

Docker impide la eliminación de la imagen cuando existe un contenedor que depende de ella. En este caso, el contenedor `modulo3` utiliza la imagen `ubuntu:20.04`, por lo que es necesario eliminar primero el contenedor antes de borrar la imagen.

Aunque existe la opción `docker rmi -f ubuntu:20.04` para forzar determinadas operaciones, no es la alternativa recomendada para esta práctica.

La solución más adecuada consiste en eliminar primero el contenedor asociado y, posteriormente, eliminar la imagen. De este modo, se respeta el orden de dependencias entre los recursos de Docker.

## 4.2 Eliminar el contenedor y la imagen

Para completar la práctica, realizamos las operaciones necesarias para eliminar ambos recursos.

### 4.2.1 Comprobar el estado del contenedor

En primer lugar, consultamos el listado de contenedores para verificar el estado de `modulo3`:

```bash
docker ps -a
```

![image7.png](IMAGENES/image7.png)

Si el contenedor estuviera en ejecución, sería necesario detenerlo antes de eliminarlo:

```bash
docker stop modulo3
```

![image8.png](IMAGENES/image8.png)

### 4.2.3 Eliminar el contenedor

Una vez detenido, si fuera necesario, eliminamos el contenedor `modulo3`:

```bash
docker rm modulo3
```

![image9.png](IMAGENES/image9.png)


A continuación, volvemos a consultar todos los contenedores para comprobar que se ha eliminado correctamente:

```bash
docker ps -a
```
![image10.png](IMAGENES/image10.png)

**4.2.4** Eliminación y comprobación del contenedor `modulo3`.

### 4.3 Eliminar la imagen de Ubuntu 20.04

Después de eliminar el contenedor, ejecutamos el comando para borrar la imagen:

```bash
docker rmi ubuntu:20.04
```
![image11.png](IMAGENES/image11.png)

Por último, comprobamos que la imagen ya no aparece en el listado de imágenes locales:

```bash
docker images
```
![image12.png](IMAGENES/image12.png)

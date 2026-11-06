
#Tarea 5.2
**1\. Creamos la primera red denominada “Red1”:**  

```bash
docker network create --driver bridge --subnet 172.28.0.0/16 --gateway 172.28.0.1 red1
```

**![](IMAGENES/image1.png)**  

**Esto crea la red con los siguientes datos:**

* **Nombre: redil**  
* **Driver: bridge**  
* **Dirección de red: 172.28.0.0**  
* **Máscara: 255.255.0.0**  
* **Gateway: 172.28.0.1**

**2\. Procedemos a crear la segunda red la cual denominaremos “Red2”:**  

```bash
docker network create --driver bridge red2
```

**![](IMAGENES/image2.png)**  

**3\. Comprobamos que efectivamente se han creado:**  

```bash
docker network ls
```

**![](IMAGENES/image3.png)**  

**4\. Inspeccionamos la red 1 y vemos la configuración que establecimos:**  

```bash
docker network inspect red1
```

**![](IMAGENES/image4.png)**  

**5\. Inspeccionamos la red 2 y vemos la configuración asignada por defecto:**  

```bash
docker network inspect red2
```

**![](IMAGENES/image5.png)**  

**Tarea 5.2**  

**1\. Comenzamos creando un contenedor (u1) poniendo en ejecución un contenedor de la imagen ubuntu:20.04:**  

```bash
docker run -dit --name u1 --hostname host1 --network red1 --ip 172.28.0.10 ubuntu:20.04
```

**![](IMAGENES/image6.png)**

**2\. Instalamos ping en el contenedor u1:**  

**1º Lo ejecutamos:**

```bash
docker exec -it u1 bash
```

**2º Instalamos ping:**

```bash
apt update && apt install inetutils-ping -y
```

**![](IMAGENES/image7.png)**  

**3º Comprobamos la configuración de red y el nombre de host:**

```bash
hostname
```

**![](IMAGENES/image8.png)**  

```bash
ip addr show
```

**![](IMAGENES/image9.png)**  

**3\. Creamos el segundo contenedor (u2)**

```bash
docker run -dit --name u2 --hostname host2 --network red2 ubuntu:20.04
```

**![](IMAGENES/image10.png)**  

**4\. Instalamos ping en u2:**  

**1º Lo ejecutamos:**

```bash
docker exec -it u2 bash
```

**2º Instalamos ping:**

```bash
apt update && apt install inetutils-ping -y
```

**![](IMAGENES/image11.png)**  

**3º Comprobamos la configuración de red y el nombre de host:**

```bash
hostname
```

**![](IMAGENES/image12.png)**  

```bash
ip addr show
```

**![](IMAGENES/image13.png)**  

**5\. Intentamos los pings**  

**Por nombre de host:**

```bash
ping host1
```

**![](IMAGENES/image14.png)**  

```bash
ping host2
```

**![](IMAGENES/image15.png)**  

**Por IP:**

```bash
ping 172.18.0.10 (IP u1)
```

**![](IMAGENES/image16.png)**  

```bash
ping 172.18.0.2 (IP u2)
```

**![](IMAGENES/image17.png)**  

**6\. Conectar u1 a la red2:**

```bash
docker network connect red2 u1
```

**![](IMAGENES/image18.png)**  

**7\. Comprobamos que ahora sí se ven:**  

**1º**

```bash
docker exec -it u1 bash
```

**![](IMAGENES/image19.png)**  

**2º**

```bash
ping 172.18.0.2 (IP u2)
```

**![](IMAGENES/image20.png)**

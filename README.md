# Fundamentos de Docker
## Seminario COMMLAB
#### Wilmer Moina-Rivera

## Instalación de Docker
Opciones de instalacion: 

### **Artefactos (paquetes para MAC, Windows y Linux)**

https://www.docker.com/get-started/

### **Manual**

https://docs.docker.com/desktop/ 

### **Script (Distribuciones Linux)**

Descargar:
```
wget -O docker-install.sh https://get.docker.com/ 
```
Dar permisos de ejecución al script:
```
sudo chmod a+x docker-install.sh
```
Ejecutar:
```
bash docker-install.sh
```
### **Comprobar instalación**

Comprobar version:
```
sudo docker --version 
```
Verifique que el motor Docker está instalado correctamente ejecutando la imagen hello-world:
```
sudo docker run hello-world
# Hello from Docker! 
```
> **Salida:** Este comando descarga una imagen de prueba y la ejecuta en un contenedor. Cuando el contenedor se ejecuta, imprime un mensaje y sale.

> Post-installation steps for Linux:

https://docs.docker.com/engine/install/linux-postinstall/

### **Alternativa si no lograron instalar docker:**
Usar Play with docker: https://labs.play-with-docker.com/ 

> Requisitos para usar **Play with docker**. Crear una cuenta en Docker hub: https://hub.docker.com 
## Primeros pasos con Docker
### **Paso-1: Estado de un contenedor:**

Ejecutar un contenedor:
```
docker run hello-world
```
Listar conenedores terminados:
```
docker ps
```
Inspeccionar un contenedor:
```
docker inspect <CONTAINER ID>
```
Agregar un nombre al contenedor:
```
docker run --name hello-commlab hello-world
```
### **Paso-2: Ejecutar un contenedor iterativo:**

Ejecutar un sistema operativo completo ubuntu:
```
docker run --name myubuntu -it ubuntu
```

### **Paso-3: Ciclo de vida de un contenedor:**

Ejecutar un sistema operativo completo ubuntu:
```
docker run --name myubuntu -it ubuntu
```
Ejecutar ubuntu con nuevo proceso principal:
```
docker run --name running -d ubuntu tail -f /dev/null
```
Mostrar el pid de un contendor:
```
docker inspect running --format '{{.State.Pid}}'
```
### **Paso-4: Exponer un contendor:**

Ejecutar y exponer servidor proxy:
```
docker run --name proxy -p 80:80 nginx
```

Ejecutar servidor proxy:
```
docker run -d --name proxy -p 80:80 nginx
```

### **Paso-5: Datos en Docker:**

Bind mounts:

docker run --name proxy -p 80:80 -v **/PATH_LOCAL:/PATH_      CONTENEDOR** nginx
```
docker run --name proxy -p 80:80 -v $PWD/dockerdata/:/usr/share/nginx/html nginx
```
Volúmenes:

Listar los volúmenes
```
docker volume ls
```

Crear un volúmen:
```
docker volume create web
```
Montar un volumen en un contendor:
```
docker run --name proxy -d -p 80:80 --mount src=web,dst=/usr/share/nginx/html nginx
```
Insertar y extraer archivos de un contenedor:

Crear el fichero a copiar:

```
echo "!Benvenuti al seminario CoMMLab -v1.1!" > ciao.html
```
Insertar el fichero en el contendor proxy:
```
docker cp ciao.html proxy:/usr/share/nginx/html
```
Extraer el fichero del contendor proxy:
```
docker cp ciao.html proxy:/usr/share/nginx/html
```
### **Paso-6: Imagenes:**
Decargar una imagen desde docker hub:
```
docker pull ubuntu:20
```
Construir una imagen:
```
docker build -t nginx:commlab .
```
Agregar un tag a la imagen:
```
docker build -t nginx:commlab .
```
### **Paso-7: Docker compose:**
Levantar los servicios:
```
docker-compose -f docker-compose.yml  up
```
Imprime el log de app
```
docker-compose logs -f app 
```
Bajar los servicios:
```
docker-compose -f docker-compose.yml  down
```
Compose en equipo:
```
cat <<EOF >>docker-compose.override.yml
version: "3.9"

services:
  app:
    build: .
    environment:
      COMMLAB: "Ciao commlab!!"
EOF
```
### **Paso-8: Administrando tu ambiente de Docker:**
Borrar todos los contenedores inactivos:
```
docker container prune
```
Borrar todo lo que no se esté usando
```
docker system prune 
```
Limitar la memoria:
```
docker run -d --name proxy --memory 1g nginx
```
Consumo de recursos:
```
docker stats
```
### **Paso-9: Docker Multi-Stage Build:**





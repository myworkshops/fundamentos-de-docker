# Fundamentos de Docker
#### Wilmer Moina-Rivera
##### Seminario COMMLAB

## Instalación de Docker

### Artefactos (paquetes)
https://www.docker.com/get-started/

### Manual
https://docs.docker.com/desktop/ 

### Script (Distribuciones Linux)
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
### Comprobar instalación
Comprobar version:
```
docker --version 
```
Verifique que el motor Docker está instalado correctamente ejecutando la imagen hello-world:
```
sudo docker run hello-world
# Hello from Docker! 
```
> **Salida:Hello from Docker!** Este comando descarga una imagen de prueba y la ejecuta en un contenedor. Cuando el contenedor se ejecuta, imprime un mensaje y sale.

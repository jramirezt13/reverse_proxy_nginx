# Proxy inverso

Implementación de un proxy inverso con nginx y docker.

## Ambiente de trabajo

* Debian 11
* Docker versión 20.10
* Docker compose versión 1.25.0
* Git
* Nginx
* Goaccess

## Instalación

Antes de realizar los pasos mencionados a continuación debe asegurarse sobre que sistema operativo esta trabajando ya que los comandos a ejecutar pueden variar un poco.


* **Instalación de docker**

Comparto el link con los metodos de instalación paso a paso:
 [Instalar Docker](https://docs.docker.com/get-docker/).

Nota: los pasos a  continuación son una copia de la pagina oficial.

 1. Abrir una terminal.

2. Actualizar el repositorio.
 ```bash
sudo apt-get update
```

3. Instalar certificados.
 ```bash
sudo apt-get install ca-certificates curl gnupg
```

4. Agregar la clave GPG oficial de Docker.
 ```bash
 sudo install -m 0755 -d /etc/apt/keyrings
 curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
 sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

5. Configurar el repositorio.
 ```bash
 echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
6. Actualizar el repositorio.
 ```bash
sudo apt-get update
```

7. Instalar la última versión.
 ```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

8. Verificar la instalación.
 ```bash
sudo docker run hello-world
```

Este comando descarga una imagen de prueba y la ejecuta en un contenedor.Cuando se ejecuta el contenedor, imprime un mensaje de confirmación y sale:

Ahora ha instalado y iniciado con éxito el motor Docker.


Otra forma para comprobar si se creo el contenedor es con el comando docker images.

 ```bash
sudo docker images

REPOSITORY          TAG       IMAGE ID       CREATED       SIZE
hello-world         latest    9c7a54a9a43c   3 weeks ago   13.3kB
```


* **Instalación de git**

1. Abrir una terminal y ejecutar:

```bash
sudo apt-get install git
```

2. Comprobar la instalación
```bash
git --version

git version 2.30.2
```

## Clonar proyecto de git

1. Desde la terminal crear una carpeta con el nombre y en el directorio que le guste.

```bash
mkdir proxy_nginx
```

2. Ingresar en el directorio creado

```bash
cd proxy_nginx
```

3. Clonar el proyecto que se encuentra en git

```bash
git clone https://github.com/jramirezt13/reverse_proxy_nginx.git
```

3. Verificar si se clonó el proyecto

```bash
ls  

reverse_proxy_nginx
```

## Ejecutar el contenedor.

1. Abrir una terminal e ingresar al directorio donde clono el proyecto y entrar a la carpeta docker.

```bash
cd /directorio_del_proyecto/reverse_proxy_nginx/docker
```
Nota: reemplazar "directorio_del_proyecto" por la ruta donde clono el proyecto.

2. Crear la carpeta "logs" que será usada por el contenedor para alojar los logs que generé la aplicación.

```bash
mkdir logs
```

2. Construir el contenedor con docker-compose.

```bash
docker-compose up --build -d
```

3. Verificar si levanto correctamente el contenedor

```bash
docker-compose ps

       Name                      Command               State                    Ports                  
-------------------------------------------------------------------------------------------------------
nginx_reverse_proxy   /docker-entrypoint.sh /bin ...   Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```

Para probar el funcionamiento del proxy se debe agregar el hostname al DNS local que se encuentra en /etc/hosts.


1. Editar el archivo con permisos de root

```bash
sudo vi /etc/hosts
```

2. Agregar el hostname "mytestapi.com" al final del archivo y guardas los cambios.

```bash
127.0.0.1	localhost
127.0.1.1	jramirez

127.0.1.1	mytestapi.com

```

3. Desde un explorador web ingresar la url:

https://mytestapi.com/sites

Debería mostrar un contenido parecido a un json.


 
## Ver las métricas del proxy.


Ingresar a la url http://localhost/goaccess/report.html






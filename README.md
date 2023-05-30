# Proxy inverso

Implementación de un proxy inverso con nginx y docker.

## Ambiente de trabajo

* Debian 11
* Docker versión 20.10
* Docker compose versión 1.25.0
* Git

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




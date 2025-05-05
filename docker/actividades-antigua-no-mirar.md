## ACTIVIDAD 1  
### Instalar Docker

1. Actualizamos el sistema:

```bash
sudo apt update


Instalamos los paquetes necesarios:

bash
Copiar
Editar
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y


Importamos la clave GPG de Docker:

bash
Copiar
Editar
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg


Añadimos el repositorio estable:

bash
Copiar
Editar
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
Instalamos Docker:

bash
Copiar
Editar
sudo apt install docker-ce docker-ce-cli containerd.io -y


Habilitamos y arrancamos el servicio:

bash
Copiar
Editar
sudo systemctl enable docker
sudo systemctl start docker


ACTIVIDAD 2
Práctica del primer artículo
Ejecutar imagen hello-world
bash
Copiar
Editar
docker run hello-world


Ver imágenes instaladas
bash
Copiar
Editar
docker images


Ver contenedores activos e inactivos
bash
Copiar
Editar
docker ps
docker ps -a


Práctica del segundo artículo
Crear cuenta en Docker Hub
Crear Dockerfile
bash
Copiar
Editar
mkdir mi_app && cd mi_app
Dockerfile:

Dockerfile
Copiar
Editar
FROM node:lts-alpine
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["node", "src/index.js"]


Construir la imagen
bash
Copiar
Editar
npm init
mkdir src && touch src/index.js
docker build -t josepepe313/mi_app:1.0 .


Ejecutar el contenedor
bash
Copiar
Editar
docker run -d -p 3000:3000 josepepe313/mi_app:1.0


Subir a Docker Hub
bash
Copiar
Editar
docker login
docker tag mi_app:1.0 josepepe313/mi_app:1.0
docker push josepepe313/mi_app:1.0


ACTIVIDAD 3
Descargar imágenes
bash
Copiar
Editar
docker pull ubuntu
docker pull hello-world
docker pull nginx


Ver imágenes
bash
Copiar
Editar
docker images


Crear contenedores con nombres
bash
Copiar
Editar
docker run --name myhello1 hello-world
docker run --name myhello2 hello-world
docker run --name myhello3 hello-world
Ver contenedores
bash
Copiar
Editar
docker ps -a


Detener contenedores
bash
Copiar
Editar
docker stop myhello1
docker stop myhello2
Eliminar contenedores
bash
Copiar
Editar
docker rm myhello1
Ver los activos:

bash
Copiar
Editar
docker ps
Eliminar todos los contenedores
bash
Copiar
Editar
docker rm -f $(docker ps -aq)
ACTIVIDAD 4
Volúmenes Docker
bash
Copiar
Editar
docker volume create web
docker run -d --name my-apache-app -v web:/usr/local/apache2/htdocs -p 8080:80 httpd:2.4
docker exec my-apache-app bash -c 'echo "<h1>Hola</h1>" > /usr/local/apache2/htdocs/index.html'
curl localhost:8080


Guestbook
bash
Copiar
Editar
docker network create guestbook
docker run -d --name redis --network guestbook -v /opt/redis:/data redis redis-server --appendonly yes
docker run -d -p 80:5000 --name guestbook --network guestbook iesgn/guestbook


Redes en Docker
bash
Copiar
Editar
docker run -it --name con1 --rm debian bash
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' con1
ACTIVIDAD 5
Docker Compose con Volumenes
yaml
Copiar
Editar
services:
  web:
    image: httpd
    volumes:
      - webdata:/usr/local/apache2/htdocs
volumes:
  webdata:
bash
Copiar
Editar
docker compose up -d
docker volume ls
Bind Mount con Compose
bash
Copiar
Editar
mkdir miweb
echo "<h1>Hola</h1>" > miweb/index.html
yaml
Copiar
Editar
services:
  web:
    image: httpd
    ports:
      - "8080:80"
    volumes:
      - ./miweb:/usr/local/apache2/htdocs
bash
Copiar
Editar
docker compose up -d
ACTIVIDAD 6
Versiones con Docker
Versión 1
bash
Copiar
Editar
git clone https://github.com/josedom24/curso_docker_ies
cd curso_docker_ies/ejemplos/modulo5/ejemplo1/version1
docker build -t version1 .
docker run -d -p 8080:80 version1
Versión 2
Modificar index.html y Dockerfile y luego:

bash
Copiar
Editar
docker build -t version2 .
docker run -d -p 8081:80 version2
Versión 3
Nueva modificación y despliegue:

bash
Copiar
Editar
docker build -t version3 .
docker run -d -p 8082:80 version3

**-----------------------------ACTIVIDAD 1-----------------------------------------------------**
  **intalar docker**
  primero hacemos un update

  sudo apt update
  
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/widd.png)

instalamos los paquetes

sudo apt install apt-transport-https ca-certificates curl software-properties-common -y

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzqwe.png)

importamos la clave GPG de Docker:
  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

  ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zgpg.png)

  añadir repositorio estable

  echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

  instalamos docker

  sudo apt install docker-ce docker-ce-cli containerd.io -y

  ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zindoc.png)

  Habilitamos y arrancamos el servicio de Docker

  sudo systemctl enable docker
  sudo systemctl start docker

  ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yhabi.png)

**-----------------------------ACTIVIDAD 2-----------------------------------------------------**
 **Lleva a cabo la práctica descrita en el primer artículo**

   parte 1:
   Ejecuta la imagen "hello-world"
   
   docker run hello-world
   
   ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zdoc.png)
   
   parte 2:
   Muestra las imágenes Docker instaladas
   
   docker images
   
   ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yim.png)
   
   parte 3:
   
   Muestra los contenedores Docker

   docker ps (este muestra solo los activos)

   docker ps -a (este muestra todos tanto los activos como los inactivos)

   ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ydocc.png)
   
**Lleva a cabo la práctica descrita en el segundo artículo**
paso 4:
  **crearse una cuenta en docker hub**

   parte 1:

   **Edita el fichero Dockerfile**

   crear un directorio para el y acceder a el

   mkdir mi_app && cd mi_app

   dentro de ese directorio crear un archivo sin extension con este contenido

FROM node:lts-alpine
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["node", "src/index.js"]

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzpo.png)

parte 2:
**Construye el contenedor**

hay que crear dos archivos un package.json y un src

package.joson

ejecutar npm init y seguir las preguntas que te hacen

crear el directorio src

mkdir src && touch src/index.js

y dentro del src poner un codigo de prueba

construimos la imagen

docker build -t josepepe313/mi_app:1.0 .

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zyic.png)

parte 3:

Ejecútalo

docker run -d -p 3000:3000 josepepe313/mi_app:1.0

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzpssso.png)

paso 5:

Publícalo

docker login
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yyrrr.png)

Etiquetar la imagen

docker tag mi_app:1.0 josepepe313/mi_app:1.0

Subir la imagen a Docker Hub:

docker push josepepe313/mi_app:1.0

**-----------------------------ACTIVIDAD 3-----------------------------------------------------**
**parte 1:**

Descarga la imagen de ubuntu

docker pull ubuntu

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yino.png)

**parte 2:**

Descarga la imagen de hello-world

docker pull hello-world

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yino.png)

**parte 3:**

Descarga la imagen nginx

docker pull nginx

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yino.png)

**parte 4:**

Muestra un listado de todas la imágenes

docker images

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zimagen.png)

**parte 5:**

Ejecuta un contenedor hello-world y dale nombre “myhello1”

docker run --name myhello1 hello-world

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzmiyon.png)

**parte 6:**

Ejecuta un contenedor hello-world y dale nombre “myhello2”

docker run --name myhello2 hello-world

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zwzyon.png)

**parte 7:**

Ejecuta un contenedor hello-world y dale nombre “myhello3”

docker run --name myhello3 hello-world

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zwzpon.png)

**parte 8:**

Muestra los contenedores que se están ejecutando

docker ps

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzwwe.png)

**parte 9:**

Para el contenedor "myhello1”

docker stop myhello1

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ystop1y2.png)

**parte 10:**

Para el contenedor "myhello2”
docker stop myhello2
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ystop1y2.png)

**parte 11:**
Borra el contenedor “myhello1”

docker rm myhello1
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzwedockerfin.png)

**parte 12:**

Muestra los contenedores que se están ejecutando.

docker ps -a
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzwedockerfin.png)

**parte 13:**

Borra todos los contenedores

docker rm $(docker ps -a -q)
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzwedockerfin.png)

**-----------------------------ACTIVIDAD 4-----------------------------------------------------**

**ejemplo1:**
 Crear un volumen llamado mi_volumen

 docker volume create mi_volumen

 ejecutar un contenedor utilizando el volumen

 docker run -d --name contenedor_nginx -v mi_volumen:/usr/share/nginx/html nginx

 ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yydockerf.png)
 
**ejemplo2:**

 Crear un directorio en el host

 mkdir -p ~/docker_bind_mount
echo "Hola desde Bind Mount" > ~/docker_bind_mount/index.html

docker run -d --name contenedor_nginx_bind -v ~/docker_bind_mount:/usr/share/nginx/html nginx

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yzfocker.png)

despues al ejecutar en el navegador http://localhost aparecerá el texto Bind Mount

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzydockernav.png)


**ejemplo3:**

Crear una red personalizada

docker network create mi_red
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zdockerred.png)

con esto ejecutamos dos contenedores en la misma red

docker run -d --name contenedor1 --network mi_red alpine sleep 1000
docker run -d --name contenedor2 --network mi_red alpine sleep 1000

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zdockerred.png)

verificamos la conectividad
ping contenedor2



**-----------------------------ACTIVIDAD 5-----------------------------------------------------**

**ejemplo1:**

git clone https://github.com/josedom24/curso_docker_ies.git
cd curso_docker_ies/modulo4

Inicia los servicios con Docker Compose
docker-compose up -d

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zindockercompose.png)

Verifica que los contenedores estén en funcionamiento:

docker-compose ps

**ejemplo2:**

Despliegue de la aplicación

entrar al directorio tempe y hacer lo mismo que arriba

docker-compose up -d

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zindockercompose.png)

Verifica que los contenedores estén en funcionamiento:

docker-compose ps


**ejemplo3:**

entrar al directorio wordpress y hacer lo mismo que arriba

docker-compose up -d

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zindockercompose.png)

Verifica que los contenedores estén en funcionamiento:

docker-compose ps

**-----------------------------ACTIVIDAD 6-----------------------------------------------------**

**ejemplo1:**
 crear un public_html

 # syntax=docker/dockerfile:1
FROM debian:stable-slim
RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*
WORKDIR /var/www/html/
COPY public_html .
EXPOSE 80
CMD apache2ctl -D FOREGROUND

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/6docker.png)

ejecutar el siguiente comando para construir la imagen

docker build -t josedom24/ejemplo1:v1 .

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/7docker.png)

 ejecutamos el contenedor

docker run -d -p 80:80 --name ejemplo1 josedom24/ejemplo1:v1

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/88.png)

y al poner localhost en la barra de navegacion aparece nuestra web

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/8.png)

**ejemplo 2 Construcción de imágenes con una una aplicación Python**
 lo mismo de antes pero el dockerfile tendrá este contenido

 # syntax=docker/dockerfile:1
FROM debian:12
RUN apt-get update && apt-get install -y python3-pip  && apt-get clean && rm -rf /var/lib/apt/lists/*
WORKDIR /usr/share/app
COPY app .
RUN pip3 install --no-cache-dir --break-system-packages -r requirements.txt
EXPOSE 3000
CMD python3 app.py

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/9.png)

y no olvidar crear un app.py

luego ejecutar este comnando

docker build -t josedom24/ejemplo3:v1 .

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/7docker.png)

y este otro para crear el contenedor

docker run -d -p 80:3000 --name ejemplo2 josedom24/ejemplo3:v1

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/88.png)

y al poner localhost en la barra de navegacion aparece nuestra web

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/8.png)

**ejemplo 3 Construcción de imágenes con una una aplicación PHP**

 crar el archivo info.php

 echo "<?php phpinfo(); ?>" > app/info.php

 ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/99.png)

 modificar el dockerfile con esto

 # syntax=docker/dockerfile:1
FROM debian:stable-slim
RUN apt-get update && apt-get install -y apache2 libapache2-mod-php7.4 php7.4 && apt-get clean && rm -rf /var/lib/apt/lists/* && rm /var/www/html/index.html
COPY app /var/www/html/
EXPOSE 80
CMD apache2ctl -D FOREGROUND

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/999.png)

construir imagen 

con este comando de aqui

docker build -t josedom24/ejemplo2:v1 .

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/7docker.png)

crear contenedor con este comando de aqui

docker run -d -p 80:80 --name ejemplo2 josedom24/ejemplo2:v1

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/88.png)

y al poner localhost en la barra de navegacion aparece nuestra web

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/8.png)



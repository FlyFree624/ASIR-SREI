# **-----------------------------ACTIVIDAD 1---------------------------------**

# INSTALAR DOCKER
  
▶️ 1) primero hacemos un update
   ```
   sudo apt update
   ```
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/widd.png)

▶️ 2) instalamos los paquetes
   ```
    $ sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
   ```
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzqwe.png)

▶️ 3) importamos la clave GPG de Docker:
   ```
    $ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```
  ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zgpg.png)

▶️ 4) añadir repositorio estable
   ```
    $ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee        $ /etc/apt/sources.list.d/docker.list > /dev/null
```

▶️ 5) instalamos docker
```
    $ sudo apt install docker-ce docker-ce-cli containerd.io -y
    ```
  ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zindoc.png)
   ```

▶️ 6) Habilitamos y arrancamos el servicio de Docker
 ```
    $ sudo systemctl enable docker
    $ sudo systemctl start docker
   ```
  ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yhabi.png)

  

# **-----------------------------ACTIVIDAD 2---------------------------------**

 # 1- Lleva a cabo la práctica descrita en el primer artículo
   ☑️ **1.1) parte 1:**   
   Ejecuta la imagen "hello-world"
   ```
     $ docker run hello-world
```
   ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zdoc.png)
   
   ☑️ **1.2) parte 2:**
   
   Muestra las imágenes Docker instaladas
   ```
     $ docker images
```
   ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yim.png)
   
   ☑️ **1.3) parte 3:**
   Muestra los contenedores Docker
     $ docker ps (este muestra solo los activos)
     $ docker ps -a (este muestra todos tanto los activos como los inactivos)
   ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ydocc.png)
   
   
# 2 Lleva a cabo la práctica descrita en el segundo artículo
✔️ **2.1) Edita el fichero Dockerfile**
   crear un directorio para el y acceder a el
       $ mkdir mi_app && cd mi_app
dentro de ese directorio crear un archivo sin extension con este contenido
    FROM node:lts-alpine
    WORKDIR /app
    COPY . .
    RUN npm install
    EXPOSE 3000
    CMD ["node", "src/index.js"]
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzpo.png)

✔️ **2.2) Construye el contenedor**
hay que crear dos archivos un package.json y un src
package.joson
*ejecutar npm init y seguir las preguntas que te hacen*
crear el directorio src
      $ mkdir src && touch src/index.js
y dentro del src poner un codigo de prueba
construimos la imagen
      $ docker build -t josepepe313/mi_app:1.0 .
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zyic.png)


✔️ **2.3) Ejecútalo**
    $ docker run -d -p 3000:3000 josepepe313/mi_app:1.0
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zzpssso.png)

✔️ **2.4) crearse una cuenta en docker hub**

✔️ **2.5) Publícalo**
    $ docker login
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/yyrrr.png)
Etiquetar la imagen
    $ docker tag mi_app:1.0 josepepe313/mi_app:1.0
Subir la imagen a Docker Hub:
    $ docker push josepepe313/mi_app:1.0


# **-----------------------------ACTIVIDAD 3---------------------------------**

▶️ **1) para descargar la imagen ubuntu como menciona el enunciado poner en la terminal**

    $ docker pull ubuntu y para las demas igual solo que sustitullendo el nombre de ubuntu
    
▶️ **2) para descargar la imagen de hello-world**
    $ docker pull hello-world
    
▶️ **3) para descargar la imagen nginx**
    $ docker pull nginx
![image](https://github.com/user-attachments/assets/e2001b31-6788-46bc-b0aa-3ca349bbe87f)

▶️ **4) para mostrar las imagenes descargadas usamos**
    $ docker images
![image](https://github.com/user-attachments/assets/009bc6e7-8b93-4b51-bf8a-974a711a3c83)

▶️ **5) para ejecutar un contenedor hello-world y dale nombre “myhello1”**
ponemos lo siguiente
    $ docker run --name myhello1 hello-world
    
▶️ **6) para ejecutar un contenedor hello-world y dale nombre “myhello2”**
    $ docker run --name myhello2 hello-world
    
▶️ **7) para ejecutar un contenedor hello-world y dale nombre “myhello3”**
    $ docker run --name myhello3 hello-world
![image](https://github.com/user-attachments/assets/b652db69-59ab-455a-a3e8-12b74000b08b)
![image](https://github.com/user-attachments/assets/86a2c58c-f7fc-4057-8126-850b7351e380)
![image](https://github.com/user-attachments/assets/c91cd17e-90ab-4796-93fe-f63287d438d7)

▶️ **8) para mostrar los contenedores que se estan ejecutando usamos**
    $ docker ps -a
![image](https://github.com/user-attachments/assets/a3736b71-073a-4565-9d48-e851628ff431)
he leido que suelen poner docker ps solo pero a mi me gusta usar docker ps -a para que me mustre todo al completo

▶️ **9) Para detener el contenedor myhello1**
    $ docker stop myhello1

▶️ **10) Para detener el contenedor myhello2**
    $ docker stop myhello2
![image](https://github.com/user-attachments/assets/caccd472-1884-46be-b8d8-674ccd880720)

▶️ **11) para borrar el contenedor myhello1**
    $ docker rm myhello1
![image](https://github.com/user-attachments/assets/e477f808-e5bb-4bae-98a3-7a4fc045ff83)

▶️ **12) volvemos a usar docker ps para mostar los contenedores en ejecucion**
![image](https://github.com/user-attachments/assets/513461ec-56a8-4ec8-8d9f-cfafc0443808)

▶️ **13) para eliminar todos los contenedores tanto los detenidos como los que no usamos**
    $ docker rm -f $(docker ps -aq)
no lo pongo en captura para que se vea que esta hecho porque si no puede tender a confusion que no lo he hecho (me ha pasado en varias ocasiones y prefiero no ejecutar lo de borrado para que no tienda a errores)


# **-----------------------------ACTIVIDAD 4---------------------------------**

# TRES EJEMPLOS DEL MODULO 3 DOCUMENTADOS Y CAPTURA DE PANTALLA

🥇 **ejemplo 1: Asociando almacenamiento a los contenedores: volúmenes Docker**
creamos un volumen
    $ docker volume create web
![image](https://github.com/user-attachments/assets/15933a43-d1be-44c3-addc-bfaa4e460884)
para continuar hay que tener instalado apache
creamos un contenedor con el volumen asociado, usando -v, y creamos un fichero index.html
    $ docker run -d --name my-apache-app -v web:/usr/local/apache2/htdocs -p 8080:80 httpd:2.4
![image](https://github.com/user-attachments/assets/4b5dfbf9-692d-48c8-8fea-6023547239f9)
le metemos informacion dentro
    $ docker exec my-apache-app bash -c 'echo "<h1>Hola</h1>" > /usr/local/apache2/htdocs/index.html'
![image](https://github.com/user-attachments/assets/3aa4a713-d88d-4e9a-86e8-ccd22f6011b6)
le hacemos un curl
![image](https://github.com/user-attachments/assets/d7978e51-8443-458b-93da-d8ea870d82d6)
lo borramos
![image](https://github.com/user-attachments/assets/12477743-2bca-4ec7-a2aa-c719002f3403)
cremos uno de nuevo y vemos como el contenido no se borra
![image](https://github.com/user-attachments/assets/68604cb3-a8c0-44c5-8bee-929bef731228)

🥈 **ejemplo 2 Despliegue de la aplicación Guestbook**
    $ docker network create guestbook
![image](https://github.com/user-attachments/assets/c1914da8-6b28-46c5-a866-c3de8f626862)
recordar que hace falta el uso de redis
para ejecutarlo
    $ docker run -d --name redis --network guestbook -v /opt/redis:/data redis redis-server --appendonly yes
![image](https://github.com/user-attachments/assets/7f167ecd-0a8b-4bcf-8cbe-e9026ff38039)
    $ docker run -d -p 80:5000 --name guestbook --network red_guestbook iesgn/guestbook
![image](https://github.com/user-attachments/assets/f56629e1-dc12-40f7-a377-242c44c67f9d)
he usado otro nombre y puerto porque me daba error porque ya existia
y como ves poniendo localhost y el puerto accedo a guestbook
![image](https://github.com/user-attachments/assets/df30e3f8-4357-4f4c-be2f-89c034fef894)

🥉 **ejemplo 3 Redes en Docker**
crear un contenedor interactivo con la imagen debian
    $ docker run -it --name con1 --rm debian bash
![image](https://github.com/user-attachments/assets/43e80fc7-4a29-4f4a-ac72-c595d339ea65)
obtenemos la ip asignada
    $ docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' con1
![image](https://github.com/user-attachments/assets/c074422b-b8c5-4b37-8898-1e76043e32a6)
luego conecto el contenedor a la red host
![image](https://github.com/user-attachments/assets/6a9b2eb2-0ab3-4d72-9306-25e21619e270)


# **-----------------------------ACTIVIDAD 5---------------------------------**

# TRES EJEMPLOS DEL MODULO 4 DOCUMENTADOS Y CAPTURA DE PANTALLA

🥇 **emjemplo 1: almacenamiento**
esto es como si fuese una caja donde yo guardo mis cosas, si yo rompo la caja mis cosas desaparecen, para evitarlo usamos volumenes que es como si guardamos los datos en un sitio y al cambiar la caja los datos quedan intactos es decir que no se borraran ni nada
se puede hacer de dos manera usando un volumen y bind mount
**usando volumen**
comenzamos con la actividad:
creamos un archivo nuevo usamos nano
    $ nano docker-compose.yml
y dentro pegamos lo siguiente
![image](https://github.com/user-attachments/assets/341714da-1319-413e-935f-357ab64279b4)
para iniciarlo lo iniciamos con esto de aqui
    $ docker compose up -d
![image](https://github.com/user-attachments/assets/fbe9c331-0abd-43fc-a434-8b61f17d43ce)
lo comprobamos 
como se muestra en el ejemplo con 
     $ docker volume ls
 ![image](https://github.com/user-attachments/assets/0e8fad27-d875-4373-8734-8d94fb060e1c)
 y aqui demuestro como se ha creado y se puede ver
 como opcional porque no viene en el ejemplo explicado 
 para acceder y ver los archivos que se pueden correr dentro de el usamos el comando siguiente
     $ sudo docker exec -it [nombre] bash
**usando bind mount**
hacemos lo mismo de antes
creamos el .yml
    $ sudo nano dockerr-compose.yml y escribimos dentro lo siguiente
![image](https://github.com/user-attachments/assets/21e37c3c-20dd-4d3e-ba58-d988af81c6a3)
pasos para la ejecucion
creamos una carpeta para ello y ponemos un texto
    $ mkdir miweb
    $ echo "<h1>hola</h1>">miweb/index.html
para ejecutar como antes
    $ docker compose up -d
y en el navegador solo hay que poner en la barra de busqueda de navegacion localhost y el puerto 
![image](https://github.com/user-attachments/assets/e45e259b-a570-479b-8b33-363e65d642fd)
y aqui se puede ver como esta corriendo

🥈 **ejemplo 2:**
**El comando docker compose**
desplegar letschat
arrancamos el contenedor
    $ docker compose up -d
![image](https://github.com/user-attachments/assets/05c63bac-1498-4fd4-be2b-7d67b35a1614)
y poner en la barra de busqueda localhost y el puerto

🥉 **ejemplo 3: Despliegue de la aplicación Temperaturas**
cremaos un .yml como en el ejemplo
![image](https://github.com/user-attachments/assets/c91792fc-9fea-4916-95ac-903663085429)
lo arrancamos como siempre
    $ docker compose up -d
![image](https://github.com/user-attachments/assets/af796576-d374-4fe0-84cb-f0b6d429e902)


# **-----------------------------ACTIVIDAD 6---------------------------------**

# TRES EJEMPLOS DEL MODULO 5 DOCUMENTADOS Y CAPTURA DE PANTALLA

🥇 **ejemplo1:**
*version:1*
descargamos los archivos del ejemplo
con git clone  https://github.com/josedom24/curso_docker_ies/tree/main/ejemplos/modulo5/ejemplo1/version1
![image](https://github.com/user-attachments/assets/26e87dc9-ebf3-419c-a8d8-0f9d4ea27971)
contruimos la imagen
![image](https://github.com/user-attachments/assets/ac2a63a3-b0b7-4195-bbe7-226252172332)
ejecutamos el nuevo contenedor
![image](https://github.com/user-attachments/assets/272c79f1-76a6-43d2-8a9d-a935dc558289)ç
y escuchando esta 
![image](https://github.com/user-attachments/assets/35b1676d-ecec-4788-a956-9b92d14ef658)
*version 2:*
dentro del index.html lo modificamos y creamos una web para que haya diferencia
y ponemos este fraggmento de codigo en el dockerfile
![image](https://github.com/user-attachments/assets/a0e37ce2-2300-4b71-95b2-d1353793394c)
construimos la imagen
![image](https://github.com/user-attachments/assets/e9b150d5-ef3d-40f2-bc3a-85fa3a1ad209)
ejecutamos esto para ejecutar
![image](https://github.com/user-attachments/assets/09ea9193-7193-42e8-b77c-51fd6990ead6)
y aqui demustro como funciona que se ve
![image](https://github.com/user-attachments/assets/0e95ce0c-63fd-4767-8ec6-380eaa7aa576)
*version 3:*
nos situamos en version dos y en index.html agregamos esto
![image](https://github.com/user-attachments/assets/ee4910d4-d6d0-44b7-9b5e-5dae63d354cf)
hacemos un nano dockerfile y agregamos esto
![image](https://github.com/user-attachments/assets/fb3f4849-9434-479b-a5d5-61b58c7fe476)
ejecutamos para construir la imagen
![image](https://github.com/user-attachments/assets/9f0e1f1d-b71c-43f2-94b8-82f3dccc9848)
ejecutamos para que se vea en la web
![image](https://github.com/user-attachments/assets/5fa375fa-e5f3-405a-807c-9ef30e4c1715)
aqui muestro como se ve 
![image](https://github.com/user-attachments/assets/2a011413-7f33-46a9-b956-6267cd36ed7b)

🥈 **ejemplo 2:**
*version 1:*
ya estamos en ejemplo2
![image](https://github.com/user-attachments/assets/7dc485e7-a2a8-4010-8dab-d8c73d26e05a)
modificamos el index.php de la carpeta app por esto que añado en la imagen cualquuier cosa que añada en un .html o .php o lo que sea da igual lo muestro para desmostrar que lo he modificado
![image](https://github.com/user-attachments/assets/15399478-0349-423e-b058-b797825eac5f)
ejecutamos esto para construir la imagen
![image](https://github.com/user-attachments/assets/b275b8fd-ee1b-4426-8d78-287f124a0d19)
voy asin 
![image](https://github.com/user-attachments/assets/c9ee64ba-7462-4c00-9540-39f7a3b06c4a)
![image](https://github.com/user-attachments/assets/7d70b95a-3dd2-492b-9785-49b31a3f7660)
luego poner localhost y el puerto en el navegador y se ve
![image](https://github.com/user-attachments/assets/703a271e-dc73-4b1b-8542-df4963fdb6f4)
*version 2:*
modificamos el dockerfile como siempre
![image](https://github.com/user-attachments/assets/66c1e39a-fa1c-4946-b815-4874c3288ca8)
creamos y ejecutamos
y vemos como funciona
![image](https://github.com/user-attachments/assets/a6e08326-4f83-4331-be19-76daaf460cb3)
es lo mismo pero como ya habiamos creado antes las cosas por eso es tan corto 

🥉 **ejemplo 3:**
*version 1:*
modificamos el Dockerfile como se especifica en el ejemplo
![image](https://github.com/user-attachments/assets/744c28c9-1ae0-4bde-af4b-ea415ef30f83)
por lo visto hay que esperar unos 30 minutos por el reloj de docker he estado leyendo y en dockerfile hay que cambiar esta linea que se muestra en la imagen
![image](https://github.com/user-attachments/assets/6b4d2aa3-b987-424c-a718-7415223f0b45)
se me creo al fin 
![image](https://github.com/user-attachments/assets/b665164d-827a-4a63-915c-d7b8ee9dadc3)
tuve que hacer un 
    $ sudo apt install ntpdate
    $ sudo ntpdate time.google.com
  para sincronizar la hora
construimos la imagen
![image](https://github.com/user-attachments/assets/97d88298-6c90-4309-93cd-51c14e22530f)
creamos el contenedor
![image](https://github.com/user-attachments/assets/d2b63ba2-b83a-4f0c-845c-a71a8b3abaf7)
aqui demuestro como esta funcionando
![image](https://github.com/user-attachments/assets/c38e2a2c-2ba5-4c17-94f9-d0abb55dcca3)
*version 2:*
en este caso no hace falta modificar el dockerfile
solo montamos la imagen
![image](https://github.com/user-attachments/assets/5c3a1769-6160-4b48-9df8-e877a9124e3a)
ejecutamos el contenedor
![image](https://github.com/user-attachments/assets/4ee09df6-ba58-46bd-9c6d-f8d098c75196)
aqui demuestro como se esta ejecutando correctamente
![image](https://github.com/user-attachments/assets/d2b940c5-617f-41fb-ba87-3d1d2457ecd1)
para subir la imagen a dockerhub como me piden 
  hago un docker push y nombre de la imagen y listo pero hay que iniciar sesion ante
![image](https://github.com/user-attachments/assets/6dfaa847-3676-4600-9b44-05667739a432)
esta es la url para descargar las imagenes
  https://hub.docker.com/u/josepepe313

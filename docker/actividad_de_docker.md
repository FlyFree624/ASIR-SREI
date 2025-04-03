
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

para descargar la imagen ubuntu como menciona el enunciado poner en la terminal

docker pull ubuntu y para las demas igual solo que sustitullendo el nombre de ubuntu

docker pull hello-world
docker pull nginx

![image](https://github.com/user-attachments/assets/e2001b31-6788-46bc-b0aa-3ca349bbe87f)

para mostrar las imagenes descargadas usamos

docker images

![image](https://github.com/user-attachments/assets/009bc6e7-8b93-4b51-bf8a-974a711a3c83)

para ejecutar un contenedor hello-world y dale nombre “myhello1”

ponemos lo siguiente

docker run --name myhello1 hello-world

y en los siguientes casos igual solo que cambiando **myhello1**

docker run --name myhello2 hello-world
docker run --name myhello3 hello-world

![image](https://github.com/user-attachments/assets/b652db69-59ab-455a-a3e8-12b74000b08b)

![image](https://github.com/user-attachments/assets/86a2c58c-f7fc-4057-8126-850b7351e380)

![image](https://github.com/user-attachments/assets/c91cd17e-90ab-4796-93fe-f63287d438d7)

para mostrar los contenedores que se estan ejecutando usamos 

docker ps -a

![image](https://github.com/user-attachments/assets/a3736b71-073a-4565-9d48-e851628ff431)

he leido que suelen poner docker ps solo pero a mi me gusta usar docker ps -a para que me mustre todo al completo

Para detener el contenedor myhello1 y mhello2

docker stop myhello1
docker stop myhello2

![image](https://github.com/user-attachments/assets/caccd472-1884-46be-b8d8-674ccd880720)

para borrar el contenedor myhello1

docker rm myhello1

![image](https://github.com/user-attachments/assets/e477f808-e5bb-4bae-98a3-7a4fc045ff83)







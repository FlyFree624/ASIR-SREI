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


**-----------------------------ACTIVIDAD 3-----------------------------------------------------**


**-----------------------------ACTIVIDAD 4-----------------------------------------------------**


**-----------------------------ACTIVIDAD 5-----------------------------------------------------**


**-----------------------------ACTIVIDAD 6-----------------------------------------------------**



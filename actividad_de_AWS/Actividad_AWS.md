
-------------------practica del aws final es esta  Instalación de WordPress con EC2, RDS y EFS  -------------------------------------------------------------------------------------------------------

**entrar al laboratorio**

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin1aws.png)

dar en crear vpc
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin2aws.png)

se empieza a crear el flujo

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin3aws.png)

**creacion maquinas ec2**

dar al mismo sitio que crear la vpc pero en vez de poner vpc ec2

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin4aws.png)

entrar y dar en lanzar instancia, una vez dentro elegimos el S.O

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin5aws.png)

asignamos el par de claves

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin6aws.png)

configuramos la vpc y la subred

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin7aws.png)

creamos las reglas 

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin8aws.png)

y dar en lanzar

procedemos a la instalacion

instalar la clave ppk

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin9aws.png)

copiar el dns publico de la instancia

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin10aws.png)

en putty debe de quedar asi

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin11aws.png)

y en browser ponemos la clave ppk que hemos descargado antes

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin12aws.png)

y aqui como accedemos a la instancia
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin13aws.png)

realizamos un update y un upgrade y a instalar apache y php

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin14aws.png)

he usado esto para instalar php
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin15aws.png)

**procedemos a crear la BD con RDS**

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin16aws.png)

le damos a crear
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin17aws.png)

le clickamos a mysql y escogemos la capa gratis

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin18aws.png)

establecemos una password

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fin19aws.png)

la password es: aceituna

elegimos esta opcion

![image](https://github.com/user-attachments/assets/bfd7818f-b8e6-45e3-a88b-062db7de9b5e)

y darle a crear

![image](https://github.com/user-attachments/assets/a9a8a71a-2c8c-457f-b9c0-8889d58c1f5b)

y ahora pulsamos en la bd y le damos aqui

![image](https://github.com/user-attachments/assets/fc901a7d-1152-4164-a1c8-f2e311ee16c6)

ponemos el nombre de nuestra instancia

![image](https://github.com/user-attachments/assets/4a7bbe35-e15d-42f9-9107-caad9c9d630f)

y dar en continuar

crear el sistema de archivo efs

![image](https://github.com/user-attachments/assets/a01d4d24-c772-4f7a-b470-3cb23f8c3814)


le damos a crear
![image](https://github.com/user-attachments/assets/09f0e3ec-9b5b-4cd4-a898-849f6b1add55)

![image](https://github.com/user-attachments/assets/c99e9031-e047-4664-8a09-5fdb0b023a5f) y dar a crear

procedemos a instalar wordpress y mysql

![image](https://github.com/user-attachments/assets/2cb25562-2bdf-4ecd-be11-7b7c513d9ec4)

![image](https://github.com/user-attachments/assets/c1b340ec-4bfb-48de-8cb7-5e83ead51335)

nos conectamos a la base de datos

![image](https://github.com/user-attachments/assets/1cad6fb3-e16b-46be-a823-9eee0c284451)

creamos una bd para wordpress

![image](https://github.com/user-attachments/assets/2510155c-aaa9-4b3b-a3ed-a361bd1c753e)

y ya solo queda poner nuestra ip publica en el navegador y carga wordpress

![image](https://github.com/user-attachments/assets/c310a8e3-84fc-42ec-a47a-6353379729a1)


![image](https://github.com/user-attachments/assets/29a5d7f5-d1a1-4d2c-a690-1970859e1cfe)















































 
 

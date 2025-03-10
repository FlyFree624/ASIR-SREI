Acceder a la instancia AWS
 Conéctate a tu instancia de AWS (Amazon Linux, Ubuntu o cualquier otra distribución compatible) 
usando SSH:
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/123aws.png)

 antes que nada actualizar
 sudo apt update 
y ahora procedemos con la instalacion de apache
 sudo apt install apache2 libapache2-mod-auth-mysql -y 
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/321aws.png)

Iniciamos y habilitamos Apache 
sudo systemctl start apache2 
sudo systemctl enable apache2

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/421aws.png)

Configurar Autenticación con MySQL  o MariaDB
 sudo apt install mariadb-server -y 
sudo apt install mysql-server -y

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/2235aws.png)

 Iniciar MySQL 
sudo systemctl start mariadb
 sudo systemctl enable mariadb
 creamos una base de datos y usuario para la utenticación
 CREATE DATABASE auth_db; 
CREATE USER 'auth_user'@'localhost' IDENTIFIED BY 'password_segura'; 
GRANT SELECT ON auth_db.* TO 'auth_user'@'localhost'; 
FLUSH PRIVILEGES;
 Configurar autenticación en Apache
 en /etc/httpd/conf/httpd.conf  agregamos esto
 <Directory "/var/www/html/privado"> 
AuthType Basic AuthName "Área Segura" 
AuthBasicProvider mysql 
AuthUserFile /etc/apache2/.htpasswd 
Require valid-user 
</Directory> 

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/432115aws.png)

Reiniciar Apache 
sudo systemctl restart apache2 
Crear un Certificado SSL Autofirmado 
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache
selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/3587aws.png)

Configurar SSL en Apache 
aquí: sudo nano /etc/apache2/sites-available/default-ssl.conf 
añadir esta directiva:
 <VirtualHost *:443> ServerAdmin tu@email.com DocumentRoot /var/www/html SSLEngine on 
SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt SSLCertificateKeyFile 
/etc/ssl/private/apache-selfsigned.key <Directory "/var/www/html"> AllowOverride All Require all 
granted </Directory> </VirtualHost> 

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/812aws.png)

habilitamos ssl
 sudo a2enmod ssl 
reiniciamos apache
 sudo systemctl restart apache2


 ---------- Instalación de WordPress con EC2, RDS y EFS-----------------
procedo a cpmenzar a hacer la activadad
 primero que nada escribo
 aws sts get-caller-identity para ver si tengo acceso aws-cli
 ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/1aws.png)
 nos muestra que tenemos acceso lo vemos porque nos muestra un id y Account ID

 Creamos una instancia EC2

 aws ec2 run-instances --image-id ami-0c02fb55956c7d316 --count 1 --instance-type t3.micro --key-name MyKeyPair --security-groups default --query 'Instances[0].InstanceId'

 pero primero hay que crear una clave ssh

 aws ec2 create-key-pair --key-name MiClaveAWS --query 'KeyMaterial' --output text > MiClaveAWS.pem

 y le asignamos los permisos

 chmod 400 MiClaveAWS.pem

 luego ya podemos hacer uso de este comando
 
aws ec2 run-instances --image-id ami-0c02fb55956c7d316 --count 1 --instance-type t3.micro --key-name MiClaveAWS --security-groups default --query 'Instances[0].InstanceId'

 "i-0bb45fd0cbb1d41d5"

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/2aws.png)

crear una bd con rds

aws rds create-db-instance --db-instance-identifier MiDBWordPress --db-instance-class db.t3.micro --engine mysql --master-username admin --master-user-password "Contrasena123" --allocated-storage 20 --no-publicly-accessible

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/3aws.png)

Conectar EC2 a RDS
aws rds describe-db-instances --db-instance-identifier MiDBWordPress --query "DBInstances[0].Endpoint.Address"
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/4aws.png)

ahora configuramos la base de datos

sudo nano /var/www/html/wp-config.php

donde pone define('DB_HOST', 'localhost'); cambiamos localhost por esto midbwordpress.cfmjptxu6lnr.us-east-1.rds.amazonaws.com

que asin

define('DB_HOST', 'midbwordpress.cfmjptxu6lnr.us-east-1.rds.amazonaws.com');

conectarse con ssh

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/5aws.png)

una vez ya todo procedemos a instalar el mysql php y el wordpress

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/6aws.png)

puse el fondo negro porque me estaba confundiendo 

he usado este comando para intalar wordpress

cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xvzf latest.tar.gz
sudo mv wordpress/* .
sudo chown -R apache:apache /var/www/html/*

editamos el archivo wp-config.php y reiniciamos apache como siempre
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/7aws.png)

con sudo systemctl restart httpd

y una vez intalado todo ponemos nuestra ip en el navegador y accedemos a wordpress

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/8aws.png)

-------------------practica del aws final es esta-------------------------------------------------------------------------------------------------------

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

la password es: Aceitunaconhueso

elegimos esta opcion
![image](https://github.com/user-attachments/assets/bfd7818f-b8e6-45e3-a88b-062db7de9b5e)














 
 

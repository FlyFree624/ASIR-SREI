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


 

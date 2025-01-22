**Práctica 1- Servidor alojamiento web**
primero actualizamos el sistema con
sudo apt-get update

procedemos a instalar apache y todo lo que nos pide

sudo apt install apache2 php libapache2-mod-php mariadb-server phpmyadmin vsftpd openssh-server postfix dovecot-imapd dovecot-pop3d certbot python3-certbot-apache -y

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/apaa.png)

ahora habilitamos php

sudo a2enmod php

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/apad.png)

sudo systemctl restart apache2

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/apdr.png)

ahora habilitamos los host virtuales

sudo nano /etc/apache2/sites-available/000-default.conf

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/hostq.png)

añadimos lo siguiente

<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    <Directory /var/www/html>
        AllowOverride All
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

![]()




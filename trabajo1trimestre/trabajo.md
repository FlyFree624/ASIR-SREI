![image](https://github.com/user-attachments/assets/b0d09e2c-0de4-471d-856e-38d1677fb064)**Instalación del servidor web apache. Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. 
El primero servirá el contenido mediante wordpress y el segundo una aplicación en python**

Instalar Apache:

sudo apt install apache2 -y
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/installap.png)

Iniciar el servicio de Apache:

sudo systemctl start apache2

detener Apache:

sudo systemctl stop apache2

Para reiniciar Apache:

sudo systemctl restart apache2

configuración de los dominios y la instalación de WordPress y la aplicación en Python:

sudo nano /etc/hosts y una vez dentro agrego lo siguiente

127.0.0.1 centro.intranet
127.0.0.1 departamentos.centro.intranet
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/hosts.png)

creo carpetas para guardar cada sitio:

sudo mkdir -p /var/www/centro.intranet
sudo mkdir -p /var/www/departamentos.centro.intranet

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/carpeta.png)

Instalar WordPress para centro.intranet

cd /tmp

wget https://wordpress.org/latest.tar.gz

tar -xzf latest.tar.gz

sudo mv wordpress/* /var/www/centro.intranet/

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/Captura%20de%20pantalla%202024-11-03%20160241.png)

asigno permisos a los directorios creados

sudo chown -R www-data:www-data /var/www/centro.intranet

sudo chmod -R 755 /var/www/centro.intranet

hay que instalar una base de datos escojo MARIADB ya que estoy usando kali y no admite mysql pero es totalmente compatible

sudo apt install mariadb-server --fix-missing

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/mariadb.png)

para iniciar el servicio de mariadb:

sudo systemctl start mariadb
sudo systemctl enable mariadb

accedemos a mariadb:

sudo mariadb -u root -p

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ma.png)

una vez dentro de mariadb creamos la base de datos para wordpress:

CREATE DATABASE wordpress;
CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;

Crear Archivos de Configuración de Apache:
(wordpress)

ejecutar en una bash esto sudo nano /etc/apache2/sites-available/centro.intranet.conf

y pegar esta directiva en el archivo 

<VirtualHost *:80>
    ServerName centro.intranet
    DocumentRoot /var/www/centro.intranet

    <Directory /var/www/centro.intranet>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/centro.intranet_error.log
    CustomLog ${APACHE_LOG_DIR}/centro.intranet_access.log combined
</VirtualHost>

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/dire.png)

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/wp.png)

(python)
en una bash pegar el siguiente codigo
sudo nano /etc/apache2/sites-available/departamentos.centro.intranet.conf
pegar esta directiva en el archivo creado
<VirtualHost *:80>
    ServerName departamentos.centro.intranet
    DocumentRoot /var/www/departamentos.centro.intranet

    WSGIScriptAlias / /var/www/departamentos.centro.intranet/app.wsgi
    <Directory /var/www/departamentos.centro.intranet>
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/departamentos.centro.intranet_error.log
    CustomLog ${APACHE_LOG_DIR}/departamentos.centro.intranet_access.log combined
</VirtualHost>

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/py.png)

habilitamos los dos:

sudo a2ensite centro.intranet.conf
sudo a2ensite departamentos.centro.intranet.conf

habilitamos modulos

sudo a2enmod rewrite
sudo a2enmod wsgi

reiniciamos apache

sudo systemctl restart apache2

ahora en el navegador poner 
http://centro.intranet para acceder a WordPress.

http://departamentos.centro.intranet para acceder a tu aplicación Python.

**activar wgsi**

instalar wsgi:

sudo apt install libapache2-mod-wsgi-py3

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/wsgi.png)

habilitarlo

sudo a2enmod wsgi

reiniciar apache:

sudo systemctl restart apache2

Instalar Flask:

sudo apt install python3-pip
pip3 install Flask

crear una carpeta para guardar la aplicaciones

sudo mkdir /var/www/mi_aplicacion

crear una aplicacion aqui
sudo nano /var/www/mi_aplicacion/app.py

dentro de app.py

from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "¡Hola, esta es mi primera aplicación en WSGI!"

if __name__ == '__main__':
    app.run()
    
crear un archivo wgsi para que Apache pueda manejar la aplicación

sudo nano /var/www/mi_aplicacion/app.wsgi

agrego esto dentro del wsgi

import sys
import logging

logging.basicConfig(stream=sys.stderr)
sys.path.insert(0, "/var/www/mi_aplicacion")

from app import app as application

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/win.png)

Configurar Apache para Servir la Aplicación

Crear un Archivo de Configuración para el VirtualHost:

sudo nano /etc/apache2/sites-available/mi_aplicacion.conf

y dentro poner la siguiente directiva

<VirtualHost *:80>
    ServerName mi_aplicacion.local  # Cambia esto si necesitas otro nombre
    DocumentRoot /var/www/mi_aplicacion

    WSGIScriptAlias / /var/www/mi_aplicacion/app.wsgi
    
    <Directory /var/www/mi_aplicacion>
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/mi_aplicacion_error.log
    CustomLog ${APACHE_LOG_DIR}/mi_aplicacion_access.log combined
</VirtualHost>

Habilito el sitio:
sudo a2ensite mi_aplicacion.conf

reinicio apache:

sudo systemctl restart apache2

editar el etc hosts y poner 

127.0.0.1 mi_aplicacion.local

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/bien.png)


**proteger el acceso a la aplicación python mediante autenticación**

instalar la herramienta htpasswd

sudo apt install apache2-utils
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/hta.png)
crear el archivo .htpasswd para almacenar nombres de usuarios
sudo htpasswd -c /etc/apache2/.htpasswd usuario


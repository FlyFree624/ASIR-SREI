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
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/usuario.png)
configuramos la autenticación del archivo apache

sudo nano /etc/apache2/sites-available/mi_aplicacion.conf

y agregar esta directiva
<Directory /var/www/mi_aplicacion>
    AuthType Basic
    AuthName "Restricted Access"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/cf.png)

reiniciar apache

sudo systemctl restart apache2
 y cuando pongamos en el navegador http://mi_aplicacion.local aparecera el nombre y password intriducido antes es usuario las dos

 **instalar awast**

 sudo apt install awstats

 creo las carpetas donde van aguardarse:
 sudo mkdir -p /etc/awstats/wwwroot/cgi-bin/
 

 copio el fichero de configuracion para el dominio mio

 sudo cp /etc/awstats/awstats.conf /etc/awstats/wwwroot/cgi-bin/awstats.mi_aplicacion.conf


 edito el fichero de configuracion:

 sudo nano /etc/awstats/wwwroot/cgi-bin/awstats.mi_aplicacion.conf
 
 al editar el fichero de configuración:
 tener en cuenta que hay que modificar estas opciones

**SiteDomain: el dominio de la aplicación.** es: mi_aplicacion.local/
**LogFile: la ruta al archivo de log que AWStats analizará** es: /var/log/apache2/access.log
**DirData: el directorio donde se guardarán los datos de AWStats** es: /var/lib/awstats

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/sitedomain.png)

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/logfiles.png)

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/dirdata.png)

para actualizar awast despues de los cambios:

sudo perl /usr/lib/cgi-bin/awstats.pl -config=mi_aplicacion -update

instalar php

 sudo apt install php libapache2-mod-php php-mysql php-xml php-mbstring php-curl php-zip php-gd
 
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/php.png)

activar el modulo poner estos comandos:
  sudo a2enmod php hay que ver la version que tienes en mi caso es la 8.2 entonces es sudo a2enmod php8.2

  no olvidar reiniciar apache: sudo systemctl restart apache2

  **escojo ngix**

  hay que instalarlo [se recuerda hacer un sudo apt update]

  uso el comando:
  sudo apt install nginx

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/servebgbix.png)

para configurar nginx para que escuche por el puerto 8080 hacemos lo siguiente

sudo nano /etc/nginx/sites-available/servidor2.centro.intranet

y agregamos este contenido:

server {
    listen 8080;
    server_name servidor2.centro.intranet;

    root /var/www/servidor2.centro.intranet;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php-fpm.sock;
    }
}
        
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/contenido.png)

una vez ya guardado ejecutar lo siguiente:

sudo ln -s /etc/nginx/sites-available/servidor2.centro.intranet /etc/nginx/sites-enabled/

creamos un directorio para el nuevo dominio

sudo mkdir -p /var/www/servidor2.centro.intranet

ahora configurar php para ngnix (instalar si no está instalado aunque en ejercicios anteriries pedian que se instalara)

sudo apt install php-fpm php-mysql -y (por las dudas y por hechar una mano aqui dejo lo dejo de nuevo)

listen = /run/php/php8.2-fpm.sock (esta opcion tiene que estar habilitada)

para llegar hay podemos acceder desde aqui: sudo nano /etc/php/8.2/fpm/pool.d/www.conf

despues de todo esto reiniciarlo:

sudo systemctl restart php8.2-fpm

añadir el servidor al /etc/hosts

a ese fichero se accede de esta manera:

sudo nano /etc/hosts

y agregarlo

127.0.0.1 servidor2.centro.intranet

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/agregarserv.png)

sudo apt install phpmyadmin -y (el -y es para que le de a yes de manera automatica hago referencia por si lo he puesto antes que creo recordar que lo he puesto varias veces)

crear un sitio para poder acceder facilmente a phpmyadmin:

sudo ln -s /usr/share/phpmyadmin /var/www/servidor2.centro.intranet/phpmyadmin

reiniciar nginx:

sudo systemctl restart nginx




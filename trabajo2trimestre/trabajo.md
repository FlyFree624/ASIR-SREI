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

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/virtual.png)

reiniciamos

sudo systemctl restart apache2

habilitamos los TLS

sudo certbot --apache

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/tls.png)

registrarse para obtener un dominio online

![]() esta actividad la dejo perndiente

configurar un ftp con TLS

sudo nano /etc/vsftpd.conf

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ftptls.png)

lo ajustamos para que ponga esto

ssl_enable=YES
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
force_local_data_ssl=YES
force_local_logins_ssl=YES

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/confftp.png)

reiniciamos el servicio ftp

sudo systemctl restart vsftpd

configuramos ssh y ftp

permitir solo sftp

editamos el /etc/ssh/sshd_config y añadimos lo siguiente

Subsystem sftp internal-sftp
Match Group sftp
    ChrootDirectory %h
    ForceCommand internal-sftp
    AllowTcpForwarding no
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/winss.png)

y reiniciamos

sudo systemctl restart ssh

Configurar Postfix y Dovecot

configuramos Dovecot

sudo nano /etc/dovecot/dovecot.conf

y ponemos

protocols = imap pop3
ssl = required
ssl_cert = </etc/ssl/certs/ssl-cert-snakeoil.pem
ssl_key = </etc/ssl/private/ssl-cert-snakeoil.key

creacion de script

para la creacion de usuarios y directorios

Creación de usuarios y directorios

#!/bin/bash
read -p "Nombre de usuario: " username
read -p "Dominio: " domain
sudo useradd -m -s /bin/bash $username
sudo passwd $username
sudo mkdir -p /var/www/$domain
sudo chown $username:$username /var/www/$domain
sudo chmod 755 /var/www/$domain
cat <<EOF | sudo tee /etc/apache2/sites-available/$domain.conf
<VirtualHost *:80>
    ServerName $domain
    DocumentRoot /var/www/$domain
    <Directory /var/www/$domain>
        AllowOverride All
    </Directory>
</VirtualHost>
EOF

sudo a2ensite $domain
sudo systemctl reload apache2

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/usuydire.png)

creacion de base de datos y usuario

#!/bin/bash
read -p "Nombre de usuario SQL: " db_user
read -sp "Contraseña: " db_pass
read -p "Nombre de la base de datos: " db_name

mysql -u root <<EOF
CREATE DATABASE $db_name;
CREATE USER '$db_user'@'localhost' IDENTIFIED BY '$db_pass';
GRANT ALL PRIVILEGES ON $db_name.* TO '$db_user'@'localhost';
FLUSH PRIVILEGES;
EOF

echo "Base de datos y usuario creados."

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/bdyusu.png)

para habilitar servidorweb

instalar mod_wsgi

sudo apt install libapache2-mod-wsgi-py3

creamos un archivo de configuracion para apache

sudo nano /etc/apache2/sites-available/example.com.conf

y agregamos esta directiva para wsgi

<VirtualHost *:80>
    ServerName example.com
    DocumentRoot /var/www/example.com

    # Configuración para WSGI
    WSGIScriptAlias / /var/www/app.wsgi

    # Permitir acceso al directorio de la aplicación
    <Directory /var/www/>
        Require all granted
    </Directory>

</VirtualHost>

habilito el archivo de configuracion

sudo a2ensite example.com.conf

reinicio apache

sudo systemctl restart apache2

para la crAutomatización con Scripts
para crear usuarios y su hosting ponemos esye script

#!/bin/bash
# crear_usuario.sh usuario

if [ $# -eq 0 ]; then
    echo "Error! Debes introducir un nombre de usuario."
    exit 1
fi

USER=$1
DOCUMENT_ROOT="/var/www/html/$USER"
USER_HOME="/home/$USER"

# Crear usuario en el sistema
sudo useradd -m -d $USER_HOME -s /bin/bash $USER
echo "$USER:password123" | sudo chpasswd  # Cambia esto por una contraseña segura

# Crear directorio web del usuario
sudo mkdir -p $DOCUMENT_ROOT
sudo chown -R $USER:$USER $DOCUMENT_ROOT
sudo chmod -R 755 $DOCUMENT_ROOT

# Crear página por defecto
echo "<h1>Bienvenido $USER</h1>" > $DOCUMENT_ROOT/index.html

echo "Usuario $USER creado con éxito y configurado en Apache."

**configurar subdominios en BIND9:**

#!/bin/bash
# crear_subdominio.sh usuario ip

if [ $# -le 1 ]; then
    echo "Error! Debes introducir un usuario y una IP."
    exit 1
fi

USER=$1
IP=$2
SUB_DOMAIN="${USER}.ejemplo.com"
ZONE_FILE="/etc/bind/db.ejemplo.com"

echo "Creando subdominio $SUB_DOMAIN en DNS..."
echo "$SUB_DOMAIN. IN A $IP" | sudo tee -a $ZONE_FILE

**Script para Crear Usuarios y Webs**
#!/bin/bash
# Script para crear usuarios y su web

if [ $# -lt 1 ]; then
    echo "Uso: $0 nombre_usuario"
    exit 1
fi

USER=$1
DOCUMENT_ROOT="/var/www/html/$USER"

# Crear usuario en Linux
sudo useradd -m -d /home/$USER -s /bin/bash $USER
echo "$USER:1234" | sudo chpasswd  

# Crear directorio web
sudo mkdir -p $DOCUMENT_ROOT
sudo chown -R $USER:$USER $DOCUMENT_ROOT
echo "<h1>Bienvenido $USER</h1>" > $DOCUMENT_ROOT/index.html

echo "Usuario y página web creados correctamente."

**Configurar Apache para Ejecutar Python**

 Abre este archivo en tu servidor:
 
nano /etc/apache2/sites-available/000-default.conf

y añadir esto:

ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
<Directory "/usr/lib/cgi-bin">
    AllowOverride None
    Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
    Require all granted
</Directory>


![]()

# Reiniciar servicio DNS
sudo systemctl restart bind9
echo "Subdominio $SUB_DOMAIN configurado con éxito."

Habilitar Aplicaciones Python en el Servidor Web Edita el archivo de configuración de Apache (/etc/apache2/sites-available/000-default.conf) y poner esto

<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html

    # Permitir ejecución de Python
    ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
    <Directory "/usr/lib/cgi-bin">
        AllowOverride None
        Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>





**actividad 2**

(proceder a la instalación de un servidor en docker)

- primero actualizamos usando

sudo apt update && sudo apt upgrade -y

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/doc.png)

- instalo los paquetes necesarios

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/adoc.png)

- agrego la clave gpg de docker
  pongo el comando aqui por si en la imagen no se precia bien
  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo tee /usr/share/keyrings/docker-archive-keyring.gpg
  ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/gpg.png)
  
- agrego el repositorio de docker
  pongo el comando por si en la imagen no se aprecia bien

  echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian bookworm stable" | sudo tee /etc/apt/sources.list.d/docker.list

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/aof.png)

- instalo docker
  sudo apt install -y docker-ce docker-ce-cli containerd.io
  
  ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/instalardocker.png)

  [nota importante si aparece algun error al instalar haz un update]

  - habilitamos y ejecutamos docker

    sudo systemctl enable docker
    sudo systemctl start docker

    ponemos esto en la shell

    vemos si esta corriendo escribiendo en la shell este comando de aqui

    sudo systemctl status docker

    ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/dockercorriendo.png)

    y aqui comprobamos que esta corriendo perfectamente

    
- procedo a realizar la actividad de el desarrollo de las prácticas especificadas en el tema de “Introducción a Docker”

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/actividad.png)

- creo una red docker
  
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/reddocker.png)

 [Creo un servidor DNS con bind9]
 
  creamos un .sh con nano con este contenido

  docker run -d --name dns_server \
  --network mi_red \
  -p 53:53/udp \
  -p 53:53/tcp \
  ubuntu/bind9

  (al archivo lo llamo mi_red)

[Creo un servidor web]

creamos un .sh con nano con este contenido

docker run -d --name web_server \
  --network mi_red \
  -p 8080:80 \
  nginx

(al archivo lo llamo mi_redd)

- que la configuración del DNS y el servidor web se guarde creamos un .sh con nano con este contenido

  docker run -d --name dns_server \
  --network mi_red \
  -p 53:53/udp \
  -p 53:53/tcp \
  -v $(pwd)/dns_config:/etc/bind \
  ubuntu/bind9

  al archivo lo llamos dns_config.sh

  - para nginx crer un fichero con nano con este contenido
    
    docker run -d --name web_server \
  --network mi_red \
  -p 8080:80 \
  -v $(pwd)/html:/usr/share/nginx/html \
  nginx

al fichero lo llamo html.sh

- creo un docker compose para automatizar

  version: "3"
services:
  dns:
    image: ubuntu/bind9
    container_name: dns_server
    networks:
      - mi_red
    ports:
      - "53:53/udp"
      - "53:53/tcp"
    volumes:
      - ./dns_config:/etc/bind

  web:
    image: nginx
    container_name: web_server
    networks:
      - mi_red
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html

networks:
  mi_red:
    driver: bridge

fichero llamado docker-compose.yml

para ejecutarlo usamos el comando docker-compose up -d

demostramos que tanto el servidor web como el dns estan funcionando

escribimos

http://localhost:8080 en la barra de busqueda

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/serngx.png)

probamos la ejecucion de los servideres DNS

docker exec -it mi_nginx nslookup google.com dns_server o su ip

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/dnsserver.png)







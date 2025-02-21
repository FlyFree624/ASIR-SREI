----------------actividad4--------------------

**Obtén la dirección IP de los siguientes dominios: www.uhu.es, www.us.es, es.wikipedia.org**

poner en la shell dig y el nombre del dominio

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/dig.png)
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/digus.png)
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/digwiki.png)

**Obtén la dirección y los servidor DNS que corresponden a los siguientes dominios:  net, com, us.es, wikipedia.org**

para obtener la direccion que nos pide hacer en la shell esto:

dig net NS +noall +answer

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/digns.png)

y con todos se hace lo mismo

**Averigua los registros MX de los siguientes dominios:  uhu.es, us.es, wikipedia.org**

poner en la shell

dig uhu.es MX +noall +answer

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/gimx.png)

y con todos se hace lo mismo


**Obten la dirección IPV6 de www.isc.org**

poner en la shell

dig www.isc.org AAAA

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ipv6dig.png)

**Muestra los servidores de correo de yahoo.com**

poner en la shell
dig yahoo.com MX +noall +answer

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/mxd.png)

**Muestra la información asociada con la dirección 75.126.153.206**

escribir en la shell

dig -x 75.126.153.206

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/digshell.png)

**Muestra la dirección de www.google.es utilizando uno de los servidores DNS de google.com**

dig @ns1.google.com www.google.com

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/siete.png)

**Muestra información sobre el TTL de drive.google.com. Ejecútalo en varias ocasiones y comprueba cómo cambia el valor**

dig +nocmd drive.google.com +noall +answer

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/tll.png)

**Muestra los registro type NS de redhat.com**

dig -t NS redhat.com +noall +answer

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/t8.png)

**Muestra todos los registros de google.com**

dig google.com ANY +noall +answer

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/t2.png)


**Crea un fichero de texto que contenga los dominios;**
nano names.txt
ubuntu.com
redhat.com

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/t4.png)

**Haz una consulta con dig empleando el fichero anterior**

dig -f names.txt +noall +answer

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/t9.png)

----------------actividad5--------------------

**Instala y configura bin9 en primer lugar como servidor caché y por último como forwarding. 
En ambos casos debes:
Comprueba la sintaxis del archivo de configuración (named-checkconf)
Visualiza el archivo log y comprueba que responde adecuadamente (/var/log/syslog)**

actualizamos con sudo ap update

y ponemos esto en la shell para instalar: sudo apt-get install bind9 bind9utils bind9-doc

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/dns.png)

**probar la configuracion**

en la shell escribir sudo named-checkconf

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/tconfdns.png)

si hay errores no muestra errores como es el caso, si hubiese errores te mostraria una advertencia

reiniciamos

sudo systemctl restart bind9

ver los log:

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/dnslog.png)

----------------actividad 6--------------------

zona directa

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/directa.png)

zona inversa

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/inversa.png)

configuramos el /etc/bind/named.conf.local con las zonas configuradas

reiniciamos con 

sudo systemctl restart bind9

y ya solo queda hacer la consulta con dig

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/soa.png)

----------------actividad 8--------------------

Ararancamos el servidor ssh
ssh systemctl start sshd

para que root no haga login en sshd_config hay que activar la opcion permit root loguin

y para que escuche por el puerto 2222 en el mismo sitio cambiar la configuracion a el puerto 2222

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/rooot.png)

la actividad que dice que quitemos la fecha y hora es en el mismo lado solo que hay que modificar esta opcion

PrintLastLog no

inportante si esta comentada # hay que quitar el #

ahora reiniciamos con 

sudo systemctl restart ssh para que se aplique

y procedemos a probarlo

desde la maquina cliente hacer

ssh usuario@la ip de la maquina -p el puerto asignado
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/sshcli.png)


![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/demostrar.png)

aqui demuestro como me he conectado he pulsado un exit para que se vea que estoy conectado en y salgo y que la sesion se ha cerrado y vuelvo a mi usuario

----------------actividad 8 subdominio--------------------

# actividad 1 

crear un script que cree subdominios

#!/bin/bash

echo "Ingrese el nombre del subdominio:"
read dominio

echo "Ingrese la dirección IP:"
read ip

if [[ $EUID -ne 0 ]]; then
  exit 1
fi

echo "$ip $dominio" >> /etc/hosts

# actividad 2

#!/bin/bash

echo "Ingrese el nombre del subdominio:"
read dominio

echo "Ingrese la dirección IP:"
read ip

if [[ $EUID -ne 0 ]]; then
  exit 1
fi
INCLUDE="subdominio.txt"

cat $INCLUDE
echo "$ip $dominio" >> /etc/hosts

"suponiendo que en la descripcion es subdominio.txt"

# actividad 3

hacer lo mismo pero en python

este es el script

import subprocess
import os

dominio = input("Ingrese el subdominio: ")
ip = input("Ingrese la dirección IP: ")

if os.geteuid() != 0:
    exit(1)
subprocess.popen(['cat', 'subdominio.txt']).communicate()
subprocess.popen(['sh', '-c', f'echo "{ip} {dominio}" >> /etc/hosts'])

----------------actividad de Instalación de Wordpress en instancia Debian(o Ubuntu) EC2 con soporte de base de datos RDS y EFS--------------------

voy a utilizar vitual box por razones me es complicado usar aws y para hacer la actividad he decido proceder a hacerla en virtual box

creamos una nueva maquina y palicamos dos configuraciones de red

una tipo nat y la otra tipo red interna

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/nat.png)
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/interna.png)

iniciamos la maquina 
y hacenis un update

sudo apt update

mi usuario y clave es kali

instalamos apache

sudo apt install apache2 -y

habilitamos el servicio

sudo systemctl enable apache2
sudo systemctl start apache2

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/wor.png)

En el navegador: http://<IP> para ver que esta corriendo
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/woor.png)

y aqui esta la prueba de que lo está

Instalar NFS

sudo apt install nfs-common -y

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/wnfs.png)

y este otro tambien 

sudo apt install nfs-kernel-server -y


cremos un directorio de montaje

sudo mkdir /mnt/efs

Montamos almacenamiento compartido

sudo mount -t nfs 10.0.2.15:/mnt/efs /mnt/efs

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/www.png)

si da un error como este

sudo mount -t nfs 10.0.2.15:/mnt/efs /mnt/efs
mount.nfs: access denied by server while mounting 10.0.2.15:/mnt/efs

seguramente sea por la línea de configuración

poner esto para solucionarlo

sudo nano /etc/exports

/mnt/efs 10.0.2.0/24(rw,sync,no_subtree_check,no_root_squash)

sudo exportfs -ra para aplicar cambios


Configuración de Base de Datos RDS


instalamos mysql server

sudo apt install mysql-server -y

configuramos el usuario de la base de datos

sudo mysql
CREATE DATABASE wordpress;
CREATE USER 'wordpressuser'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'%';
FLUSH PRIVILEGES;
EXIT;
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/wdb.png)

Instalar WordPress

cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xvzf latest.tar.gz
sudo chown -R www-data:www-data wordpress

Configurar acceso a la base de datos en el archivo wp-config.php

sudo cp /var/www/html/wordpress/wp-config-sample.php /var/www/html/wordpress/wp-config.php
sudo nano /var/www/html/wordpress/wp-config.php

DB_NAME: wordpress

DB_USER: wordpressuser

DB_PASSWORD: password

DB_HOST:(IP del servidor de base de datos)10.0.2.15

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/zinc.png)

**para acceder a wordpres en el navegador escribimos http://<IP>/wordpress**


por si da fallo

Configurar MySQL para acceso remoto
editamos el archivo de configuración y permitir conexiones remotas

sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

Cambiar bind-address de 127.0.0.1 a 0.0.0.0

Reiniciar el servicio:

sudo systemctl restart mysql

Permitir tráfico en el puerto 3306

Agregar regla al firewall:

sudo iptables -A INPUT -p tcp --dport 3306 -s 10.0.2.0/24 -j ACCEPT

Asignar permisos al directorio de WordPress

sudo chown -R www-data:www-data /var/www/html/wordpress
sudo chmod -R 755 /var/www/html/wordpress






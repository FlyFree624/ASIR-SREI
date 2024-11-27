--------------------------------------------------------------ACTIVIDAD 3--------------------------------------------------------------

**Directivas de identificación**
la se utilizan para configurar cómo se identifica y maneja el servidor en las respuestas HTTP
ServerName: Especifica el nombre del servidor web aplica en el archivo de configuración principal o en configuraciones de un host virtual
ejemplo:
                  ServerName www.ejemplo.com
                  ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/diris.png)
                  
ServerAdmin: Define el correo electrónico del administrador, mostrado en páginas de error.
ejemplo:           ServerAdmin admin@ejemplo.com
                    ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/dirad.png)
                  
ServerTokens: cuánta información del servidor se muestra en las cabeceras HTTP se configura en el httpd.conf
ejemplo:            ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/conf_todas.png)
                    esto vale para todas (configurarlo en httpd.conf, ami me resulta mas facil que en un VirtualHost pero tambien es valido)

**Directivas de localización de ficheros**

DocumentRoot: Especifica la ubicación de los archivos que se servirán.
ejemplo: DocumentRoot "/var/www/html"  **mirar foto de arriba**

ErrorLog:	Define el archivo donde se registran los errores del servidor.
Ejemplo: ErrorLog "/var/log/apache2/error.log" **mirar foto de arriba**
CustomLog:	Establece un archivo personalizado para registrar accesos.
Ejemplo:CustomLog "/var/log/apache2/access.log" combined **mirar foto de arriba**
ServerRoot: Indica el directorio base del servidor.
Ejemplo: ServerRoot "/etc/httpd" **mirar foto de arriba**

**Directivas de control de la conexión**

Timeout: Configura el tiempo de espera antes de cerrar una conexión inactiva.
Ejemplo: Timeout 300 **mirar foto de arriba**
KeepAlive: Activa/desactiva conexiones persistentes
Ejemplo: KeepAlive On **mirar foto de arriba**
MaxKeepAliveRequests: Limita el número de solicitudes por conexión persistente.
Ejemplo:MaxKeepAliveRequests 100 **mirar foto de arriba**
KeepAliveTimeout: Define el tiempo de espera entre solicitudes en una conexión persistente.
Ejemplo: KeepAliveTimeout 5: **mirar foto de arriba**
**Foto para no olvidar es importante te puede servir de gran ayuda**
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/conf_todas.png)

--------------------------------------------------------------ACTIVIDAD 4--------------------------------------------------------------

**<IfModule>**
esta directiva se utiliza para incluir configuraciones en el archivo de configuración de Apache solo si un módulo específico está cargado
	
ejemplo: ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ifm.png)

Si el módulo mod_rewrite está habilitado, entonces se activa la reescritura de URL.

**LoadModule**
esta directiva se usa para cargar módulos adicionales en Apache, permitiendo la habilitación como la reescritura de URL

"son configuraciones claves en el archivo httpd.conf"

ejemplo:

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/lm.png)
	
**Include**
permite incluir otros archivos de configuración dentro del archivo principal de configuración de Apache, es útil para organizar la configuración en archivos más pequeños y manejables, especialmente en entornos con múltiples sitios o configuraciones.

"son configuraciones claves en el archivo httpd.conf"

ejemplo: 

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/include.png)
	
**<Directory>**
Especifica configuraciones específicas para un directorio en particular
ejemplo:
	
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ddi.png)

Esta configuración permite que los archivos .htaccess en /var/www/html puedan anular la configuración del servidor.

**<Files>**
Se usa para aplicar configuraciones específicas a ciertos archivos, basados en su nombre
ejemplo: 

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/fih.png)

Esta configuración niega el acceso al archivo config.php desde cualquier lugar.
	
**<Location>**
	
actúa sobre las rutas de URL

ejemplo: 

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/loca.png) 

Este bloque restringe el acceso a cualquier URL que comience con /admin solo al usuario admin

**<VirtualHost>**

Permite configurar múltiples (virtual hosts) en un mismo servidor Apache, cada uno con su propia configuración

ejemplo: 

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/virh.png)

Esto configura dos sitios diferentes, uno para site1.com y otro para site2.com, ambos en el puerto 80.
	
**¿Qué son los ficheros .htaccess?**
Son archivos de configuración utilizados para modificar la configuración de Apache a nivel de directorio sin necesidad de editar el archivo principal httpd.conf, es muy util para configuraciones específicas de directorios, como reglas de reescritura de URL, restricciones de acceso...etc.








--------------------------------------------------------------ACTIVIDAD 5--------------------------------------------------------------

Ejercicios:

**1 Crea un directorio llamado "dir1" y otro llamado "dir2"**

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/dir1.png)

**2 Explica qué diferencia existe entre ambos.:**

**<Order Deny,Allow** # esto significa que Deny se aplican primero, seguidas de la regla Allow
**Deny from All** # Deny from All: Se deniega el acceso
**Allow from 192.168.1.100** # Se permite el acceso únicamente a la ....
**</Directory>**

Permite el acceso solo a 192.168.1.100 y bloquea a todas las demás IP

**<Directory /var/www/example1>** # esto quiere decir que se aplican las reglas dentro de un directorio
**Order Allow,Deny** # aqui dice que las reglas de Allow se aplican primero y depues reglas de Deny
**Deny from All** eniega el acceso
**Allow from 192.168.1.100** permite el acceso exclusivamente a la ...
**</Directory>**

esta Afecta únicamente al directorio /var/www/example1

# nota importante mirar lo de Order Deny,Allow y esas cosas porque hay te dicen el orden en que se aplican las directivas

**3 Para dir1**
**Permite el acceso de las peticiones provenientes de 10.3.0.100**

he movido el dir1 y el dir2 aqui /var/www/html para hacerlo desde hay ya que la directiva anterior me ha llamado la atención y he decido paracticar con esa ruta

# esto es para acceder al archivo de configuración
# /etc/apache2/sites-available/000-default.conf para configuraciones específicas de sitios.
# /etc/apache2/apache2.conf para configuraciones globales.
# /etc/apache2/httpd.conf solo si decides incluir configuraciones adicionales.

hago un sudo nano /etc/apache2/sites-available/000-default.conf para acceder al archivo de configuracion

esta directiva:
<Directory /var/www/html/dir1>
    Order Deny,Allow         
    Deny from All                                                 
    Allow from 10.3.0.100                                      
</Directory>

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/direcdir.png)

me aseguro de aplicar los cambios con este comando:

sudo a2ensite 000-default.conf

# reinicio apache:

# sudo systemctl restart apache2


**Permite el acceso desde "marisma.intranet" en dir1**

escribo esta ruta en mi shell:

sudo nano /etc/apache2/sites-available/000-default.conf

añado esta directiva

<Directory /var/www/html/dir1>
    # Permitir acceso solo desde marisma.intranet
    Require host marisma.intranet
</Directory>

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/pri.png)

en ip a veo la ip de mi servidor

en /etc/hosts añado mi ip y marisma.intranet

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ma.png)

resultado:
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/err.png)
me sale eso porque tengo la otra activa, la dejo porque la actividad lo pide y si la quito esta mal

**Permite el acceso desde cualquier subdominio de "marisma.intranet"**

sudo nano /etc/apache2/sites-available/000-default.conf  aqui como antes la unica diferencia es que hay que añador un .

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/mintra.png)

# no olvidar reiniciar apache

# sudo systemctl restart apache2
y en el /etc/hosts/ añadir la ip y sub.marisma.intranet luego pones eso en el navegador y listo

**Permite el acceso de las peticiones provenientes de "10.3.0.100" con máscara "255.255.0.0"**

en sudo nano /etc/apache2/sites-available/000-default.conf poner la directiva

<Directory /var/www/html/dir1>
    Require all denied
    Require ip 10.3.0.0/16
</Directory>

reiniciar apache:
sudo systemctl restart apache2

**4 Modifica la configuración de forma que el acceso a dir1:
Se permita a "marisma.intranet" y no se permita desde 10.3.0.101"**

en sudo nano /etc/apache2/sites-available/000-default.conf poner la directiva

<Directory /var/www/html/dir1>
    Require all denied
    Require host marisma.intranet
    Require not ip 10.3.0.101
</Directory>

reiniciar apache:
sudo systemctl restart apache2

**5 Modifica la configuración de forma que el acceso a dir2:
Se permita a "10.3.0.100/8" y no a "marisma.intranet"**

en sudo nano /etc/apache2/sites-available/000-default.conf poner la directiva

<Directory /var/www/html/dir2>
    Require all denied
    Require ip 10.0.0.0/8
    Require not host marisma.intranet
</Directory>

reiniciar apache:
sudo systemctl restart apache2

--------------------------------------------------------------ACTIVIDAD 6--------------------------------------------------------------
Escribe las expresiones regulares para los siguientes supuestos:

**Directorios en /www/ cuyo nombre consista en tres dígitos.**

^/www/\d{3}$

Ficheros: *.gif, *.jpeg, *.jpg, *.png d
**.+\.(gif | jpe?g | png )**

.+\.(gif|jpe?g|png)$

**Escribe una directiva para redireccionar todos los GIF a ficheros JPEG en otro servidor**
RedirectMatch "(.*)\.gif$" "$1.jpg"

"(.*)\.gif$" "$1.jpg"

**Números enteros y decimales**
^[+-]?\d+(\.\d+)?$

**Números de teléfono en el formato Americano: 123-123-1234**
^\d{3}-\d{3}-\d{4}$

**Palabras**

^[a-zA-Z]+$

**Códigos hexadecimales de color de 24 o 32 bits**

^#([0-9a-fA-F]{6}|[0-9a-fA-F]{8})$

**Palabras de 4 letras**

^[a-zA-Z]{4}$

**Número entero sin signo**

^\d+$

**Número entero con signo**

^[+-]?\d+$

**Números reales**

^[+-]?\d*\.\d+$

**Número reales con exponente**

^[+-]?\d*\.?\d+([eE][+-]?\d+)?$

**Email**

^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$

**Números del 0 a 255**

^([1-9]?[0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])$

--------------------------------------------------------------ACTIVIDAD 7--------------------------------------------------------------
**reescribir la URL y que usemos en vez de php html**

 http://localhost/operacion.html?op=suma&op1=6&op2=8
 
Options FollowSymLinks
RewriteEngine On
RewriteRule ^operacion\.html$ operacion.php

**usar la extensión do en vez de html**

en .htacces escribir

Options FollowSymLinks
RewriteEngine On
RewriteRule ^(.+)\.do$ $1.html [nc]

**Crear URL amigables**

Crea un .htaccess con lo siguiente:

Options FollowSymLinks
RewriteEngine On
RewriteBase /
RewriteRule ^([a-z]+)/([0-9]+)/([0-9]+)$ operacion.php?op=$1&op1=$2&op2=$3

**Acortar URL**

 escribimos en nuestro .htaccess un RewriteRule de la siguiente forma:

RewriteRule ^buscar busqueda/buscar.php


**Uso del RewriteCond**

%{HTTP\_USER\_AGENT}: Información del cliente que accede

%{QUERY_STRING}: Guarda la cadena de parámetros de una URL dinámica.

%{REMOTE_ADDR}: Dirección de destino

%{HTTP_REFERER}: Guarda la URL que accede a nuestra página y %{REQUEST_URI} guarda la URI, URL sin nombre de dominio. Podemos evitar el Hot_Linking, o uso de recursos de tu servidor desde otra web. Por ejemplo, un caso muy común es usar imágenes alojadas en tu servidor puestas en otras web.



--------------------------------------------------------------ACTIVIDAD 8--------------------------------------------------------------

**CONFIGURAR UN Virtual host**

instalar apache si no esta instalado bueno ya lo hicimos antes

crear un directorio para un sitio web (el tuyo)

sudo mkdir -p /var/www/mi_sitio

Crear un Archivo de Configuración para el Virtual Host

los ficheros de configuración de apache se encuentran aqui
/etc/apache2/sites-available/


sudo nano /etc/apache2/sites-available/mi_sitio.local.conf

creamos un archivo de configuracion

sudo nano /etc/apache2/sites-available/mi_sitio.local.conf

y agregamos esto

<VirtualHost *:80>
    ServerAdmin webmaster@mi_sitio.local
    DocumentRoot /var/www/mi_sitio
    ServerName mi_sitio.local
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    <Directory /var/www/mi_sitio>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>

despues procedemos a habilitarlo

sudo a2ensite mi_sitio.local.conf

abrimos el /etc/hosts y añadimos la siguiente ip y el dominio ese

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/Captura%20de%20pantalla%202024-11-18%20180333.png)

reiniciamos apache

sudo systemctl restart apache2

comprobar:

escribir en el navegador http://mi_sitio.local

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/localmis.png)

--------------------------------------------------------------ACTIVIDAD 9--------------------------------------------------------------

**Crea cinco usuarios: usuario1, usuario2, usuario3, usuario4, usuario5.**
sudo htpasswd -c /etc/apache2/.htpasswd usuario1

el **-c** crea el archivo, si ya existe, no lo uses para agregar más usuarios (solo la primera vez).

Te pedirá que ingreses y confirmes la contraseña para ese usuario.

**Crea dos grupos de usuarios, el primero formado por usuario1 y usuario2; y el segundo por el resto de usuarios.**
sudo groupadd grupo1 el primer grupo

sudo usermod -aG grupo1 usuario1
sudo usermod -aG grupo1 usuario2

sudo groupadd grupo2 el segundo grupo

sudo usermod -aG grupo2 usuario3
sudo usermod -aG grupo2 usuario4
sudo usermod -aG grupo2 usuario5

**Crea un directorio llamado privado1 que permita el acceso a todos los usuarios.**

sudo mkdir /var/www/html/privado1 (crear directorio)

configuro los permisos para acceder al directorio privado1
sudo chmod 775 /var/www/html/privado1
sudo chown :www-data /var/www/html/privado1

**Crea un directorio llamado privado2 que permita el acceso sólo los usuarios del grupo1.**

sudo mkdir /var/www/html/privado2 (crear directorio)
configuro los permisos grupo1 puedan acceder al directorio privado2

sudo chown :grupo1 /var/www/html/privado2
sudo chmod 770 /var/www/html/privado2

**La directiva satisfy controla cómo se debe comportar el servidor cuando tenemos autorizaciones a nivel de host (order, allow, deny) y autorizaciones de usuarios (require).http://httpd.apache.org/docs/2.4/es/mod/mod_access_compat.html#satisf**

Para configurar adecuadamente el comportamiento del servidor en relación con la directiva Satisfy, necesitas considerar cómo combinar las autorizaciones basadas en usuarios/grupos (Require) y las basadas en direcciones IP o hosts Order, Allow, Deny o Require ip
Ejemplo de configuración para privado2:
apache
Copiar código
<Directory "/var/www/html/privado2">
    # Restricción basada en usuario o grupo
    AuthType Basic
    AuthName "Privado"
    AuthUserFile /etc/apache2/.htpasswd
    Require group grupo1

    # Restricción basada en dirección IP
    Require ip 127.0.0.1

    # Comportamiento combinado
    Satisfy any
</Directory>

Reiniciar Apache
sudo systemctl restart apache2

**En el directorio privado2 haz que sólo sea accesible desde el localhost, y 
estudia cómo se comporta la autorización si ponemos: satisfy any, satisfy all**

usar las opciones any y all
En el archivo de configuración de Apache (/etc/apache2/sites-available/000-default.conf) escribir

<Directory "/var/www/html/privado2">
    AuthType Basic
    AuthName "Directorio privado"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user

    Require ip 127.0.0.1

    Satisfy any
</Directory>

crer un .htpasswd 
sudo htpasswd -c /etc/apache2/.htpasswd usuario1

Reiniciar Apache
sudo systemctl restart apache2
--------------------------------------------------------------ACTIVIDAD 9 Authentication. Digest----------------------------------------------

**Crea dos subdirectorios en el host virtual default que se llamen grupo1 y grupo2.**
voy al directorio por defecto

cd /var/www/html

creo las carpetas grupo1 y grupo2

sudo mkdir grupo1
sudo mkdir grupo2

luego en la url de mi navegador pongo 127.0.0.1/grupo1 y 2

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/vhost.png)

**Crea varios usuarios con la utilidad htdigest, asignando a cada uno un dominio distinto (dominio1 y dominio2).**

La herramienta htdigest se utiliza para crear archivos de contraseñas encriptadas que permiten implementar autenticación HTTP Digest

crear el archivo en donde se van a guardar las contraseñas

sudo touch /etc/apache2/.htdigest

creo el dominio y el usuario

sudo htdigest /etc/apache2/.htdigest dominio1 usuario1

editamos la configuracion de nuestro sitio web

sudo nano /etc/apache2/sites-available/000-default.conf

y le asignamos las directivas a dominio1 y a dominio2

<Location "/dominio1">
    AuthType Digest
    AuthName "dominio1"
    AuthDigestProvider file
    AuthUserFile /etc/apache2/.htdigest
    Require valid-user
</Location>

<Location "/dominio2">
    AuthType Digest
    AuthName "dominio2"
    AuthDigestProvider file
    AuthUserFile /etc/apache2/.htdigest
    Require valid-user
</Location>

habilitamos el modulo digest

sudo a2enmod auth_digest

y reiniciamos apache

sudo systemctl restart apache2

**Configura el directorio grupo1 para que sólo puedan acceder los usuarios del dominio dominio1; y el directorio grupo2 para que sólo puedan acceder los usuarios del dominio dominio1**

en el directorio de mi sitio web 
 aqui

<Directory "/var/www/html/grupo1">
    AuthType Digest
    AuthName "dominio1"
    AuthDigestProvider file
    AuthUserFile /etc/apache2/.htdigest
    Require valid-user
</Directory>

y asin en el otro

y reiniciar apache

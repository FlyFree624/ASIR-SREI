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

**<IfModule>**
esta directiva se utiliza para incluir configuraciones en el archivo de configuración de Apache solo si un módulo específico está cargado
	
ejemplo: ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ifm.png)

Si el módulo mod_rewrite está habilitado, entonces se activa la reescritura de URL.

**LoadModule**
esta directiva se usa para cargar módulos adicionales en Apache, permitiendo la habilitación como la reescritura de URL

ejemplo: 
	
**Include**
	
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



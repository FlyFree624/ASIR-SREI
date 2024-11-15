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

<IfModule>
esta directiva se utiliza para incluir configuraciones en el archivo de configuración de Apache solo si un módulo específico está cargado
	
ejemplo: ![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ifm.png)

LoadModule
esta directiva se usa para cargar módulos adicionales en Apache, permitiendo la habilitación como la reescritura de URL

ejemplo: 
	
Include
	
<Directory>
Especifica configuraciones específicas para un directorio en particular
ejemplo:
	
![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ddi.png)

<Files>
Se usa para aplicar configuraciones específicas a ciertos archivos, basados en su nombre
ejemplo: 
	
<Location>
	
<VirtualHost>
	
¿Qué son los ficheros .htaccess?



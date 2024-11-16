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

en ip a veo la ip de mi servidor

en /etc/hosts añado mi ip y marisma.intranet

![](https://github.com/FlyFree624/ASIR-SREI/blob/main/tema0/imagenes/ma.png)


**Permite el acceso desde cualquier subdominio de "marisma.intranet"**

**Permite el acceso de las peticiones provenientes de "10.3.0.100" con máscara "255.255.0.0"**

**4 Modifica la configuración de forma que el acceso a dir1:
Se permita a "marisma.intranet" y no se permita desde 10.3.0.101"**

**5 Modifica la configuración de forma que el acceso a dir2:
Se permita a "10.3.0.100/8" y no a "marisma.intranet"**



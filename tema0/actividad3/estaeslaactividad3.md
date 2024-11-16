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

**Permite el acceso desde "marisma.intranet"**

**Permite el acceso desde cualquier subdominio de "marisma.intranet"**

**Permite el acceso de las peticiones provenientes de "10.3.0.100" con máscara "255.255.0.0"**

**4 Modifica la configuración de forma que el acceso a dir1:
Se permita a "marisma.intranet" y no se permita desde 10.3.0.101"**

**5 Modifica la configuración de forma que el acceso a dir2:
Se permita a "10.3.0.100/8" y no a "marisma.intranet"**



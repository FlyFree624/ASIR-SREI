**Instalación del servidor web apache. Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. 
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
![]()





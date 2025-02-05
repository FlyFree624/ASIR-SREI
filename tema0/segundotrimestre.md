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


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




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

![]()

Muestra todos los registros de redhat


Crea un fichero de texto que contenga los dominios;

Haz una consulta con dig empleando el fichero anterior

``ejercicio 1``



¿Quién, dónde y cuándo se crea el primer servidor web?

lo creo Tim Berners-Lee y fue creado en 1990

¿Qué es pila de protocolos usados por http?
pila de protocolos son los protocolos que trabajan en el del modelo osi

son:
HTTP, TCP, IP, ethernet/Wi-Fi, física
	
 ¿Componentes de una URL?
 protocolo, nombre del dominio, puerto, la ruta, los parametros
	
¿Pasos en la recuperación de una página web mediante HTTP?
 Convertir el nombre de dominio en una dirección IP, Abrir una conexión con el servidor web, enviar solicitud, respuestas del servidory muestra la pagina
	
Diferencia entre páginas dinámicas y estáticas
que las dinámicas generan su contenido en tiempo real, su contenido puede cambiar automáticamente sin que el desarrollador necesite modificar el codigo fuente
que las estáticas su contenido es fijo y no cambia a menos que el desarrollador modifique codigo fuente
	
¿Cómo usar telnet para acceder a un servidor web?

	en la terminal poner telnet y una ip
 telnet y la ip
 
Request. 
GET:
Solicita un recurso específico del servidor, obtener datos de una URL.
POST:

Envía datos al servidor para que los procese (generalmente en un formulario web o carga de archivos).
PUT:

Sube un recurso al servidor o actualiza uno existente

DELETE:

Elimina un recurso en el servidor.
	
Response:

100 Continue: El servidor ha recibido la solicitud inicial y el cliente puede continuar con su solicitud.

200 OK: La solicitud se procesó correctamente.
201 Created: El recurso ha sido creado con éxito en el servidor.

301 Moved Permanently: El recurso se ha movido de manera permanente a una nueva URL.
302 Found: El recurso está temporalmente en una nueva ubicación.

400 Bad Request: La solicitud tiene un error de sintaxis o es incorrecta.
403 Forbidden: El servidor se niega a cumplir con la solicitud, a pesar de que el cliente está autenticado.
404 Not Found: El recurso solicitado no fue encontrado en el servidor.

500 Internal Server Error: Error genérico del servidor.
	
Content type:

text/html:

Indica que el contenido es HTML

application/json:

Indica que el contenido es en formato JSON (JavaScript Object Notation)
application/xml:

Indica que el contenido está en formato XML
text/css:

Indica que el contenido es una hoja de estilos CSS.

text/javascript:

Indica que el contenido es un archivo JavaScript.


ejercicio 5

 	python -m http.server 8000

 para ejecutar un servidor en python solo debes ponerlo donde tienes tu archivo y lanzarlo al terminar tan solo debes colo car la ip de tu compañero en la url o si es tuys poner localhost o 127.0.0.1

 ![]()




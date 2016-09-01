## HTTP (Protocolo de Transferencia de Hipertexto)

### Introducción
___

### La Web

Internet (o La Web) es es un sistema de información de cliente/servidor distribuido masivamente como se muestra en el siguiente diagrama. 

![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/TheWeb.png)

Muchas aplicaciones se están ejecutando al mismo tiempo en la web, tales como la navegación web, e-mail, transferencias de archivos, transmisión de audio y vivo, entre otros. Para lograr una correcta comunicación entre el cliente y el servidor, esas aplicaciones deben estar en un mismo nivel de protocolo tales como HTTP, FTP, SMTP, POP, etc.

### Protocolo de Transferencia de Hipertexto (HTTP)
HTTP (Protocolo de  Transferencia de Hipertexto) es probablemente el protocolo de aplicación mas usado en Internet (La Web).

* HTTP es un protocolo cliente-servidor asimétrico de solicitud-respuesta como se ilustra. Un cliente HTTP envía una solicitud a un servidor HTTP. El servidor, a su vez, regresa un mensaje de respuesta. En otras palabras, HTTP es un protocolo de extracción, el cliente extrae información del servidor (en lugar de que el servidor arroje información al cliente).

![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP.png)

* HTTP es un protocolo sin estado. En otras palabras, la solicitud actual no sabe que es lo que se ha hecho en las solicitudes anteriores.

* HTTP permite la negociación del tipo de datos y la representación, con el fin de permitir que los sistemas sean construidos independientemente de los datos que se transfieren. 

* Citando el RFC2616: "El Protocolo de Transferencia de Hyper Texto es un protocolo de nivel de aplicación para sistemas de colaboración, información hipermedia distribuidos. Es un protocolo genérico, sin estados el cual puede ser usado para muchas tareas mas allá de su uso para hipertenso, tales como servidores de nombres y sistemas de gestión de objetos distribuidos, mediante de la extensión de sus métodos de solicitudes, códigos de error y cabeceras"

### Navegador

Cada vez que se ejecuta una URL desde tu navegador para obtener un recurso web usando HTTP, ej. http://www.nowhere123.com/index.html, el navegador convierte la URL en un mensaje de solicitud y lo envía al servidor HTTP. El servidor HTTP interpreta el mensaje de solicitud, y regresa un mensaje de respuesta apropiado, el cual es el recurso que solicitaste o un mensaje de error. Este proceso se ilustra abajo: 

![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_Steps.png)

### Localizador Uniforme de Recursos (URL)

Un URL (Localizador Uniforme de Recursos) es usa para identificar de forma única un recurso a través de internet. URL tiene la siguiente sintaxis:
```
protocolo://nombre-del-host:puerto/ruta-y-nombre-de-archivo
```

Hay 4 partes en un URL

1. *Protocolo*: El protocolo de nivel de aplicación usado por el cliente y servidor, ej., HTTP, FTP, y telnet.
2. *Nombre-del-host*: El nombre del dominio DNS (ej., www.nowhere.com) o la dirección IP (ej., 192.128.1.2) del servidor.
3. *Puerto*: El numero de puerto TCP del cual el servidor esta esperando respuestas entrantes del cliente.
4. *ruta-y-nombre-de-archivo*: El nombre y localización del recurso solicitado, bajo el directorio base de documentos del servidor.

Por ejemplo, en el URL *http://www.nowhere123.com/docs/index.html*, el protocolo de comunicación es HTTP, el nombre del host es *www.nowhere123.com*, el numero del puerto no esta especificado en el URL, y toma el numero por defecto, el cual es el puerto TCP 10 para HTTP, y la dirección y nombre del archivo para que el recurso sea localizado es *"/docs/index.html"*.

Otros ejemplos de URL son:
```
ftp://www.ftp.org/docs/test.txt
mailto::user@test101.com
news:soc.culture.Singapore
telnet://www.nowhere123.com/
```

### Protocolo HTTP

Como ya mencionamos, cada vez que ingresas un URL en la caja de dirección del navegador, el navegador traduce el URL a un mensaje de solicitud de acuerdo al protocolo especificado; y envía el mensaje de solicitud al servidor.

Por ejemplo, el navegador tradujo el url *http://www.nowhere123.com/docs/index.html* en el siguiente mensaje de solicitud:
```
GET /docs/index.html HTTP/1.1
Hots: www.nowhere.com
Accept: image/gif, image/jpg, * / *
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0, Windows NT 5.1)
(blank line)
```
Cuando este mensaje llega al servidor, el servidor puede tomar alguno de estas acciones:
1. El servidor interpreta la solicitud recibida, marea la solicitud en un archivo bajo el directorio de documentos del servidor.
2. El servidor interpreta la solicitud recibida, marea la solicitud a un programa y lo mantiene en el servidor, ejecuta el programa, y regresa la salida del programa al cliente.
3. La solicitud no puede ser concretada, el servidor envía un mensaje de error.

Un ejemplo del mensaje de respuesta del HTTP se muestra aquí:
```
HTTP/1.1 200 OK
Date: Sun, 18 Oct 2009 08:56:53 GTM
Server: Apache/2/2/14 (Win32)
Last-Modified: Sat, 20 Nov 2004 07:16:26 GTM
ETag: "10000000565a5-3c-3e95b66c2e680"
Accept-Ranges: bytes
Content-Length: 44
Connection: close
Content-Type: text/html
X-Pad: avoid browser bug

<html><body><h1>It works!</h1></body></html>
```

El navegador recibe un mensaje de respuesta, interpreta el mensaje y muestra el contenido del mensaje en la ventana del navegador de acuerdo al tipo de medio de la respuesta (como en la cabecera de respuesta Content-Type). Comúnmente el tipo de medios incluye *"text/plain", "text/html", "image/gif", "image/jpeg", "audio/mpeg", "video/mpeg", "application/msword", y "application/pdf"*.

En su estado de reposo, un servidor HTTP no hace nada mas que esperar a las direcciones IP y puertos especificados en la configuración de solicitudes entrantes. Cuando una solicitud llega, el servidor analiza la cabecera del mensaje, aplica las reglas especificadas en la configuración, y realiza la acción apropiada. El control principal del administrador sobre la acción del servidor we es a través de la configuración, el cual será tratado en mayor detalle en sesiones posteriores.

HTTP a través de TCP/IP

HTTP es un protocolo cliente-servidor de nivel de aplicación. Por lo general se ejecuta sobre una conexión TCP/IP, como se ilustra. (HTTP no necesita ejecutarse en TCP/IP. Solo presume un transporte fiable. Cualquier protocolo de transporte que protocolo que provea ese tipo de garantías puede utilizarse.)

![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_OverTCPIP.png)

TCP/IP (Protocolo de Control de Transmisión/Protocolo de Internet) es un conjunto protocolos de transporte y capas de red para que las maquinas se comunican unas a otras a través de la red.

IP (Protocolo de Internete) es un protocolo de capas de res, se encarga del direccionamiento y entubamiento de la red. En una red IP, a cada maquina se le asigna una dirección IP única (ej., 165.1.2.3), y el software IP es el responsable de enlutar un mensaje de la IP fuente a la IP destino. En IPv2 (IP versión 4), la dirección IP consiste de 4 bytes, cada rango de 0 a 255, separado por puntos, el cual es llamado forma quad-dotted. Este esquema de numeración soporta direcciones hasta 4G en la red. La ultima IPv6 (IP versión 6) soporta mas direcciones. Como memorizar es difícil para la mayoría de las personas, un nombre de dominio, tal como "www.nowhere123.com" se utiliza en lugar de. El DNS (Domain Name Service) traduce el dominio en la dirección IP (a través de las tablas de búsqueda distribuidos). Una dirección IP especial 127.0.0.1 siempre se refiere a tu propia maquina. Este nombre de dominio es "localhost" y puede ser usado para *pruebas de bucle local*.

TCP (Protocolo de Control de Transmisión) es un protocolo de capas de trasporte, responsable de establecer una conexión entre dos maquina. TCP consiste en dos protocolos: TCP y UDP (User Datagram Package). TCP de confianza, cada paquete tiene un numero de secuencia, y un reconocimiento es esperado. Un paquete puede ser re transmitido si no se recibe por el recibidor. La entrega de paquetes se garantiza en TCP. UDP no garantiza la la entrega del paquete, y por ende no es confiable. Sin embargo, UDP tiene menos sobrecarga de red y puede ser usado por aplicaciones como la transmisión de audio y video, donde la exactitud no es critica.

TCP multipliexa aplicaciones dentro de la maquina IP. Para cada maquina IP, TCP soporta(multiplexado) hasta 65536 puertos, desde el puerto 0 hasta 65535. Una aplicación, como HTTP o FTP, se ejecuta en un numero de puerto particular para las solicitudes entrantes. El puerto 0 a 1023 están pre asignados a protocolos populares. ej., HTTP al 80, FTP al 21, Telnet al 23, SMTP al 25, NNTP al 119, y DNS al 53. A partir del puerto 24 están disponibles para los usuarios.

A pesar de que el puerto 80 TCP eta pre asignado a HTTP, con el numero de puedo HTTP por defecto, esto no te prohibe correr el un servidor HTTP en otro numero de puerto asignado por un usuario (1024-65535) tales como el 8000, 8080, especialmente para pruebas de servidor. También puedes correr múltiples servidores HTTP en la misma maquina con diferentes números de puertos. Cuando un cliente emite un url sin indicar explícitamente el numero de puerto, ej., *http://www.nowhere123.com/docs/index.html* el navegador se conecta al numero de puerto por defecto 80 del host *www.nowhere123.com*. Necesitas especificar explícitamente en numero de puerto en la URL, ej., *http://www.nowhere123.com:8000/docs/index.html* si el servidor esta esperando el puerto  y no al puerto por defecto 80.

En resumen, para comunicarte a través de TCP/IP, necesitas saber (a) dirección IP o nombre del host, (b) El numero de puerto.


### Especificaciones HTTP

Las especificación HTTP se mantiene por [W3C (Word-wide Web Consortium)](http://www.w3.org) y disponibles en http://www.w3.org/standards/techs/http. Actualmente hay dos versiones de HTTP, llamadas, GTTP/1.0 y HTTP/1.1. La versión original, TTP/0.9 (1991), escrita por Tim Berners-Le, es un protocolo simple para transferir datos puros a través de internet. HTTP/1.0 (1996) (definido en RFC 1945), mejoro el protocolo permitiendo mensajes tipo MIME. HTTP/1.0 no aborda asuntos de prosees, caché, conexión persistente, host virtuales y rango de descargas. Esas características son proporcionadas en HTTP/1.1 (1999) (definida en el RFC 2616).

### Servidor HTTP Apache o Servidor Apache Tomcat
___
Un servidor HTTP (Tales como Servidor HTTP Apache o Servidor Apache Tomcat) es necesario para estudiar el Protocolo HTTP.

El servidor Apache HTTP es un servidor de producción industrial, producido por Apache Software Fundation (ASF) @ [www.apache.org](http://www.apache.org). ASF es una fundación de software de código libre. Es decir, Apache HTTP server es gratis, con código abierto.

El primer servidor HTTP fue escrito por Tim Berners Le en el CERN (Centro Europeo para Investigación Nuclear) en Geneva, Suiza, quien también invento HTML. Apache fue creado en NCSA (Centro Nacional para Aplicaciones de supercomputación, USA) servidor "https 1.3", a inicio de 1995. Apache probablemente obtuvo su nombre del echo de que consiste en sodio origina (De un servidor web https de NCSA) mas algunos parches. O del nombre de un tribu de indios americanos.

Leer [Apache How-to](https://www.ntu.edu.sg/home/ehchua/programming/howto/Apache_HowToInstall.html) en como instalar y configurar un servidor HTTP: o [Tomcat How-to](https://www.ntu.edu.sg/home/ehchua/programming/howto/Tomcat_HowTo.html) para instalar y comenzar con el Servidor Apache Tomcat.


### Mensajes de Solicitud y Repuesta HTTP
___
El servidor y cliente HTTP se comunican enviando mensajes de texto. El cliente envía un mensaje de solicitud al servidor. El servidor, a si vez, regresa un mensaje de respuesta.

Un mensaje HTTP consiste en una cabecera de mensaje y un cuerpo de mensaje opcional, separadas por una linea en blanco como se alista abajo:

![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_MessageFormat.png)

### Mensaje de solicitud HTTP

El formato de un  mensaje de solicitud es el siguiente:

![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessage.png)

#### Linea de solicitud

La primera linea de la cabecera se llama *linea de solicitud*, seguida de *cabeceras de colicitud* opcionales.

La linea de solicitud tiene la sintaxis siguiente:
```
request-method-name  request-URI  HTTP-version
```
* *request-method-name*: El protocolo HTTP define un conjunto de métodos de solicitud, ej., GET, POST, HEAD y OPTIONS. El cliente puede usar uno de esos métodos para enviar una solicitud al servidor. 
* *request-URI*: especifica el recurso solicitado.
* *HTTP-version*: Dos versiones son usadas actualmente: HTTP/1.0 y HTTP/1.1.

Ejemplos de lineas de petición son:
```
GET /test.html HTTP/1.1
HEAD / query.html HTTP/1.0
POST /index.html HTTP/1.1
```

#### Cabeceras de Solicitud

Las cabeceras de solicitud están en la forma de pares *name:valie*. Miltiples valores, separados por comas, pueden ser especificadas.
```
request-header-name:  request-header-value1, request-header-value2, ...
```
Ejemplos de cabeceras de petición son:
```
Host: www.xyz.com
Connection: Keep-Alive
Accept: image/gif, image/jpeg, * / *
Accept-Language: us-en, fr, cn
```

#### Ejemplo
El siguiente ejemplo  muestra un mensaje de petición HTTP:
![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessageExample.png)

### Mensaje de respuesta HTTP
El formato de un mensaje de respuesta es el siguiente: 
![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_ResponseMessage.png)

#### Linea de estado
La primera linea es llamada *Linea de estado*, seguida por una cabecera de respuesta opcional.
La linea de estado tiene la siguiente sintaxis:
```
HTTP-version  status-code  reason-phrase
```
* *HTTP-version*: La versión HTTP es usado en esta sesión. Ya sea HTTP/1.0 o HTTP/1.1.
* *status-code*: Un numero de 3 digito generada por el servidor para reflejar la salida de la solicitud.
* *reason-phrase*: Da una corta explicación del código de estado.
* Códigos de estados comunes y significados son "200 OK", "404 Not Found ", "403 Forbidden", "500 Internal Server Error".

Ejemplos de lineas de estado son:
```
HTTP/1.1 200 OK
HTTP/1.0 404 Not Found
HTTP/1.1 403 Forbidden
```
#### Cabeceras de respuesta
La cabeceras de respuesta están en formas de pares *name:valie*:
```
response-header-name:  response-header-value1, response-header-value2, ...
```
Ejemplos de cabeceras de respuesta son:
```
Content-Type: text/html
Content-Length: 35
Connection: Keep-Alive
Kelp-Alive: timeout=15, max=100
```
El cuerpo del mensaje de respuesta contiene el recurso de datos solicitados.

#### Ejemplo
El siguiente imagen muestra un mensaje de respuesta simple:
![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_ResponseMessageExample.png)

---
 Fuente original: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/HTTP_Basics.html

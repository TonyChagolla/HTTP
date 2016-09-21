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

### Métodos de solicitud HTTP
---
El protocolo HHTP define un conjunto de métodos de solicitud. Un cliente puede usar esos métodos de solicitud para enviar una un mensaje de solicitud a un servidor HTTP. Esos métodos son.
* GET: Un cliente puede usar la solicitud GET para obtener un recurso del servidor web del servidor.
* HEAD: Un cliente puede usar la solicitud HEAD para obtener la cabecera que unas solicitud GET puede obtener. Ya que la cabecera contiene la ultima modificación de los datos, esto puede ser usado para comparar con la copia local de la caché.
* POST: Usado para publicar datos en un servidor web.
* PUT: Pedir al servidor almacenar datos.
* DELETE: Pedir al servidor que elimine datos.
* TRACE: Pedir al servidor que regrese un rastreo de diagnostico de las acciones que realiza.
* OPTION: Pedir al servidor que regrese una lista de métodos de solicitud soportados.
* CONNECT: Usado para indicar al proxy que cree una conexión con otro host y simplemente responder el contenido, sin que intente analizar o almacenar en caché.
* Otras métodos de extensión.

### Metodo de solicitud "GET"
___
Get es el método de solicitud HTTP mas común. Un cliente puede usar el método de solicitud GET para solicitar una parte de un recurso en un servidor HTTP. Un mensaje de solicitud GET tiene la siguiente sintaxis. 
```
GET request-URI HTTP-version
(Cabeceras opciones)
(blank line)
(Cuerpo de solicitud opcional)
```
* La palabra clave GET distingue mayusculas y minúsculas y debe ser escrito con mayusculas.
* request-URI: especifica la ruta del recurso solicitado, en cual  debe iniciar desde la raes "/" del documento base del directorio.
* HTTP-version: Ya sea HTTP/1.0 o HTTP/1.1. Este cliente negocia el protocolo a usar para la sesión actual. Por ejemplo, el cliente puede pedir usar HTTP/1.1. Si el servidor no soporta HTTP/1.1, este informará al cliente en la respuesta para que use HTTP/1.0.
* El cliente puede usar cabeceras opcionales (tales como Accept, Accept-Lenguage, etc) para negociar con el servidor y pedir que envíe contenido especifico(ej., El lenguaje que el cliente prefiere).
* El mensaje de solicitud GRT tiene un cuerpo de solicitud opcional que contiene la cadena de consulta.

#### Probando solicitud HTTP
Hay muchas maneras de probar una solicitud HTTP. Puedes usar un programa de utilidades tal como *"telnet"* o *"hyperterm"*, o escribir tu propio programa de red para enviar un mensaje de solicitud a un servidor HTTP para probar las diferentes solicitudes HTTP.


##### TELNET
"Telnet" es una utilidad de red muy útil. Puedes usar telnet para establecer una conexión TPC con un servidor: y emitir una solicitud HTTP. Por ejemplo, supone que iniciaste un servidor HTTP en el localhost (127.0.0.1) en el puerto 8000:
```
> telnet
telnet> help
... telnet help menu ...
telnet> open 127.0.0.1 8000
Connecting To 127.0.0.1...
GET /index.html HTTP/1.0
(Hit enter twice to send the terminating blank line ...)
... HTTP response message ...
```
Telnet tiene un protocolo basado en caracteres. Cada carácter que ingresas en el cliente de telnet será enviado al servidor inmediatamente. Por lo tanto, no puedes cometer errores tipográficos cuando ingresas un comando, así como el delete y backspace serán enviados al servidor. Debes habilidad el "local echo" para ver los caracteres que ingresas. Revisa el manual de telnet (Busca en la ayuda de Windows) para detalles de como usar telnet.

##### Programa de red
Tu puedes crear tu propio programa de red para emitir peticiones HTTP a un servidor HTTP. Tu programa de red primero debe establecer una conexión TCP/IP con el servidor. Una vez que la conexión es establecida, puedes emitir las solicitudes.

Un ejemplo de un programa de red escrito en Java es como el que se muestra (asumiendo que el servidor HTTP esta corriendo en el localhost (dirección IP 127.0.0.1) en el puerto 8000):
```
import java.net.*;
import java.io.*;
   
public class HttpClient {
   public static void main(String[] args) throws IOException {
      // El host y el servidor serán conectados.
      String host = "127.0.0.1";
      int port = 8000;
      // Crea un socket TCP y conecta host:port.
      Socket socket = new Socket(host, port);
      // Crea las flijos de entrada y salida para el socket.
      BufferedReader in
         = new BufferedReader(
              new InputStreamReader(socket.getInputStream()));
      PrintWriter out
         = new PrintWriter(socket.getOutputStream(), true);
      // Enviar la solicitud al servidor HTTP.
      out.println("GET /index.html HTTP/1.0");
      out.println();   // blank line separating header & body
      out.flush();
      // Lee la respuesta y mostrar en la pantalla de consola.
      String line;
      // readLine() regresa null si el servidor cierra el ocket.
      while((line = in.readLine()) != null) {
         System.out.println(line);
      }
      // Cierra los flujos de E/S.
      in.close();
      out.close();
   }
}
```

### Solicitud GET HTTP/1.0
A continuación se muestra un mensaje de solicitud de un GET HTTP/1.0 (emitido por telnet o tu programa de red - asumiendo que has iniciado el servidor HTTP):
```
GET /index.html HTTP/1.0
(enter twice to create a blank line)
```
```
HTTP/1.1 200 OK
Date: Sun, 18 Oct 2009 08:56:53 GMT
Server: Apache/2.2.14 (Win32)
Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
ETag: "10000000565a5-2c-3e94b66c2e680"
Accept-Ranges: bytes
Content-Length: 44
Connection: close
Content-Type: text/html
X-Pad: avoid browser bug
   
<html><body><h1>It works!</h1></body></html>
   
Connection to host lost.
```
En este ejemplo, el cliente emite una solicitud GET para pedir por un documento llamado *"índex.html"*; y negocia para usar el protocolo HTTP/1.0. Una linea en blanca es necesaria después de la linea de cabecera. Este mensaje de solicitud no contiene un cuerpo.

El servidor recibe el mensaje de solicitud, interpreta y marea el request-URI a un directorio de documento. Si el documento solicitado esta disponible, el servidor regresa el documento con un estado de estado "200 OK". La cabecera de respuesta provee la descripción necesaria del documento que regresa, tales como la ultima modificación (Last-Modified), el MIME type (Content-Type), y el largo del documento (Content-Length). El cuerpo de respuesta contiene el documento solicitado. El navegador dará formato y mostrará el documento de acuerdo al tipo de medio (ej.Texto plano, HTML, JPWG, GIF, etc) y otra dorfirmacion obtenida de la cabecera de respuesta.

Notas:
* El método de solicitud GET distingue mayusculas y minúsculas, y debe ser escrito en mayúsculas. 
* Si el método de solicitud tiene errores de escritura, el servidor regresara un mensaje de error "501 Method Not Implmeented".
* Si el nombre del método de solicitud no esta permitido, el servidor regresará un mensaje de  error "405 Method Not Allowed". Ej., DELETE es un nombre de método valido, pero no será permitido (o implementado) por el servidor.
* Si el request-URI no exists, el servidor enviara un mensaje de error "404 Not Found". Tienes que emitir el request-URI adecuado, iniciando por la raíz del documento "/" de otra manera, el servidor regresara un mensaje de respuesta "400 Bad Request".
SI la HTTP-version no se encuentra o es incorrecto, el servidor regresara un mensaje de respuesta "400 Bad Request".
EN HTTP/1.0 por defecto, el servidor cierra la conexión TCP después de que la respuesta es entregada. Si usas telnet para conectar con el servidor, el mensaje "Connection to host lost" aparcara inmediatamente después de que el cuerpo de respuesta fue recibido. Puedes usar una cabecera opcional "Connection: Keep-Alive" para solicitar una conexión persistente (o keep-alive), para que otra solicitud pueda ser enviada a través de la misma conexión TCP para lograr una mejor eficiencia de red. Por otro lado HTTP/1.1 usa la conexión keep-alive por defecto.

### Codigo de estado de respuesta
La primera linea de un mensaje de respuesta (ej. la linea de estado) contiene un código de estado de respuesta, el cual es generado por el servidor para indicar la salida de la solicitud.

El codillo de estado es un numero de 3 dígitos: 
* 1xx (Información): solicitud recibida: el servidor continua el proceso.
* 2xx (Exito): La solicitud fue recibida exitosamente, entendida, aceptada y servida.
* 3xx (Redireccion): Otras medidas deben tomarse antes de completar la solicitud.
* 4xx (Error de cliente) La respuesta contiene una sintaxis errónea o no puede ser entendida.
* 5xx (Error de servidor) El servidor falló para cumplir una solicitud valida aparente.

Algunos de los códigos de estado comunes son:
* 100 Continue: El servidor recibir la solicitud y esta en proceso de dar una respuesta.
* 200 OK: Respuesta cumplida.
* 301 Move Permanently:  El recurso solicitado ha sido movido permanentemente a una nueva localización. La URL de la nueva localización es dada en la cabecera llamada "Location". El cliente debe emitir una nueva solicitud para la nueva localización. La aplicación debe actualizar todas las referencias a esta nueva localización.
* 302 Found & Redirect (or Move Temporarily): Igual que el 301, pero la nueva localización es temporal. El cliente debe emitir una nueva solicitud, pero las aplicaciones no necesitan actualizar las referencias.
* 304 Not Modified: En respuesta a la condición de petición GET If-Modified-Since, el servidor notifica que el recurso solicitado no se ha modificado.
* 400 Bad Request: El servidor no pudo interpretar o entender la solicitud, probablemente un error de sintaxis el en mensaje de solicitud.
* 401 Authentication Required: El recurso solicitado esta protegido, probablemente requiere credenciales del cliente (username/password). El cliente debe re enviar la solicitud con la credenciales (username/password).
* 403 Forbidden: El servidor se rehusa a suministrar el recurso, si importar la identidad del cliente.
* 404 Not Found: El recurso requerido no puede ser encontrado en el servidor.

* 405 Method Not Allowed: El método de solicitud usado, ej., POST, PUT, DELETE, es un método valido. Si embargo, el servidor no soporta ese método para el recurso solicitado.
* 408 Request timeout:
* 414 Request URI to Large:
* 500 Internal Server Error: El servidor esta confundido, normalmente causado por un error el programa del servidor que responde a la solicitud.
* 501 Method Not Implemented: El método de solicitud usado es invalido (puede ser usado por un error de escritura, ej., "GET" escrito como "Get").
* 502 Bad Gateway: Proxy o Gateway indica que ha recibido una mala respuesta del servidor de origen.
* 503 Service Unavailable: El servidor no puede responder debido a una sobrecarga o mantenimiento. El cliente puede intentar mas tarde.
* 503 Gateway Timeout: El Proxy o Gateway indica que ha recibido un timeout del servidor de origen.

### Mas ejemplos de Peticiones GET HTTP/1.0

##### Ejemplo: Metodo de solicitud mal escrito
En la solicitud, "GET" es escrito como "get". El servidor regresa un error "501 Method Not Implemented". La cabecera de respuesta "Allow" dice al cliente los métodos permitidos.
```
get /test.html HTTP/1.0
(enter twice to create a blank line)
```
```
HTTP/1.1 501 Method Not Implemented
Date: Sun, 18 Oct 2009 10:32:05 GMT
Server: Apache/2.2.14 (Win32)
Allow: GET,HEAD,POST,OPTIONS,TRACE
Content-Length: 215
Connection: close
Content-Type: text/html; charset=iso-8859-1
   
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>501 Method Not Implemented</title>
</head><body>
<h1>Method Not Implemented</h1>
<p>get to /index.html not supported.<br />
</p>
</body></html>
```

##### Ejemplo: 404 Archivo no encontrado
En esta solicitud GET, el URL solicitado "/t.html" no puede ser encontrado en el directorio de documentos del servidor. EL servidor regresa un error "404 Not Found".
```
GET /t.html HTTP/1.0
(enter twice to create a blank line)

```
```
HTTP/1.1 404 Not Found
Date: Sun, 18 Oct 2009 10:36:20 GMT
Server: Apache/2.2.14 (Win32)
Content-Length: 204
Connection: close
Content-Type: text/html; charset=iso-8859-1
   
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>404 Not Found</title>
</head><body>
<h1>Not Found</h1>
<p>The requested URL /t.html was not found on this server.</p>
</body></html>
```

##### Ejemplo: Version HTTP equivocada
EN sets solicitud GET, la versión HTTP fue mal escrita, resultado de una mala sintaxis. El servidor regresa un error "404 Bad Request". La versión HTTP debe ser  HTTP/1.0 o HTTP/1.1
```
GET /index.html HTTTTTP/1.0
(enter twice to create a blank line)
```
```
HTTP/1.1 400 Bad Request
Date: Sun, 08 Feb 2004 01:29:40 GMT
Server: Apache/1.3.29 (Win32)
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<HTML><HEAD>
<TITLE>400 Bad Request</TITLE>
</HEAD><BODY>
<H1>Bad Request</H1>
Your browser sent a request that this server could not understand.<P>
The request line contained invalid characters following the protocol string.<P><P>
</BODY></HTML>
```
Nota: La ultima versión de Apache 2.2.14 ignora este error y regresa el documento con un código de estado "200 OK".

##### Ejemplo: Recurso URI equivocado
En la siguiente solicitud GET, el URI solicitado no inicia desde la raíz "/", resultando en una "bad request"
```
GET test.html HTTP/1.0
(blank line)
```
```
HTTP/1.1 400 Bad Request
Date: Sun, 18 Oct 2009 10:42:27 GMT
Server: Apache/2.2.14 (Win32)
Content-Length: 226
Connection: close
Content-Type: text/html; charset=iso-8859-1
   
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>400 Bad Request</title>
</head><body>
<h1>Bad Request</h1>
<p>Your browser sent a request that this server could not understand.<br />
</p>
</body></html>
```

##### Ejemplo: Keep-Alive Connection
Por defecto, para una solicitud HTTP/1.0 el servidor cierra la conexión una ves que la respuesta fue entregada. Puedes solicitad que la conexión TCP continue, (para poder enviar otra solicitud por la misma conexión TCP, (para mejorar la eficiencia de la red) por medio de una cabecera opcional "Connection: Keep-Alive" El servidor incluye una cabecera de respuesta "Connection: Keep-Alive" para informar al cliente que puede enviar otra solicitud usando esta conexión, antes de que se cierre la conexión. Otra cabecera de respuesta "Keep-Alive: timeout=x, max=x" le dice al cliente cuando se cerrara la conexión (en segundos) y numero máximo de solicitudes que puede enviar por medio de esta conexión.
```
GET /test.html HTTP/1.0
Connection: Keep-Alive
(blank line)
```
```
HTTP/1.1 200 OK
Date: Sun, 18 Oct 2009 10:47:06 GMT
Server: Apache/2.2.14 (Win32)
Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
ETag: "10000000565a5-2c-3e94b66c2e680"
Accept-Ranges: bytes
Content-Length: 44
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: text/html
   
<html><body><h1>It works!</h1></body></html>
```

Notas:
* El mensaje "Connection to host lost" (para telnet) aparece después de que termine el tiempo "keep-alive".
* Antes de que el mensaje "Conection to host lost" aparezca, puedes enviar otra solicitud a través de la misma conexión TCP.
* La cabecera "Connection: Keep-alive" no reconoce mayúsculas o minúsculas. El espacio es opcional.
* Si una cabecera opcional es mal escrita o invalida, será ignorada por el servidor.

##### Ejemplo: Accediendo a un recurso protegido
La siguiente solicitud GET trata de acceder a un recurso protegido. El servidor regresa un error "403 Forbidden". En este ejemplo, el directorio "htdocs\forbidden" esta configurado para denegar cualquier acceso en la configuración del servidor Apache HTTP en el archivo de configuración "https.conf" como se muestra:
```
<Directory "C:/apache/htdocs/forbidden">
   Order deny,allow
   deny from all
</Directory>
```
```
GET /forbidden/index.html HTTP/1.0
(blank line)
```
```
HTTP/1.1 403 Forbidden
Date: Sun, 18 Oct 2009 11:58:41 GMT
Server: Apache/2.2.14 (Win32)
Content-Length: 222
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: text/html; charset=iso-8859-1
   
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>403 Forbidden</title>
</head><body>
<h1>Forbidden</h1>
<p>You don't have permission to access /forbidden/index.html
on this server.</p>
</body></html>
```

### Solicitudes GET condicionales
EN todos los ejemplos previos, el servidor regresa el documento entero y si la solicitud puede ser completada. Debes usar cabeceras de solicitud adicionales para emitir un una "solicitud condicional". Por ejemplo, para pedir un documento basado en ultima fecha de modificación (para decidir si usar la copia local caché), o para pedir una porción del documento (o rango) en vez del documento entero (útil para descargar documentos grandes).

Las cabeceras de solicitud condicionales incluyen:
* *If-Modified-Since* (comprueba el coding de  estado de respuesta "304 Not Modified").
* *If-Unmodified-Since*
* *If-Match*
* *If-None-Match*
* *If-Range*

### Cabeceras de Solicitud
Esta sección describe algunas de las  cabeceras de solicitud mas usadas. La sintaxis del nombre de cabecera son palabras con la inicial en mayuscula unidas con un guión (-), ej., *Content-Length*, *If-Modified-Since*.

**Host:    doman-name**   -   HTTP/1.1 soporta host virtuales. Múltiples nombres DNS (ej., www.nowhere123.com y www.nowhere456.com) pueden decidir en el mismo servidor físico, con sus propios directorios raíz de documentos. La cabecera *Host* es obligatorio  en HTTP/1.1 para seleccionar uno de los host.

Las siguientes cabeceras pueden ser usadas para negociar contenido por el cliente para pedir al servidor  que envíe el tipo preferido de documentos (en términos de medios, ej., JPEG vs. GIF, o el lenguaje usado ej., Ingles vs Frances) si el servidor mantiene múltiples versiones del mismo documento.

**Accept: mime-type-1, mime-tupe 2,  ...** - El cliente puede usar la cabecera *Accept* para indicar al servidor los MIME types que soporta y prefiere. Si el servidor tiene múltiples versiones del documento solicitado(ej., an imagen GIF and PNG, or a document in TXT or PDF), puede revisar esta cabecera para decidir que versión entregar al cliente. (Ej. PNG es mas avanzad que GIF, pero no todos los navegadores soportan PNG.) Este proceso es llamado negociación de tipo de contenido.

**Accept-Lenguage: lenguage-1, lenguage-2, ...** - EL cliente puede usar la cabecera *Accept-Lenguage* para indicar al servidor cual lenguaje soporta y prefiere. SI el servidor tiene múltiples versiones del documento (ej., en Ingles, Chino, Frances), puede revisar esta cabecera para decidir cual versión regresar. Este proceso es llamado negociación de idioma.

**Accept-Charset: Chartset-1, Charset-2, ...** Para negociar un conjunto de caracteres, El cliente puede usar esta cabecera para informar al servidor cuales conjuntos de caracteres soporta y prefiere. Ejemplos de conjuntos de caracteres son ISO-0059-1, ISO-8859-2, ISO-8859-5, BIG5, UCS2, UCS4, UTF8.

**Accept-Encoding: encoding-method-1, encoding-method-2, ...** - El cliente puede usar esta cabecera para informar al servidor el tipo de codificación que soporta. Si el servidor tiene una versión codificada (o comprimida) del documento solicitado, puede regresar la versión codificada soportada por el cliente. EL servidor puede escoger codificar el documento entes de regresar al cliente para  reducir el tiempo de transmisión. El servidor puede establecer  la cabecera de respuesta "Content-Encoding" para informar al cliente que el documento que regreso esta codificado. Los métodos comunes de codificado son *"x-gzip (.gz, .tgz)"* y *"x-compress (.Z)"*.

**Connection: Close|Keep-Alive** - El cliente puede usar esta cabecera para indicar al servidor si quiere cerrar la conexione después de la solicitud, o para mantener  la conexión abierta para otra solicitud. HTP/1.1 usa conexión persistente (keep-alive) por defecto. HTTP/1.0 cierra la conexión por defecto.

**Refer: refer-URL** - El client usa esta cabecera par indicar la referencia de esta solicitud. Si das click en un link de una pagina web 1 para visitar una pagina web 2, la pagina web 1 es la referencia para la solicitud de la pagina web 2. Todos los navegadores implementan esta cabecera, la cual puede ser usado para rastrear de donde vienen las peticiones (para anuncios web, o contenido personalizado). Si embargo, esta cabecera no es muy confiable y puede ser fácilmente falsificada. 

**User-Agent: browser-type** - Identifica el tipo de navegador usado para hacer la solicitud. El servidor puede usar esta información para regresar diferentes documentos dependiendo del tipo de navegador.

**Content-Length: number-of-bytes** - Usado por la petición POST, para informar al servidor la longitud del cuerpo de respuesta.

**Content-Type: mime-type** - Usado por la petición para informar al servidor el tipo de medios del cuerpo de respuesta.

**Cache-Control: no-cache\...** - El cliente puede usar esta cabecera para especificar como se agregan las paginas a la caché por el servidor proxy. *"no-cache"* requiere que el proxy obtenga una copia actualizada del servidor original, incluso si hay una copia local en la caché. (Los servidores HTTP/1.0 no reconocen *"Cache-Control: no-cache"*. En su ligar, usa *"Pragma: no-cache"*. Incluir ambas cabeceras si no estas seguro de la versión del servidor)

**Authorization:** Usado por el cliente para proporcionar sus credenciales (username/password) para acceder a recursos protegidos.

**Cookie: cookie-name-1=cookie-value-1, coockie-name-2=cookie-value-2, ...** - El cliente usa esta cabecera para regresar los cookies al servidor, los cuales fueron colocados por el servidor antes para estado de administracion.

**If-Modified-Since: date** - Indica al servidor que envíe una copia solo si fue modificada después de una fecha especifica.

### Solicitud Get para Directorio
Supongamos que un directorio *"testdir"* esta presente en el directorio base de documentos *"htdocs"*.
Si un cliente emite una solicitud GET a *"/testdir/"* (ej, en el directorio).
1. El servidor regresara *"/testdir/index.html"* si el directorio contiene un archivo *"index.html"*
2. De otra manera, el servidor regresara un listado del directorio, si es listado de directorio esta habilitado en la configuración del servidor.
3. De otra manera, el servidor regresará "404 Page Not Found".

Es interesante tomar nota de que si un cliente emite una solicitud GET *"/testdir"* (sin especificar la ruta del directorio "/"), el servidor regresara una "301 Move Permanently", con una nueva *"Location"* del *"testdir"*, como se muestra:
```
GET /testdir HTTP/1.1
Host: 127.0.0.1
(blank line)
```
```
HTTP/1.1 301 Moved Permanently
Date: Sun, 18 Oct 2009 13:19:15 GMT
Server: Apache/2.2.14 (Win32)
Location: http://127.0.0.1:8000/testdir/
Content-Length: 238
Content-Type: text/html; charset=iso-8859-1
   
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://127.0.0.1:8000/testdir/">here</a>.</p>

</body></html>
```
La mayoría de los navegadores continuaran con otra solicitud a *"/testdir/"*. Por ejemplo, si tu emites *http://127.0.0.1:8000/testdir* sin el "/" desde un navegador, puedes notar que el "/" fue agregado a la dirección después de que la respuesta fue dada. La moraleja de la historia es: debes incluir el "/" para la solicitud del directorio para ahorrar una solicitud adicional GET.

### Emitir una solicitud GET a través de un servidor proxy
Para enviar una solicitud GET a través de un servidor proxy, (a) establecer una conexión TCP al servidor proxy; (b) usar un request-URI absoluto *http://hostname:port/path/fileName* al servidor objetivo.

El siguiente rastreo fue capturado usando Telnet. Una conexión es establecida con el servidor proxy, y una solicitud GET es emitida. Request-URI absoluta es usada en la linea de petición.

```
GET http://www.amazon.com/index.html HTTP/1.1
Host: www.amazon.com
Connection: Close
(blank line)
```
```
HTTP/1.1 302 Found
Transfer-Encoding: chunked
Date: Fri, 27 Feb 2004 09:27:35 GMT
Content-Type: text/html; charset=iso-8859-1
Connection: close
Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
Set-Cookie: skin=; domain=.amazon.com; path=/; expires=Wed, 01-Aug-01 12:00:00 GMT
Connection: close
Location: http://www.amazon.com:80/exec/obidos/subst/home/home.html
Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
   
ed
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<HTML><HEAD>
<TITLE>302 Found</TITLE>
</HEAD><BODY>
<H1>Found</H1>
The document has moved
<A HREF="http://www.amazon.com:80/exec/obidos/subst/home/home.html">
here</A>.<P>
</BODY></HTML>
   
0
 
```
Tome en cuenta que la respuesta se devuelve en "trozos".

### Método de Solicitud "HEAD"
___
La solicitud HEAD es similar a la petition GET. Sin embargo, el servidor regresa únicamente la cabecera de respuesta sin el cuerpo de la respuesta, el cual contiene el documento actual. La solicitud HEAD es útil para comprobar las cabeceras, tal como *Last-Modified, Content-Type, Content-Length*, antes de enviar la solicitud GET apropiada para recuperar el documento.

La sintaxis de la solicitud HEAD es la siguiente:
```
HEAD request-URI HTTP-version
(other optional request headers)
(blank line)
(optional request body)
```

##### Ejemplo
```
HEAD /index.html HTTP/1.0
(blank line)
```
```
HTTP/1.1 200 OK
Date: Sun, 18 Oct 2009 14:09:16 GMT
Server: Apache/2.2.14 (Win32)
Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
ETag: "10000000565a5-2c-3e94b66c2e680"
Accept-Ranges: bytes
Content-Length: 44
Connection: close
Content-Type: text/html
X-Pad: avoid browser bug
```
Tome en cuenta que la respuesta consiste únicamente en la cabecera sin el cuerpo, el cual contiene el documento actual.

### Metodo de Solicitud "OPTIONS"
___
Un cliente puede usar el método de solicitud OPTIONS para consultar cuales métodos de solicitud son soportados. La sintaxis para el mensaje de solicitud OPTIONS es:
```
OPTIONS request-URI|* HTTP-version
(other optional headers)
(blank line)
```
"*" pueden ser usadas en lugar de una request-URI para indicar que la solicitud no aplica a ningún recurso en particular.

##### Ejemplo
Por ejemplo, la siguiente solicitud OPTIONS es enviada a través de un servidor proxy:
```
OPTIONS http://www.amazon.com/ HTTP/1.1
Host: www.amazon.com
Connection: Close
(blank line)
```
```
HTTP/1.1 200 OK
Date: Fri, 27 Feb 2004 09:42:46 GMT
Content-Length: 0
Connection: close
Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
Allow: GET, HEAD, POST, OPTIONS, TRACE
Connection: close
Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
(blank line)
```
Todos los servidores que permiten solicitudes GET aceptarán solicitudes HEAD. Algunas veces, Head no esta listado.

### Metodo de Solicitud "TRACE"
Un cliente puede en ciar una solicitud TRACE para pedir al servidor que regrese un seguimiento de diagnostico.
La solicitud TRACE tiene la siguiente sintaxis:
```
TRACE / HTTP-version
(blank line)
```

##### Ejemplo
El siguiente ejemplo muestra una solicitud TRACE emitida a través de un servidor proxy.
```
TRACE http://www.amazon.com/ HTTP/1.1
Host: www.amazon.com
Connection: Close
(blank line)
```
```
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Date: Fri, 27 Feb 2004 09:44:21 GMT
Content-Type: message/http
Connection: close
Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
Connection: close
Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
   
9d
TRACE / HTTP/1.1
Connection: keep-alive
Host: www.amazon.com
Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
X-Forwarded-For: 155.69.185.59, 155.69.5.234
   
0
   
```
(Para comparar la solicitud TRACE con una ruta de rastro)


### Enviando formulario de datos HTML y cadenas de consulta
___
In muchas aplicaciones de ínter,et, tales como comercio electrónico y motores de búsqueda, los clientes están obligados a enviar información adicional al servidor (ej., nombre, dirección, palabras clave). Basado en los datos enviados, el servidor toma la acción apropiada y produce una respuesta personalizada.

Los clientes suelen presentarse con un formulario (producida usando la etiqueta HTML <form>). Una vez llenada con los datos requeridos y presionado el botón de enviar, el navegador empaqueta los datos del formulario y lo envía al servidor, usando ya sea una solicitud GET o POST.

El siguiente es un ejemplo de un formulario HTML, el cual es producido por el siguiente HTML script.
```
<html>
<head><title>A Sample HTML Form</title></head>
<body>
  <h2 align="left">A Sample HTML Data Entry Form</h2>
  <form method="get" action="/bin/process">
    Enter your name: <input type="text" name="username"><br />
    Enter your password: <input type="password" name="password"><br />
    Which year?
    <input type="radio" name="year" value="2" />Yr 1
    <input type="radio" name="year" value="2" />Yr 2
    <input type="radio" name="year" value="3" />Yr 3<br />
    Subject registered:
    <input type="checkbox" name="subject" value="e101" />E101
    <input type="checkbox" name="subject" value="e102" />E102
    <input type="checkbox" name="subject" value="e103" />E103<br />
    Select Day:
    <select name="day">
      <option value="mon">Monday</option>
      <option value="wed">Wednesday</option>
      <option value="fri">Friday</option>
    </select><br />
    <textarea rows="3" cols="30">Enter your special request here</textarea><br />
    <input type="submit" value="SEND" />
    <input type="reset" value="CLEAR" />
    <input type="hidden" name="action" value="registration" />
  </form>
</body>
</html>
```
![form alt](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_SampleForm.png)

Un formulario contiene campos. Los tipos de campos incluyen:
* Text Box: producido por <input type="text">.
* Password Boc: producido por <input type="password">.
* Radio Button: producido por <input type="radio">.
* Checkbox: producido por <input type="checkbox">.
* Selection: producido por <select> y <option>.
* Text Area: producido por <textarea>.
* Submit Button: producido por <input type="submit">.
* Reset Button: producido por <input type="reset">.
* Hidden Field: producido por <input type="hidden">.
* Button: producido por <input type="button">.

Cada campo tiene un nombre y puede tomar un valor especifico. Una ves que el cliente llena los campos y presiona el botón enviar, el navegador reúne cada uno de los nombre y valores de los campos, los empaquetar en pares "name=value", y contenta todos los campos usando "&" como separador de campo. A esto se le conoce como cadena de consulta. Enviará la cadena de consulta al servidor como parte de la solicitud.
```
name1=value1&name2=value2&name3=value3&...
```
Los caracteres especiales no están permitidos en la cadena de consulta. Deben ser reemplazados por un "%" seguidos por en código ASCII en Hex. Ej., "~" es reemplazado por "%7E", "#" por "%23". Como el espacio es muy común, puede ser reemplazado ya sea por "%20" o "+" (el caracter "+" debe ser reemplazado por "%2B"). A este proceso de reemplazo se le llama URL-encoding, y el resultado es un cadena de consulta codificada URL. Por ejemplo, supongamos que hay tres campos dentro de un formulario, con nombre/valor "name=Petter Lee", "adress=#123 Happy Ave" y "lenguaje=C++", la cadena de consulta codificada URL es:
```
name=Peter+Lee&address=%23123+Happy+Ave&Language=C%2B%2B
```
Esta cadena de consulta puede ser enviada al servidor usando ya sea un método de solicitud HTTP GET o POST, el cual es especificado en el atributo "method" del <form> 
```
<form method="get|post" action="url">
```
Si el método de solicitud usado es GET, la cadena de consulta codificada URL será anexada  detrás del request-URI después de un caracter "?", ej.,
```
GET request-URI?query-string HTTP-version
(otra cabecera de solicitud opcional)
(linea en blanco)
(cuerpo de solicitud opcional)
```
Usar la solicitud GET para enviar la cadena de consulta tiene los siguientes inconvenientes:
* La cantidad de datos que debes anexar detrás del request-URI es limitada. Si la cantidad excede el umbral especifico del servidor, el servidor regresará un error "414 Request URI too Large".
* La cadena de consulta codificada URL aparecerá en la caja de dirección del navegador.
EL método POST supera estos inconvenientes. Si el método de solicitud POST es usado, la cadena de consulta será enviada en el cuerpo del mensaje de solicitud, donde la cantidad no esta limitada. Las cabeceras de solicitud  *Content-Type* y *Content-Lenght* son usadas para notificar al servidor el tipo y la longitud de la cadena de consulta. La cadena de consulta no aparecerá en la caja de dirección del navegador.
##### Ejemplo
El siguiente formulario HTML es usado para recolectar el usuario y el password en un menú de inicio de sesión.
```
<html>
<head><title>Login</title></head>
<body>
  <h2>LOGIN</h2>
  <form method="get" action="/bin/login">
    Username: <input type="text" name="user" size="25" /><br />
    Password: <input type="password" name="pw" size="10" /><br /><br />
    <input type="hidden" name="action" value="login" />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
```
![login alt](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_LoginForm.png)

EL método de solicitud GET es usado para enviar la cadena de consulta. Supongamos que el usuario introduce "Peter Lee" como el nombre de usuario, "123456" como contraseña; y da clic en el botón de enviar. La siguiente solicitad GET es:
```
GET /bin/login?user=Peter+Lee&pw=123456&action=login HTTP/1.1
Accept: image/gif, image/jpeg, */*
Referer: http://127.0.0.1:8000/login.html
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: 127.0.0.1:8000
Connection: Keep-Alive
 
```
Tener en cuenta que aunque la contraseña que introduces no se muestra en pantalla, se muestra claramente en la caja de dirección del navegador. Nunca debes enviar tu contraseña sin la encriptación apropiada.
```
http://127.0.0.1:8000/bin/login?user=Peter+Lee&pw=123456&action=login
```


### URL y URI
___
#### URL (Uniform Resource Locator)
Un URL (Localizador Uniforme de Recursos), definido en el RFC 2396, es usado para identificar de forma exclusiva un recurso a través de Internet. URL tiene la siguiente sintaxis:
```
protocol://hostname:port/path-and-file-name
```
Hay 4 partes en un URL:
1. Protocolo: El protocolo de nivel de aplicación usado por el servidor, ej., HTTP, FTP y telnet.
2. Hostname: En nombre de dominio DNS (ej., www.nowhere123.com) o dirección IP (ej., 192.128.1.2) del servidor.
3. Port: El numero de puerto TCP que el el servidor tiene abierto para las solicitudes entrantes de los clientes.
4. Path-and-name-file: El nombre y localización del recurso solicitado, bajo el directorio de documentos base del servidor.

Por ejemplo, en el URL *http://www.nowhere123.com/docs/index.html*, el protocolo de comunicación es HTTP; el nombre del host es www.nowhere123.com. EL numero del puerto no esta especificado en el URL, y toma el puerto por defecto, el cual es el punto TCP 80 para HTTP [STD2]. La ruta y el nombre del archivo es "/docs/index.html"

Otros ejemplos de URL son:
```
ftp://www.ftp.org/docs/test.txt
mailto:user@test101.com
news:soc.culture.Singapore
telnet://www.nowhere123.com/
```

#### URL Codificado
Un URL no puede contener caracteres especiales, tales como espacios o '~'. Los caracteres especiales están codificados, en la forma %xx, donde xx es el dodigo ASCII Hex. Por ejemplo, '~' es codificado como *%7e*; '+' es codificado como *%2b*. Un espacio puede ser codificado como *%20* o '+'. Después de codificar el URL se le llama URL codificado.


### URI (Uniform Resource Identifier)
URI (Identificador Uniforme de Recursos), definido en FRC3986, es mas general que URL, el cual puede incluso localizar un fragmento dentro de un recurso. La sintaxis del URI para el protocolo HTTP es
```
http://host:port/path?request-parameters#nameAnchor
```
* Los parámetros de solicitud , en forma de pares de nombre=valor, son separador por el URL por un '?'. Los pares nombre=valor son separados por '&'
* El *nameAnchor* identifica un fragmento dentro del documento HTML, definido por la etiqueta de ancla *<a name="anchorName">...</a>*.
* Reescritura de URL para la gestión de sesiones, ej., "...;sesionID=xxxxxx".


### Metodo de solicitud "POST"
___
EL método de solicitud POST es usado para "postear" datos adicionales en el servidor (ej., enviar un datos de un formulario HTML o subir un archivo). Emitiendo un URL HTTP desde el navegador siempre genera una solicitud GER. Para generar una solicitud  POST, puedes usar un formulario HTML con el atributo *method="post"* o escribir tu propio programa de red. Para enviar datos de un formulario HTML, la solicitud POST es la misma que la solicitud GET excepto que la cadena de consulta codificada URL en enviada en el cuerpo de la solicitud, en ligar de anexada en el request-URI.

La solicitud POSR tiene la siguiente sintaxis:
```
POST request-URI HTTP-version
Content-Type: mime-type
Content-Length: number-of-bytes
(Otras cabeceras de solicitud opcionales)
  
(URL-encoded query string)
```
Las cabeceras de solicitud *Content-Type* y *Content-Length* son necesarias en la solicitud POST para informar al servidor el tipo de medios y la longitud del cuerpo de la solicitud.

#### Ejemplo: Enviando datos de Formulario usando el método de solicitud POST.
Usamos el mismo script HTML de arriba, pero cambiando el tipo de solicitud a POST.
```
<html>
<head><title>Login</title></head>
<body>
  <h2>LOGIN</h2>
  <form method="post" action="/bin/login">
    Username: <input type="text" name="user" size="25" /><br />
    Password: <input type="password" name="pw" size="10" /><br /><br />
    <input type="hidden" name="action" value="login" />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
```
Supongamos que el usuario ingresa "Peter Lee" como nombre de usuario, y "123456" como contraseña, y da clic al botón enviar, la siguiente solicitud post será generada por el navegador:
```
POST /bin/login HTTP/1.1
Host: 127.0.0.1:8000
Accept: image/gif, image/jpeg, */*
Referer: http://127.0.0.1:8000/login.html
Accept-Language: en-us
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Content-Length: 37
Connection: Keep-Alive
Cache-Control: no-cache
   
User=Peter+Lee&pw=123456&action=login
```
Tener en cuenta que la cabecera *Content-Type* informa al servidor que los datos son un URL codificado (con un MIME type especial *applocation/x-www-form-urlencoded*), y la cabecera *Content-Length* indica el servidor cuantos bytes leer del cuerpo del mensaje.

#### POST vs GET para enviar Datos de Formulario
Como se menciono el la sección previa, la solicitud POST tiene ventaja comparada con la  solicitud GET al enviar la cadena de consulta:
* La cantidad de data que puede ser publicada es ilimitada, al ser mantenida el el cuerpo de la solicitud, el cual se enviar a menudo al servidor en un flujo de datos independiente.
* La cadena de consulta no se muestra en la caja de dirección del navegador.

Tener en cuenta que el password no se muestra en la caja de dirección del navegador, es transmitido al servidor en texto limpio, y sometido a espionaje de red. Por lo tanto, enviar un password usando una solicitud POST no es seguro.


### Subiendo un archivo usando una solicitud POST con multiples partes de un formulario de datos
___
"RFC 1867: Subida de archivos basado en formularios en HTML" especifica como se puede subir un archivo a un servidor usando una solicitud POST desde un formulario HTML. Un nuevo atributo *type="file"* fue agregado a la etiqueta *<imput>*  del *<form>* HTML para soportar la subida de archivos. Los datos POST de carga de archivos no son URL encriptados (en el estándar *application/x-www-form-urlencoded*), pero usa un nuevo  MIME type *multipart/form-data*.

#### Ejemplo
El siguiente formulario HTML puede ser usado para la carga de archivos:
```
<html>
<head><title>File Upload</title></head>
<body>
  <h2>Upload File</h2>
  <form method="post" enctype="multipart/form-data" action="servlet/UploadServlet">
    Who are you: <input type="text" name="username" /><br />
    Choose the file to upload:
    <input type="file" name="fileID" /><br />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
```
![upload alt](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_FileUploadForm.png)

Cuando el navegador encuentra una etiqueta *<input>* con el atributo *<type="file">*,  este muestra un caja de texto con un botón "browse...", para permitir al usuario elegir el archivo que será subido.

Cuando el usuario da clic en el botón de enviar, el navegador enviar los datos del formulario el el contenido de los archivos seleccionados. El viejo tipo de codificado "*application/x-www-form-urlencoded*" es ineficiente para enviar datos binarios y caracteres no ASCII. Un nuevo tipo de medio "*multipart-gorm-data*" es usado.

Cada parte identifica el nombre de entrada dentro de el formulario HTML original, y en tipo de contenido si el medio es conocido, o como *application/octet-stream* de otra manera.

El nombre original del archivo local puede ser entregado como un parámetro "*filename*", o en la cabecera *Disposition: form-data*.

Un ejemplo de un mensaje POST para una carga de archivo es la siguiente:
```
POST /bin/upload HTTP/1.1
Host: test101
Accept: image/gif, image/jpeg, */*
Accept-Language: en-us
Content-Type: multipart/form-data; boundary=---------------------------7d41b838504d8
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Content-Length: 342
Connection: Keep-Alive
Cache-Control: no-cache
   
-----------------------------7d41b838504d8 Content-Disposition: form-data; name="username" 
Peter Lee
-----------------------------7d41b838504d8 Content-Disposition: form-data; name="fileID"; filename="C:\temp.html" Content-Type: text/plain 
<h1>Home page on main server</h1> 
-----------------------------7d41b838504d8--
```
Selvet 3.0 proporciona soporte integrado para el procesamiento de carga de archivos. Leer "[Uploading Files in Servlet 3.0](https://www.ntu.edu.sg/home/ehchua/programming/java/JavaServletCaseStudyPart2.html#FileUpload)"

### Metodo de Solicitud "CONNECT"
___
La solicitud CONNECT HTTP es usada para parir al proxy crear una conexión a otro host y simplemente retransmitir el contenido, en lugar de tratar de analizar o guardar el mensaje en la caché. Esto a menudo se utiliza para realizar una conexión a través de un proxy.

### Otros métodos de solicitud
___
PUT: Pedir al servidor que almacene datos.

DELETE: Pedir al servidor que elimine datos.

Por motivos de seguridad, PUT and DELETE no están soportados por la mayoría de los servidores de producción.

Métodos de extensión (también códigos de error y cabeceras) pueden ser definidos para extender la funcionalidad del protocolo HTTP.

### Negociación de contenido
___
Como ya mencionamos, HTTP soporta la negociación de contenido entre el cliente y servidor. Un cliente puede usar cabeceras de solicitud adicionales (tales como *Acept, Accept-Lenguage, Accept-Charset, Accept-Encoding*) para indicar al servidor que es lo que soporta o cuales son sus preferencias.Si el servidor posee múltiples versiones del mismo archivo en diferentes formatos, este regresara el formato que el cliente prefiere. Este proceso es llamado negociación de contenido.


### Negociación de Tipo de Contenido
El servidor usa un archivo de configuración MIME (llamado "*conf/mime.types*") para capear la extensión del archivo y el tipo de medios, para que pueda identificar el tipo de archivo examinado la extensión del archivo. Por ejemplo, extensiones de archivo "*.htm*", "*.html*" son asociados con el tipo de medios MIME "*text/html*", extensiones de archivo "*.jpg*", "*.jpeg*" son asociadas con "*image/jpeg*". Cuando un archivo es regresado al cliente, el servidor agrega una cabecera de respuesta *Content-Type* para informar al cliente el tipo de medios de los datos.

Para la negociación de tipo de contenido, supongamos que el cliente pide el archivo llamado "*logo*" sin especificar el tipo, y envía la cabecera "*Accept: image/gif, image/jpeg,...*" Si el servidor tiene dos formados de "*logo*": "*logo.gif*" y "*logo.jpg*" y la configuración MIME tiene las siguientes entradas:
```
image/gif        gif
image/jpeg       jpeg jpg jpe
```
El servidor regresará "*logo.gif*" al cliente, basado en la cabecera *Accept* del cliente, el el mareo de archivo MIME type. El servidor incluirá una cabecera "*Content-type: image/gif*" en su respuesta.

Se muestra el seguimiento del mensaje:
```
GET /logo HTTP/1.1
Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg,
  application/x-shockwave-flash, application/vnd.ms-excel, 
  application/vnd.ms-powerpoint, application/msword, */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: test101:8080
Connection: Keep-Alive
(blank line)
```
```
HTTP/1.1 200 OK
Date: Sun, 29 Feb 2004 01:42:22 GMT
Server: Apache/1.3.29 (Win32)
Content-Location: logo.gif
Vary: negotiate,accept
TCN: choice
Last-Modified: Wed, 21 Feb 1996 19:45:52 GMT
ETag: "0-916-312b7670;404142de"
Accept-Ranges: bytes
Content-Length: 2326
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: image/gif
(blank line)
(body omitted)
```
Sin embargo, si el servidor tiene 3 archivos "*logo*", "*logo.gif*", "*logo.html*", "*logo.html*" y "*Accept:* * / *" fue usado:
```
GET /logo HTTP/1.1
Accept: */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: test101:8080
Connection: Keep-Alive
(blank line)
```
```
HTTP/1.1 200 OK
Date: Sun, 29 Feb 2004 01:48:16 GMT
Server: Apache/1.3.29 (Win32)
Content-Location: logo.html
Vary: negotiate,accept
TCN: choice
Last-Modified: Fri, 20 Feb 2004 04:31:17 GMT
ETag: "0-10-40358d95;404144c1"
Accept-Ranges: bytes
Content-Length: 16
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: text/html
(blank line)
(body omitted)
```
```
Accept: * / *
```
Las siguientes directivas de configuración de Apache son relevantes para la negociación de tipo de contenido:
* La directiva *TypeConfig* puede ser usada para especificar la locación del mapeo de archivos MIME:
  ```
  TypeConfig conf/mime.types
  ```
* La directiva *AddType* puede ser usada para incluir metro de MIME type adicionales en el archivo de configuración:
  ```
  AddType mime-type extension1 [extension2]
  ```
* La directiva *DefaultType* da el MIME type de una extensión de archivo desconocida (en la cabecera *Content-Type*)
  ```
  DefaultType text/plain
  ```


### Negociación de Lenguaje y "Opciones de MultiView"

La directiva "*Options MultiView*" es la manera mas simple de imperar negociación de lenguajes.
Por ejemplo:
```
AddLanguage en .en
<Directory "C:/_javabin/Apache1.3.29/htdocs">
    Options Indexes MultiViews
</Directory>
```
Supongamos que el cliente solicita "index.html" y envia un "*Accept-Lenguage: en-us*". Si el servidor tiene "*test.html*", "*text.html.cn*", basado en las preferencias del cliente, se regresara "*text.html.en*". ("*en*" incluye "*en-us*".)

El mensaje de seguimiento es el siguiente:
```
GET /index.html HTTP/1.1
Accept: */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: test101:8080
Connection: Keep-Alive
(blank line)
```
```
HTTP/1.1 200 OK
Date: Sun, 29 Feb 2004 02:08:29 GMT
Server: Apache/1.3.29 (Win32)
Content-Location: index.html.en
Vary: negotiate
TCN: choice
Last-Modified: Sun, 29 Feb 2004 02:07:45 GMT
ETag: "0-13-40414971;40414964"
Accept-Ranges: bytes
Content-Length: 19
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: text/html
Content-Language: en
(blank line)
(body omitted)
```
La directiva *AddLenguage* es necesaria para asociar un código de lenguaje con una extensión de archivo, similar al mapeo de archivos MIME type.

Tener en cuenta que la directiva "*Options All*" no incluye la opción "MultiViews". Es decir, hay que encender de forma especifica la MultiViews.

La directiva *LenguagePriority* puede ser usada para especificar la preferencia de lenguaje en caso de un empate durante la negociación de contenido o que el cliente no exprese una preferencia. Por ejemplo:
```
<IfModule mod_negotiation.c>
   LanguagePriority en da nl et fr de el it ja kr no pl pt pt-br
</IfModule>
```


### Negociación de conjunto de Caracteres
Un cliente puede usar la cabecera de solicitud *Accept-Charset* para negociar con el servidor el tipo de conjunto de caracteres que prefiere.
```
Accept-Charset: charset-1, charset-2, ...
```
Los tipos de conjuntos de caracteres comúnmente encontrados incluyen: ISO-8859-1 (Latin-I), ISO-8859-2, ISO-8859-5, BIG5 (Chinese Traditional), GB2312 (Chinese Simplified), UCS2 (2-byte Unicode), UCS4 (4-byte Unicode), UTF8 (Encoded Unicode), y etc.

Del mismo modo, la directiva *AddCharset* se utiliza para asociar la extendió de archivo con el conjunto de caracteres. Por ejemplo:
```
AddCharset ISO-8859-8   .iso8859-8
AddCharset ISO-2022-JP  .jis
AddCharset Big5         .Big5  .big5
AddCharset WINDOWS-1251 .cp-1251
AddCharset CP866        .cp866
AddCharset ISO-8859-5   .iso-ru
AddCharset KOI8-R       .koi8-r
AddCharset UCS-2        .ucs2
AddCharset UCS-4        .ucs4
AddCharset UTF-8        .utf8
```


### Negociación de Codificado
Un cliente puede usar la cabecera *Accept-Encoding* para informar al servidor el tipo de codificación que soporta. Los esquemas de codificación comunes son: "*x-gzip (.gz, .tgz)*" y "*x-compress (.Z)*".
```
Accept-Encoding: encoding-method-1, encoding-method-2, ...
```
Del mismo modo, la directiva *AddEncoding* es usada para asociar la extensión de archivo con el esquema de codificación. Por ejemplo:
```
AddEncoding x-compress  .Z
AddEncoding x-gzip      .gz .tgz
```

###Conexiones Persistentes (o Keep-Alive)
En HTTP/1.0, el servidor cierra la conexión TCP después de entregar la respuesta por defecto (*Connection: Close*). Es decir, cada conexión TCP sirve solo una solicitud. Esto no es eficiente ya que muchas paginas HTML contienen hyperlinks (vía etiquetas *<a href="url">*) a otros recursos (tales como imágenes, scripts - ya sea locales o de un servidor remoto). Si descargas una pagina con 5 imágenes, el navegador tiene que establecer una conexión TCP 6 veces con el mismo servidor.

El cliente puede negociar con el servidor para pedir que no cierre la conexión después de entregar la respuesta, para que otras solicitudes puedan ser enviadas a través de la misma conexión. A esto se le conoce como conexión persistente (o conexión keep-alive). Las conexiones persistentes han mejorado la eficiencia de la red. Para HTTP/1.0, la conexión por defecto no es persistente. Para pedir una conexión persistente, el cliente debe incluir una cabecera de solicitud "*Connection: Keep-Alive*" en el mensaje de solicitud para negociar con el servidor.

Para HTTP/1.0, la conexión por defecto es persistente. El cliente no tiene que enviar la cabecera "*Connection: Keep-Alive*". En su lugar, el cliente puede si lo desea, enviar la cabecera *Connection: Close*" para pedir al servidor cerrar la conexión después de enviar la respuesta.

La conexión persistente es extremadamente útil par paginas web con muchas imágenes pequeñas y otros datos asociados, todos pueden ser descargados usando la misma conexión. Los beneficios de una conexión persistente son:
* Ahorro de recursos y tiempo del CPU al abrir y cerrar una conexión TCP con el cliente, proxy, gateways, o el servidor de origen.
* Las solicitudes pueden ser "pipermines". Es decir, un cliente puede hacer varias solicitudes sin esperar por cada respuesta, para que en uso de la red sea mas eficiente.
* Respuesta mas rapada al no necesitar tiempo para realizar una apetura de conexión TCP.

En el servidor Apache HTTP, varias directivas de configuraciones están relacionadas a la conexión persistente: 

La directiva *KeepAlive* decide si admite soportar conexiones persistentes. Este toma un valor ya sea On o Off.
```
KeepAlive On|Off
```
La directiva *MaxKeepAliveRequest* establece el numero marino de solicitudes que pueden ser enviadas a través de una conexión persistente. Puedes establecer en 0 para permitir solicitudes ilimitadas. Es recomendado establecer un gran numero para un mejor desempeño y eficiencia de red.
```
MaxKeepAliveRequests 200
```
La directiva *KeepAliveTimeOut* establece el tiempo de espera en segundos que una conexión persistente espera por la siguiente solicitud.
```
KeepAliveTimeout 10
```


### Rango de descarga
___
```
Accept-Ranges: bytes
Transfer-Encoding: chunked
```


### Control de Caché
___
El cliente puede enviar una cabecera de solicitud "*Cache-Control: no-cache*" para indicar al proxy que obtenga una copia reciente desde el servidor de origen, aun si hay una copia en la caché local. Desafortunadamente, Los servidores HTTP/1.0 no entienden esta cabecera, pero usan una cabecera de solicitud vieja "*Pragma: no-cache*". Puedes incluir ambas cabeceras a tu solicitud.
```
Pragma: no-cache
Cache-Control: no-cache
```
___

### Referencias y Recursos
* W3C HTTP specifications at http://www.w3.org/standards/techs/http.
* RFC 2616 "Hypertext Transfer Protocol HTTP/1.1", 1999 @ http://www.ietf.org/rfc/rfc2616.txt.
* RFC 1945 "Hypertext Transfer Protocol HTTP/1.0", 1996 @ http://www.ietf.org/rfc/rfc1945.txt.
* STD 2: "Assigned numbers", 1994.
* STD 5: "Internet Protocol (IP)", 1981.
* STD 6: "User Datagram Protocol (UDP)", 1980.
* STD 7: "Transmission Control Protocol (TCP)", 1983.
* RFC 2396: "Uniform Resource Identifiers (URI): Generic Syntax", 1998.
* RFC 2045: "Multipurpose Internet Mail Extension (MIME) Part 1: Format of Internet Message Bodies", 1996.
* RFC 1867: "Form-based File upload in HTML", 1995, (obsoleted by RFC2854).
* RFC 2854: "The text/html media type", 2000.
* Mutlipart Servlet for file upload @ www.servlets.com


___

#### Fuente original: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/HTTP_Basics.html

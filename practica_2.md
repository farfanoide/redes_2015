Capa de Aplicación - Redes y comunicaciones ­ 2015
==================================================

Práctica 2 - Capa de Aplicación
-------------------------------

1. ¿Cuál es la función de la capa de aplicación?

  > La capa de aplicación da soporte a las aplicaciones de red; incluye los
  > protocolos HTTP (Web), SMTP (email) y FTP (transferencias de archivos)
  > entre otros.

2. Si dos procesos deben comunicarse:

  1. ¿Cómo podrían comunicarse si están en diferentes máquinas?

    > Utilizan el intercambio de mensajes a través de la red. El proceso emisor
    > crea y envía los mensajes, y el receptor los recibe y responde si es
    > apropiado hacerlo. Los protocolos de la capa de aplicación definirán el
    > formato y orden en que deben enviarse esos mensajes, y las acciones a
    > tomar en consecuencia a la llegada de un mensaje.

  2. ¿Y si están en la misma máquina qué alternativas existen?

    > Utilizan las facilidades de comunicación inter-proceso que soporte el SO
    > huésped (uso de señales, memoria compartida...).

3. Explique brevemente cómo es el modelo Cliente/Servidor. De un ejemplo de un
   sistema Cliente/Servidor en la "vida cotidiana" y un ejemplo de un sistema
   informático que siga el modelo Cliente/Servidor. ¿Conoce algún otro modelo
   de comunicación?

  > En la arquitectura Cliente-Servidor un host cliente se comunica con otro,
  > servidor, enviando solicitudes. Los clientes se comunican sólo con el
  > servidor -no entre ellos-, y posiblemente desde IP dinámica -al contrario
  > del servidor, con IP fija-. Es común que un host actúe como cliente y
  > servidor de un servicio, o que haya solicitudes y envío de información en
  > ambas direcciones; en este caso, se denomina cliente al host que comienza
  > la sesión. Ejemplo: Un servidor Web -i.e. Apache- y un browser -i.e.
  > Mozilla Firefox-. Otros modelos de comunicación son: P2P (Peer to Peer, los
  > clientes se comunican entre ellos directamente y posiblemente con un
  > servidor que administra las IP de los clientes conectados) y sistemas
  > híbridos (un servidor coordina algunas tareas y adminsitra las IP cliente,
  > y los clientes se comunican entre ellos tras interactuar con el servidor).

4. Describa la funcionalidad de la entidad genérica "Agente de usuario" o "User
   agent".

  > Un user agent es la interfaz entre el usuario final y una aplicación de red
  > (por ejemplo, el browser en el caso de la WEB). Implementa la parte cliente
  > de algunos protocolos de aplicación. 

DNS
---

Requerimientos:


Debe usar el Live CD de Lihuen GNU/Linux provisto. Ver URL de descarga en el
sitio de la cátedra en https://catedras.info.unlp.edu.ar/

La forma recomendable de usar la ISO armando una maquina virtual con VirtualBox
con:

  - Placa de red en modo NAT
  - Verifique que el CD de la máquina virtual referencie el archivo ISO de
    Lihuen LiveCD.

5. Investigue y describa cómo funciona el DNS. ¿Cuál es su objetivo?

  > Un DNS es una base de datos distribuida implementada en una jerarquía de
  > servidores de nombres, y un protocolo de nivel de aplicación que permite a
  > los hosts y dichos servidores comunicarse para proveer el servicio de
  > traducción entre la dirección mnemónica y la dirección IP. Cuando una
  > aplicación precisa traducir una dirección mnemónica a IP, el host invocará
  > un mensaje hacia el cliente DNS con el nombre a traducir. El cliente envía
  > un mensaje de petición a través de la red, y luego de un retardo recibe la
  > dirección de IP enviada por el servidor DNS.

6. ¿Qué es un root server? ¿Qué es un generic top-level domain (gtld)?

  > Los servidores DNS se organizan en forma jerárquica. Un host hace su
  > solicitud a un servidor local de nombres que, si no posee la traducción, se
  > transforma en un cliente consultando a un servidor raíz de nombres -root
  > server-. Si el root server conoce al servidor autorizado de nombres para el
  > dominio que se intenta resolver, envía la solicitud terminando la cadena;
  > si lo desconoce, consulta a servidores intermedios hasta que eventualmente
  > alguno lo conozca. En cada paso, un servidor podría tener registrado el IP
  > del dominio consultado o mantenerlo en cache por una consulta anterior,
  > ofreciendo una respuesta directa. 

  > Para un nombre de dominio, se denomina Top Level Domain (TLD) a la etiqueta
  > más a la derecha, desde el último punto. Un generic top-level domain es una
  > clasificación de los dominios de Internet, -un subconjunto de los TLD's-
  > que actualmente incluye sólo las terminaciones: .com, .info, .net y .org.
  > Otras clasificaciones mantienen por ejemplo códigos por país o
  > administrados por distintas organizaciones.

7. ¿Qué es una respuesta del tipo authoritative?

  > Una respuesta authoritative es aquella entregada por el servidor oficial
  > para el nombre de dominio consultado -es decir, que ningún servidor local,
  > raíz ni intermedio respondió con información de caché-. 

8. ¿Qué diferencia una consulta DNS recursiva de una iterativa?

  - Consulta DNS Recursiva: Un host realiza una consulta a un servidor, éste se
    encarga de obtener la resolución de IP y devuelve la respuesta al host. 

  - Consulta DNS Iterativa: Un name server realiza una consulta a un servidor;
    si este no tiene la respuesta le devuelve la IP del próximo servidor. El
    name server original se encarga de realizar nuevas solicitudes hasta
    obtener la respuesta.

  Típicamente, un local name server realiza consultas iterativas, y el resto
  recursivas -ya que tienen mayor volúmen de consultas que el local name
  server-. 

9. ¿Qué es el resolver?

  > Se denomina resolver a la parte cliente del DNS, encargada de iniciar y
  > secuenciar las consultas. Usualmente trabajan de modo iterativo, aunque
  > algunos sólo se conectan a un name server único y trabajan con consultas
  > recursivas. 

10. Describa para que se usan los siguientes tipos de registros de DNS:

  > Los name servers mantienen registros de recursos (RR) con el mapeo hostname
  > <=> IP, en una cuádrupla (name, value, type, TTL). Las respuestas a
  > consultas incluyen uno o varios RR de distintos tipos. El campo TTL -Time
  > To Live- indica cuánto tiempo mantener el RR en caché.

  - A: El campo name es un hostname, value su IP. Es el único que traduce
    hostname <=> IP, y representa al nombre canónico (cualquier otro nombre
    para el hosts será un alias con RR tipo CNAME). Puede haber más de un
    registro tipo A con igual hostname y distintas IP en el caso de servidores
    replicados para realizar un balance de carga: la respuestas DNS incluirán
    la lista de asociaciones pero el servidor irá alternando las posiciones
    para distribuir los accesos de los clientes. 

  - PTR: (Pointer Record). Exactamente al revés que un registro tipo A, indica
    en `name` el IP de un host y en `value` su hostname. Permiten la resolución
    reversa.

  - NS: El campo name es un hostname, value el hostname de un name server a
    quien seguir consultando. Permite continuar las consultas hasta obtener la
    traducción definitiva.

  - MX: (Mail eXchange Record). El campo name es un alias para un mail server,
    value incluye un valor numérico que indica la prioridad y el hostname del
    mail server. Permite que los hosts del mail server tengan una dirección mas
    simple a través del alias. Si un programa desea enviar un correo a un host
    de ese dominio, debe intentar primero con el de menor valor de prioridad
    -prioridad más alta- y sólo si falla intentar con el resto.

  - SOA: Por Start of Authority, indica que los registros siguientes de la base
    de datos corresponden a información autoritativa. Indica: nombre canónico
    del NS, usuario responsable -dirección de email con un punto en vez del
    arroba-, número de versión -serial- del archivo de configuración del NS,
    refresh o tiempo de espera de servidores secundarios para pedir el SOA al
    primario, expire o tiempo en segundos que tardarán los servidores
    secundarios en descartar los datos si no logran contactar al primario, y el
    mínimo valor TTL para los registros de recursos siguientes

  - CNAME (Canonical Name Record): El campo name es un alias para un hostname,
    value el nombre canónico o real del mismo (por ejemplo, el uso de alias
    permite que un sitio sea accedido como www.sitio.com y como sitio.com
    -alias-).


11. Utilizando el Live CD, utilice alguno de los siguientes comandos: nslookup,
    host o dig, para obtener:

  1. La dirección de Internet del host www.redes.unlp.edu.ar

    ```bash
    host www.redes.unlp.edu.ar
    ```
    ```
    #=> www.redes.unlp.edu.ar has address: 127.0.0.1
    ```

  2. La dirección de Internet o el hostname del servidor de DNS del dominio
     redes.unlp.edu.ar

    ```bash
    dig www.redes.unlp.edu.ar -t NS
    ```
    ```
    ;; SERVER: 127.0.0.1#53
    ```

  3. La dirección de Internet o el hostname del servidor de correo del dominio
     redes.unlp.edu.ar

    ```bash
    dig www.redes.unlp.edu.ar -t MX
    ```
    ```
    ;; SERVER: 127.0.0.1#53
    ```

12. Para realizar el siguiente ejercicio va a necesitar que el LiveCD tenga
    Internet. También puede realizarlo desde una PC que tenga los comandos y
    conexión a Internet.
    Realice consultas de DNS para averiguar, ya sea con el comando dig, host o
    nslookup los siguientes datos:

  1. La cantidad de servidores de mail que aceptan correo para el dominio
     gmail.com:

  ```bash
  dig gmail.com -t MX
  ```
  ```
  ; <<>> DiG 9.8.3-P1 <<>> gmail.com MX
  ;; global options: +cmd
  ;; Got answer:
  ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 5893
  ;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 5

  ;; QUESTION SECTION:
  ;gmail.com.     IN  MX

  ;; ANSWER SECTION:
  gmail.com.    791 IN  MX  20 alt2.gmail-smtp-in.l.google.com.
  gmail.com.    791 IN  MX  5  gmail-smtp-in.l.google.com.
  gmail.com.    791 IN  MX  40 alt4.gmail-smtp-in.l.google.com.
  gmail.com.    791 IN  MX  10 alt1.gmail-smtp-in.l.google.com.
  gmail.com.    791 IN  MX  30 alt3.gmail-smtp-in.l.google.com.

  ;; ADDITIONAL SECTION:
  alt1.gmail-smtp-in.l.google.com. 191 IN A 74.125.206.26
  alt3.gmail-smtp-in.l.google.com. 235 IN A 74.125.205.27
  alt2.gmail-smtp-in.l.google.com. 260 IN A 74.125.136.26
  gmail-smtp-in.l.google.com. 116 IN  A 64.233.186.26
  alt4.gmail-smtp-in.l.google.com. 181 IN A 74.125.200.27

  ;; Query time: 170 msec
  ;; SERVER: 192.168.43.1#53(192.168.43.1)
  ;; WHEN: Thu Mar 26 20:24:44 2015
  ;; MSG SIZE  rcvd: 230
  ```

  2. El nombre del servidor de correo principal de gmail.com.

  > gmail-smtp-in.l.google.com

  3. ¿En que ocasión los demás servidores de correo recibirían correos
     dirigidos al dominio gmail.com?  ¿que sucede luego de que uno de estos
     servidores recibe un correo para un usuario del dominio, gmail.com en este
     caso?

    > Los servidores alternativos o secundarios recibiran correos en caso de
    > que los servidores con mayor autoridad no puedan responder

  4. La cantidad de servidores de DNS del dominio unlp.edu.ar:

    ```bash
    dig unlp.edu.ar -t NS
    ```

    ```
    ; <<>> DiG 9.8.3-P1 <<>> unlp.edu.ar -t NS
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 26885
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

    ;; QUESTION SECTION:
    ;unlp.edu.ar.     IN  NS

    ;; ANSWER SECTION:
    unlp.edu.ar.    86400 IN  NS  ns1.riu.edu.ar.
    unlp.edu.ar.    86400 IN  NS  unlp.unlp.edu.ar.
    unlp.edu.ar.    86400 IN  NS  anubis.unlp.edu.ar.

    ;; ADDITIONAL SECTION:
    unlp.unlp.edu.ar. 85768 IN  A 163.10.0.67

    ;; Query time: 77 msec
    ;; SERVER: 192.168.43.1#53(192.168.43.1)
    ;; WHEN: Thu Mar 26 20:42:55 2015
    ;; MSG SIZE  rcvd: 107
    ```

  5. La dirección de Internet del host www.info.unlp.edu.ar

    ```bash
    host www.info.unlp.edu.ar
    ```
    ```
    #=> www.info.unlp.edu.ar has address 163.10.5.91
    ```

13. ¿Qué función cumple en Linux/Unix el archivo /etc/hosts o en Windows el
    archivo \WINDOWS\system32\drivers\etc\hosts?

    > El archivo hosts de un ordenador es usado por el sistema operativo para
    > guardar la correspondencia entre dominios de Internet y direcciones IP.
    > Este es uno de los diferentes métodos que usa el sistema operativo para
    > resolver nombres de dominios. Antiguamente cuando no había servidores DNS
    > que resolvieran los dominios, el archivo hosts era el único encargado de
    > hacerlo, pero dejó de utilizarse cuando Internet empezó a crecer en
    > nombres de dominio, pasando a usar servidores de resolución de DNS. En
    > muchos sistemas operativos este método es usado preferentemente respecto
    > a otros como el DNS. En la actualidad también es usado para bloquear
    > contenidos de Internet como la publicidad web.  El archivo hosts es un
    > archivo de texto plano que puede ser editado por el administrador del
    > equipo. Este archivo es tradicionalmente llamado "hosts" y su ubicación
    > depende del sistema operativo.

14. Abra el programa Wireshark (como root) para comenzar a capturar el tráfico
    de red en la interfaz de loopback lo. Una vez abierto realice una consulta
    DNS con el comando dig para averiguar el registro MX de redes.unlp.edu.ar y
    luego otra para averiguar los registros NS correspondientes a el dominio
    redes.unlp.edu.ar. Analice la información proporcionada por dig y comparelo
    con la captura.

15. Dada la siguiente situación: "Una PC en una red determinada, con acceso a
    Internet, utiliza los servicios de DNS de un servidor de la red". Analice:

  1. ¿Qué tipo de consultas (iterativas o recursivas) realiza la PC a su
     servidor de DNS?

  2. ¿Qué tipo de consultas (iterativas o recursivas) realiza el servidor de
     DNS para resolver requerimientos de usuario como el anterior? ¿A quién le
     realiza estas consultas?

HTTP
----

16. Defina cada una de las siguientes entidades: Navegador, Servidor WEB,
    Página WEB, HTTP y URL.  ¿Cómo participa cada uno de ellas en la
    comunicación cliente WEB ­ servidor WEB?

  - Navegador:

    > Es una aplicación que opera a través de Internet, interpretando la
    > información de archivos y sitios web para que podamos ser capaces de
    > leerla, (ya se encuentre ésta alojada en un servidor dentro de la World
    > Wide Web o en un servidor local).  Es la aplicación en el host cliente que
    > pide los objetos al host servidor.

  - Servidor web:

    > Almacena documentos HTML, imágenes, archivos de texto, escrituras, y demás
    > material Web compuesto por datos (conocidos colectivamente como contenido),
    > y distribuye este contenido a clientes que la piden en la red. Es donde se
    > almacenan los objetos que piden los hosts clientes.

  - Página web:

    > Documento o información electrónica adaptada para la World Wide Web y que
    > puede ser accedida mediante un navegador para mostrarse en un monitor de
    > computadora o dispositivo móvil. Es almacenada en el servidor y transferida
    > hacia el cliente.

  - HTTP (Hypertext Transfer Protocol):

    > Es el protocolo usado en cada transacción de la World Wide Web. Es un
    > protocolo orientado a transacciones y sigue el esquema petición-respuesta
    > entre un cliente y un servidor.

  - URL (Uniform Resource Locator):

    > Es una secuencia de caracteres, de acuerdo a un formato modélico y
    > estándar, que usa para nombrar recursos en Internet para su localización o
    > identificación, como por ejemplo documentos textuales, imágenes, vídeos,
    > presentaciones, presentaciones digitales, etc.

17. ¿Qué son y en qué se diferencian HTML y HTTP?

  > HTML es el lenguaje de marcado predominante para la elaboración de páginas
  > web. Es usado para describir la estructura y el contenido en forma de
  > texto, así como para complementar el texto con objetos tales como imágenes.
  > Como se explicó en el punto anterior HTTP es un protocolo.
  > HTML y HTTP son cosas diferentes, uno es un lenguaje que define un formato
  > y el otro es un protocolo de transferencia de objetos. HTTP puede usarse
  > para transferir archivos HTML así como otros tipos de archivos como
  > multimedia o texto. HTML puede ser transferido por otros protocolos además
  > de HTTP, pero en el caso de la web este es el protocolo utilizado.

18. Utilizando el Live CD, abra un navegador (Iceweasel). Utilizando el
    analizador de paquetes Wireshark (as root) capture los paquetes HTTP
    enviados y recibidos teniendo en cuenta:

  ```

  Nota 1: capture los paquetes utilizando la interfaz de loopback lo. (Menú
  "Capture -> Options". Luego seleccione la interfaz lo y presione Start)

  Nota 2: Para que el analizador de red sólo nos muestre los mensajes del
  protocolo http introduciremos la cadena `http' (sin las comillas) en la
  ventana de especificación de filtros de visualización (display-filter). Si no
  hiciéramos ésto veríamos todo el tráfico de red que es capaz de capturar
  nuestra placa de red, lo en este caso. De los paquetes que son capturados,
  aquel que esté seleccionado será mostrado en forma detallada en la sección
  que está justo debajo. Como sólo estamos interesados en http ocultaremos toda
  la información que no es relevante para esta práctica (Información de trama,
  Ethernet, IP y TCP). Desplegar la información correspondiente al protocolo
  HTTP bajo la leyenda "Hipertext Transfer Protocol"

  Nota 3: Para borrar la cache del navegador, deberá ir al menú "Herramientas->
  Borrar historial reciente". Alternativamente puede utilizar Ctrl+F5 en el
  navegador para forzar la petición HTTP evitando el uso de cache del
  navegador.

  Nota 4: En caso de querer ver de forma simplificada el contenido de una
  comunicación http, utilice el botón derecho sobre un paquete HTTP
  perteneciente al flujo capturado y seleccione la opción Follow TCP Stream.

  - Borrar la cache del navegador y luego, con la captura activada, visitar la
  - URL: www.redes.unlp.edu.ar. Luego de un instante refresque la página
  - utilizando F5 o el icono para recargar la misma.

  ```


  1. ¿Cuántos requerimientos realizó el navegador? Para cada par de
     requerimiento/respuesta responda:

    - ¿Qué versión de http emplea tu navegador?

        > Request Version: HTTP/1.1

    - ¿Qué versión de http ejecuta el servidor?

        > Response: HTTP/1.1

    - ¿Qué idiomas indica tu navegador al servidor que está dispuesto aceptar
        en la respuesta?

      > Accept-Languague: es-ar,es; q=0.8; en-us; q=0.5; en; q=0.3

    - ¿Qué recurso solicitó?

        > Request URI: /

    - ¿Cuándo fue modificado por última vez el recurso solicitado?

        > If-Modified-Since: Tue 26 Mar 2013 15:03:53 GMT

    - ¿Qué método utilizó: (GET/POST)?

        > GET

    - ¿Cuántas cabeceras viajaron en el requerimiento?

        ```
        GET / HTTP/1.1
        Host: www.redes.unlp.edu.ar
        Connection: keep-alive
        Cache-Control: max-age=0
        Accept: application/xml,application/xhtml+xml,text/html;q=0.9,text/plain;q=0.8,image/png,*/*;q=0.5
        User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-US) AppleWebKit/534.3 (KHTML, like Gecko) Chrome/6.0.472.63 Safari/534.3
        Accept-Encoding: gzip,deflate,sdch
        Accept-Language: en-US,en;q=0.8
        Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3
        If-None-Match: "4f9d3-161c-4d8d53acd2840"
        If-Modified-Since: Tue, 26 Mar 2013 15:03:53 GMT
        ```
        > Cantidad de Headers: 11

    - ¿Cuál es el código de estado devuelto a tu navegador por el servidor en
        la respuesta? ¿Cuál es el significado de ese código de estado?

       > El codigo es el 200: OK

    - ¿Cuántas cabeceras viajaron en la respuesta?

      ```bash
      curl -I www.redes.unlp.edu.ar
      ```
      ```
      HTTP/1.1 200 OK
      Date: Fri, 27 Mar 2015 03:10:42 GMT
      Server: Apache/2.2.16 (Debian)
      Last-Modified: Tue, 26 Mar 2013 15:03:53 GMT
      ETag: "551cc-161c-4d8d53acd2840"
      Accept-Ranges: bytes
      Content-Length: 5660
      Vary: Accept-Encoding
      Content-Type: text/html
      ```
      > Cantidad de Headers: 9

    - ¿Por qué en uno de los requerimientos está presente el encabezado
      `If-Modified-Since`? (Relacionar con el código de la respuesta recibida).

    - ¿Es posible extraer de la respuesta recibida la página que carga el
      navegador? Verifique en la captura los datos recibidos y compare con el
      código fuente de la página cargada.

        > Si, viene en el body del response como texto plano.

19. Utilizando el Live CD, abra un navegador (Iceweasel) e ingrese a la URL:
    www.redes.unlp.edu.ar/

  1. Ingrese al link en la sección "Capa de Aplicación" llamado "Protocolos
     HTTP". En la página mostrada se visualizan dos nuevos links llamados:
     Protocolo HTTP/1.1 y Protocolo HTTP/1.0.  Antes de ingresar a estos links
     continúe con el siguiente punto.

  2. Utilizando el analizador de paquetes Wireshark capture los paquetes
     enviados y recibidos al presionar sobre el link.

  3. Explique la diferencia entre la versión HTTP 1.0 y la versión HTTP 1.1

20. Utilizando el Live CD, abra un navegador en ingrese a la URL:
    www.redes.unlp.edu.ar/

  1. Ingrese al link en la sección "Capa de Aplicación" llamado "Métodos HTTP".
     En la página mostrada se visualizan dos nuevos links llamados: Método GET
     y Método POST. Ambos muestran un formulario como el siguiente:

  2. Analice el código HTML.

    > Difiere el metodo mediante el cual sera enviado el formulario

  3. Utilizando el analizador de paquetes Wireshark capture los paquetes
     enviados y recibidos al presionar el botón Enviar.

  4. ¿Qué diferencias detectó en los mensajes enviados por el cliente?

  5. ¿Observó alguna diferencia en el browser si se utiliza un mensaje u otro?

    > Al utilizar el metodo GET se ven los parametros en la url, mientras
      que al utilizar el POST estos se envian en el body del request.

21. Investigue para qué puede ser utilizado el comando curl. Con el mismo,
    determine la versión del servidor web que sirve el sitio
    https://www.google.com/. ¿Qué parámetros del comando utilizó?

    > curl es una herramienta para transferir datos desde o hacia un servidor.

    ```bash
    curl -sI www.google.com | grep -i server
    ```
    ```
    #=> Server: GFE/2.0
    ```

22. Relacione DNS con HTTP. ¿Se puede navegar si no hay servicio de DNS?

SMTP, POP e IMAP
----------------

23. ¿Qué protocolos se utilizan para el envío y la recepción de mails?

  Uso       | Protocolo
  ----------|----------------------------------------
  Envio     | SMTP (Simple Mail Transfer Protocol)
  Recepcion | IMAP (Internet Message Access Protocol)
            | POP (Post Office Protocol)


24. ¿Qué protocolos se utilizan para la recepción de mails? Enumere y explique
    caracteristicas y diferencias entre las alternativas posibles.

  > IMAP trabaja en modo de conexion permanete, es posible especificar
    carpetas del lado del sevidor, visualizar mensajes de forma remota.
    Transmite solo la cabecera del mensaje, dandole la posibilidad al usuario
    de borrarlo directamente. El almacenamiento local del mensaje es opcional.

  > POP se conecta periodicamente al servidor para buscar nuevo correo, en
    cada conexion se bajan todos los correos nuevos sin importar si se vayan a
    leer o no. Por defecto elimina los mensajes del servidor, no permitiendo el
    acceso a ellos desde otros dispositivos.


25. Utilizando el Live CD, abra el cliente de correo (Icedove) y configure:

  1. Una cuenta de correo POP (Omitir advertencia por uso de conexión sin
     cifrado)

  ```
  Cuenta de correo: alumnopop@redes.unlp.edu.ar
  Nombre de usuario: alumnopop
  Contraseña: alumnopoppass
  Servidor de correo POP: mail.redes.unlp.edu.ar
  Servidor de correo saliente (SMTP): mail.redes.unlp.edu.ar
  ```

  2. Una cuenta de correo IMAP (Omitir advertencia por uso de conexión sin
     cifrado)

  ```
  Cuenta de correo: alumnoimap@redes.unlp.edu.ar
  Nombre de usuario: alumnoimap
  Contraseña: alumnoimappass
  Servidor de correo IMAP: mail.redes.unlp.edu.ar
  ```

  ```
  Nota: Luego de autoconfigurar automáticamente una cuenta pop o imap, el envío
  de mails se auto configura para realizarse vía SMTP con autenticación. Para
  poder enviar mails es necesario sacar la opcion de autenticación en los
  servidores de correo saliente (Editar Configuración de cuentas  configuración
  del servidor saliente  editar  destildar la opción "usar nombre y contraseña"
  ```

  3. Envíe un email desde el cliente de una cuenta a la otra y luego chequee el
     correo de ambas cuentas.  Enviando mails (Analizando SMTP):

  4. Reitere el proceso de envío, esta vez capturando los paquetes de protocolo
     SMTP utilizando Wireshark. Analice el intercambio del protocolo entre el
     cliente y el servidor, identificando cada comando y su correspondiente
     respuesta, realice un gráfico que muestre este intercambio.

  5. Desde una terminal, utilice los comandos del protocolo SMTP observados en
     el punto anterior, para enviar un mail al servidor en forma manual.

    ```
    Nota 1: para conectarse al servidor deberá utilizar el comando:
    telnet mail.redes.unlp.edu.ar 25
    ```
    ```
    Nota 2: Verifique que haya recibido el correo en la cuenta a la que haya
    enviado el correo desde la consola.
    ```

  6. Repita este procedimiento utilizando una cuenta diferente de mail para el
     campo From:, luego verifique que el correo recibido por el destinatario
     tenga la cuenta ficticia. Recibiendo mails (Analizando POP e IMAP):

  7. Vuelva a enviar un correo a alumnopop@redes.unlp.edu.ar utilizando el
     cliente de correo configurado. Comience la captura con Wireshark y chequee
     la cuenta.de correo de alumnopop para capturar tráfico del protocolo POP.
     Analice el intercambio del protocolo entre el cliente y el servidor,
     identificando cada comando y su correspondiente respuesta, realice un
     gráfico que muestre este intercambio.

  8. Vuelva a enviar un mensaje a alumnopop@redes.unlp.edu.ar y sin chequear
     los mensajes con el cliente, Comience la captura y desde una terminal,
     utilice los comandos del protocolo POP observados en el punto anterior
     para consultar los mails del usuario alumnopop. lea el contenido del
     primer mail desde la consola utilizando telnet.

    ```
    Nota: para conectarse al servidor deberá utilizar el comando: telnet
    mail.redes.unlp.edu.ar 110
    ```

  9. Cierre el telnet y comience una nueva captura. Chequee nuevamente el mail
     con el cliente configurado. ¿Qué diferencia encuentra entre ambas
     capturas?

  10. Con el rol de administrador del sistema (root), ejecute el cliente de
      correos. Para esto, abra una consola de comandos y ejecute: `sudo
      icedove`

      De esta forma, ud. iniciará el cliente de correo con el perfil del
      superusuario (diferente del usuario con el que configuró las cuentas
      antes mencionadas). Recuerde que la contraseña del usuario root es
      lihuen.

      Luego configure las cuentas pop e imap de los usuarios alumnopop y
      alumnoimap como se describió anteriormente pero desde el cliente de
      correos del usuario root


      ¿Qué diferencias observa entre el servicio ofrecido por POP vs el
      ofrecido por IMAP?

26. Relacione DNS con SMTP. Describa el proceso completo para el envío de un
    correo desde pepe@yahoo.com a jose@hotmail.com.

  ```
  Ayuda: Tenga en cuenta al analizar dicho proceso, como hace el servidor de
  correo del usuario que manda el correo electrónico, para identificar el
  servidor de correo al que debería enviar el correo. El proceder de las
  comunicaciones tiene un parecido al ejercicio en el que se describe cómo
  viaja una carta postal desde el origen al destino.
  ```

Desafio - Capa de Aplicación
----------------------------

Realice los siguientes pasos para iniciar el ejercicio  

1. Inicie el LiveCD de modo que el mismo tenga acceso a Internet 

2. Descargue en el LiveCD el archivo publicado en el sitio de la materia.

3. Abra una terminal de root y vaya al directorio en el que está el archivo
   descargado

4. Posiblemente al archivo le falten permisos de ejecución. Ejecute lo
   siguiente para agregárselos:

    ```bash
    chmod 755 binario 
    ```

5. Ejecute el archivo descargado, para ello debe ejecutar:

    ```bash
    ./binario <parametro> 
    ```

  El parámetro esperado por el binario es el nombre del servidor Web que sirve
  el sitio de la Secretaría de Extensión de la Facultad de Informática
  (http://extension.info.unlp.edu.ar)

  Si la ejecución del mismo es correcta, deberá recibir en pantalla el
  siguiente mensaje

  ```
  "***** El desafío está en marcha *****"
  ```
 
6. Abra un navegador e intente navegar en Internet 
 
  Responda: 
 
  - Es posible navegar correctamente? Pruebe sitios como: 
    http://ar.yahoo.com/
    http://163.10.5.91
  - ¿Qué fue lo que ocurrió? ¿Cómo lo solucionaría?

    > No, se soluciona configurando un servidor DNS en /etc/resolv.conf, por e

7. Luego de solucionar el problema, corrobore que los sitios más
visitados funcionan correctamente:
 
  https://www.facebook.com
  https://www.google.com
  https://www.gmail.com

  Responda: 
 
  - ¿Detectó algún problema? 

      > google.com no funciona.

  - ¿Qué debe hacer para solucionarlo? 

      > borrando la linea que lo referencia en /etc/hosts

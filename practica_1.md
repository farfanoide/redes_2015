Redes y comunicaciones – 2015 Práctica 1
========================================


1. ¿Qué es una red? ¿Cuál es el principal objetivo para construir una red?

  > Una red (de computadoras) es un conjunto de hosts interconectados entre si,
  > los cuales comparten informacion, recursos y servicios. Los objetivos de
  > las redes es hacer que todos los programas, datos y equipos estén
  > disponibles para cualquiera de la red que lo solicite, sin importar la
  > localización física del recurso y del usuario.

2. ¿Qué es Internet? Describa los principales componentes que permiten su
funcionamiento.

  > Internet es una red de redes, debilmente jerarquica que se basa en ciertos
  > protocolos que rigen su funcionamiento. Un protocolo define el formato y el
  > orden de los mensajes intercambiados entre dos o más entidades que se
  > comunican, así como las acciones que se llevan a cabo en la transmisión y/o
  > recepción de un mensaje u otro evento.

  <!-- tcp/ip, routers... -->
  <!-- &#45; hardware? -->

3. ¿Qué son las RFCs?

  > Petición de Comentarios (en español). Es un estandar. Primero los RFC eran
  > comentarios y aportes; luego se hizo un estandar. Cada una de ellas
  > individualmente es un documento cuyo contenido es una propuesta oficial
  > para un nuevo protocolo de la red Internet. Cualquiera puede enviar una
  > propuesta de RFC a la IETF (Grupo de Trabajo en Ingeniería de Internet),
  > pero es ésta la que decide finalmente si el documento se convierte en una
  > RFC o no. Si luego resulta lo suficientemente interesante, puede llegar a
  > convertirse en un estándar de Internet.

4. ¿Qué es un protocolo?

  > Un protocolo de comunicaciones es el conjunto de reglas normalizadas para
  > la representación, señalización, autenticación y detección de errores
  > necesario para enviar información a través de un canal de comunicación.

5. ¿Por qué dos máquinas con distintos sistemas operativos pueden formar parte
   de una misma red?

  > Ese es uno de los objetivos de las redes, que las redes físicas
  > heterogéneas que la componen funcionen como una red lógica única.

  - standares y protocolos?

6. ¿Cuáles son las 2 categorías en las que pueden clasificarse a los sistemas
   finales o End Systems? Dé un ejemplo del rol de cada uno en alguna
   aplicación distribuida que corra sobre Internet.

  > Las dos categorias son: cliente y servidor. Un ejemplo de rol del lado del
  > servidor es: un servidor Apache, o un servidor Web y del lado del cliente
  > un browser.

7. Cuál es la diferencia entre una red conmutada de paquetes y una red
   conmutada de circuitos.

  > Cuando se usa un circuito en una red de conmutación de circuitos, se tiene
  > el circuito completo durante todo el tiempo que se esté usando, sin la
  > competencia de otros usuarios. En las redes de conmutación de paquetes,
  > como es Internet, los paquetes se enrutan a su destino por la ruta más
  > oportuna, pero no todos los paquetes que viajan entre dos hosts siguen la
  > misma ruta, ni siquiera los que pertenecen a un mismo mensaje. Esto
  > prácticamente garantiza que los paquetes llegarán en diferentes momentos y
  > desordenados. En una red de conmutación de paquetes, los paquetes (mensajes
  > o fragmentos de mensajes) se enrutan individualmente entre los nodos en
  > vínculos de datos que pueden estar compartidos por otros nodos. En la
  > conmutación de paquetes, a diferencia de la conmutación de circuitos, las
  > diferentes conexiones con nodos de la red comparten el ancho de banda
  > disponible.

8. Analice de qué tipo de red es una red de telefonía y de cuál Internet.

  > Una red de telefonía es una red de conmutacion de circuitos.
  > Una red de internet es una red de conmutacion de paquetes.

9. Dada la siguiente situación: el empleado Pablo Marques que trabaja en la
   oficina “Ventas”

  (3er piso) situada en el Edificio de la empresa XX (en BA), envía una carta a
  Mario Pesada, que trabaja en la oficina de Personal de la empresa YY en un
  edificio ubicado en la ciudad de Madrid, España (en dicho edificio, funciona
  la empresa YY en los pisos de 1 a 10 y la empresa ZZ en los pisos 11 a 15).

  Determine:

  1. ¿Cuáles son los pasos necesarios para que la carta llegue desde el origen
     al destino?

  2. ¿Qué información se usa en cada punto del trayecto para que la carta siga
     su recorrido?

  3. ¿Siempre se usa el mismo transporte?

  4. Suponga que la carta está “codificada” usando algún método para que, en el
     caso de que alguien en el camino abriera el sobre, éste no pueda leer el
     verdadero contenido de la misma ¿Quiénes deben poseer la información
     necesario para codificarlo y decodificarlo?

10. Describa brevemente las tecnologías de acceso residencial a redes.

  > Acceso residencial se refiere a la conexion de un sistema terminal a un
  > router borde. Las tecnologias de acceso residencial a redes, como la
  > internet, hoy en dia son de lo llamado "banda ancha", esto quiere decir que
  > proporcionan velocidades mayores a 54 Kbps. A los usuarios se les brinda
  > internet a travez de la linea telefonica o a travez del cable coaxil de TV.

11. ¿Qué ventajas tiene una implementación basada en capas o niveles?

  > La ventaja de utilizar este tipo de implementación es que cada capa permite
  > la identificación y relación de las partes complejas del sistema, al estar
  > éste modulado es mas facil el mantenimiento y actualizacion del mismo. Cada
  > capa en combinación con las capas inferiores, implementa alguna función y
  > presta algún servicio.

12. ¿Cómo se llama la PDU de cada una de las capas del stack TCP/IP?


   Capa        |  PDU
  -------------|--------------
  Aplicacion   | Mensajes
  Transporte   | Segmento
  Red          | Datagrama
  Enlace       | Marco
  Fisica       | PDU-1   

13. Describa cuales son las funciones de cada una de las capas del stack TCP/IP
    o protocolo de Internet.

  Capa         | Funcion
  -------------|-------------------------------------------------------
  Aplicacion   | Network process to application
               | Representacion de datos y encripcion
               | Comunicacion entre hosts
  Transporte   | Conexion entre terminales y fiabilidad
  Internet/Red | Determinacion de camino y IP (Direccionamiento logico)
  Acceso a Red | MAC y LLC (Direccionamiento fisico)
               | Transimision binaria.

14. Compare el modelo OSI con la implementación TCP/IP.

  Capa           | Funcion
  ---------------|-------------------------------------------------------------------------------------------------------------------
  Aplicacion     | servicios de red a los usuarios y a procesos, aplicaciones.
  Presentation   | Representacion de datos y encripcion (formato de los datos.)
  Sesion         | Comunicacion entre hosts (mantener track de sesiones de la aplicacion.)
  Transporte     | Conexion entre terminales y fiabilidad
  Red            | Determinacion de camino y IP (Direccionamiento logico)
                 | (direccionar y rutear los mensajes host-to-host. Comunicar varias redes.)
  Enlace         | comunicacion entre entes directamente conectados. Comunicar una misma red. Acceso al Medio.
  Fisica         | transportar la informacion como señal por el medio fisico. Caracteristicas fisicas. Informacion binaria, digital.




  Capas                                              | servicios
  -------------------------------------------------- | --------------------------------------------------------
  Aplicacion, Presentation, Sesion, Transporte, Red  | proveen envio de datos de forma confiable.
  Enlace, Fisica                                     | controlan el envio fisico de los mensajes sobre la red.

Extra
-----

  - Cada SA se conecta a un router de borde o gateway, que lo conecta a otros.
    Se denominan EGP (Exterior Gateway Protocols) a los protocolos entre
    distintos AS (GGP, EGP, BGP).

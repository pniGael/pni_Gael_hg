
#**PRÁCTICA DE COMANDOS DE RED EN WINDOWS Y LINUX I**

**Objetivo**

La siguiente práctica está destinada a comprender algunos comandos importantes que son de gran utilidad en la administración de una red. 

**Material necesario**

Necesitaremos dos máquinas virtuales o reales. Una con un sistema operativo Windows y otra con Linux.

***1. Comando `ipconfig` (Windows)***

Este comando nos permite ver datos relacionados con la configuración de red de nuestro equipo. Algunas de sus principales opciones son:

***`ipconfig /all`***  -> Nos muestra información más detallada del adaptador de red.

***`ipconfig /release`*** -> Libera las configuración asignada por dhcp.

***`ipconfig /renew`*** -> Solicita al servidor DHCP la renovación de una configuración de red.

***`ipconfig /displaydns`*** -> Muestra el contenido de la caché DNS de nuestro equipo.

***`ipconfig /flushdns`*** -> Borra la caché DNS de nuestro equipo.

**Ejercicios**

+ Use el comando ***`ipconfig /all`*** para ver la dirección MAC de tu equipo.  Y la siguiente aplicación <http://coffer.com/mac_find/> para rellenar la siguiente tabla.


|Dirección IP v4|10.0.2.15|  
| - | - |
|Máscara|255.255.255.0| 
|Gateway|10.0.2.2| 
|MAC|08-00-27-77-E0-04| 
|Fabricante|cadmus computer systems|
|Dirección IP v6|00-01-00-01-2A-FA-B2-27-08-00-27-77-E0-04| 
|Servidores DNS|10.0.2.3| 
|Tiempo de concesión de la IP|Concesión obtenida: martes, 10 de enero de 2023 9:58:19 / La concesión expira : miércoles, 11 de enero de 2023 9:58:19|  
|Nombre del adaptador de red|Intel(R) PRO/1000 MT Desktop Adapter|

![Imagen 1](/img/1.png)
![Imagen 2](/img/2.png)

+ Liberar la configuración IP del adaptador con ***`ipconfig /release`*** y a continuación volver a usar el comando ***`ipconfig`*** . ¿Cuál es la ip ahora?

La nueva ip es:  169.254.78.165

![Imagen 3](/img/3.png)


+ Ejecutar el comando ***`ipconfig /renew`*** solicitando una renovación de dirección IP. A continuación volver a ejecutar ***`ipconfig`*** . ¿Cuál es la nueva ip?

La nueva ip es:  10.0.2.15

![Imagen 4](/img/4.png)


+ Ejecutar el comando ***`ipconfig /displaydns`*** y comprobar la información que contiene la caché DNS de tu equipo. Ejecuta ahora el comando ***`ipconfig /flushdns`** y después muestra otra vez el contenido de la caché DNS. ¿Qué información muestra ahora? ¿Qué ha ocurrido?*

Al ejecutar de nuevo el comando desplaynds no se muestra nada, ya que hemos borrado la caché del DNS.

![Imagen 5](/img/5.png)



+ Usar el navegador para ir a la web [https://www.w3schools.com]() y luego ejecutar el comando ***`ipconfig /displaydns`*** . Hacer una captura de pantalla donde se muestre que se ha cacheado la ip de ese nombre de dominio y pegarla aquí debajo.

![Iamgen 6](/img/7.png)



+ Borra la caché DNS con el comando ***`ipconfig /flushdns`*** y muestra una captura de pantalla en que se vea que ya no hay registros DNS en caché.

![Imagen 5](/img/5.png)


***2. Comando `ifconfig` (Línux)***

Este comando nos permite mostrar la configuración IP de nuestra máquina y configurar algunos parámetros. Algunas opciones de interés son:

***`ifconfig  –a`*** -> Nos muestra la configuración de todas las tarjetas de red incluso las desactivadas.

***`ifconfig eth0 down`*** -> Desactiva una tarjeta de red llamada eth0. (También vale ***ifdown eth0***)

***`ifconfig eth0 up`*** -> Activa la tarjeta de red llamada eth1. (También vale ***ifup eth0***)

***`ifconfig eth0 192.168.1.1 netmask 255.255.255.192`*** -> Asigna una IP y una máscara a la tarjeta eth0.

**Ejercicios**

+ Ejecuta el comando ***`ifconfig`*** y rellena lo que puedas de la siguiente tabla.


|Dirección IP v4|172.18.99.10|  
| - | - |
|Máscara|255.255.0.0| 
|Gateway|127.18.255.255| 
|MAC|08:00:27:7a:f8:8e|
|Fabricante|cadmus computer systems| 
|Dirección IP v6|fe80::2b6b:79f0:2d1b:9797/64| 
|Servidores DNS|127.0.0.53| 
|Tiempo de concesión de la IP|valid_lft 86205sec preferred_lft 86205sec| 
|Nombre del adaptador de red|enp0s3| 

![Imagen 8](/img/8.png)

![Imagen 9](/img/9.png)

+ Desactiva tu tarjeta de red con el comando ***`ifconfig eth0 down`***. A continuación, comprueba con un ***`ifconfig`*** que la tarjeta ya no aparece, se ha desactivado. Haz una captura de pantalla donde se vea que ya no está activada.

![Imagen 10](/img/10.png)


+ Usa el comando ***`ifconfig –a`*** para ver que la tarjeta está desactivada (pega una captura de pantalla debajo).

![Imagen 11](/img/11.png)


+ Ahora activa la tarjeta con el comando ***`ifconfig eth0 up`*** y luego con el comando `ifconfig` comprueba que ya está habilitada (pega una captura de pantalla debajo).

![Imagen 12](/img/12.png)

+ Usa el comando ***`ifconfig eth0 192.168.99.99 netmask 255.255.255.0`*** y pega una captura de pantalla que muestre que el adaptador de red se ha configurado correctamente.

![Imagen 13](/img/13.png)


***3. Comando ping (Windows y Línux)***

Se usa para saber si hay comunicación entre equipos. Podría “no funcionar” en caso de que el ordenador al que hacemos el ping tenga un firewall que ignore nuestros mensajes. 

Algunas opciones para Windows/Linux son

***-n*** -> Indica el número de paquetes que se enviarán. ( ***-c*** en linux)

***-l*** -> establece el tamaño del mensaje que se envía. ( ***-s*** en linux)

***-t*** -> envía paquetes de manera indefinida hasta que lo paramos con “***ctrl+c***”

***-i*** -> establecemos el TTL del ping, es decir, el número de saltos que debe dar antes de que lo destruyan. ( ***-t*** en linux)

**Ejercicios**

+ Desde una máquina con línux ejecuta el comando ***`ping –s 100 –c 2  ip\_puertadeenlace`*** para que se envíen dos ecos de 100 bytes. Muestra una captura de pantalla con el resultado.

![Imagen 16](/img/16.png)


+ Desde una máquina con windows usa el comando ***`ping –i 2 ip\_puertadeenlace`*** para hacer un ping a nuestra puerta de enlace con un TTL igual a 2. 

![Imagen 17](/img/14.png)

![Imagen 18](/img/15.png)

+ Luego haz un ping de las mismas características, pero a google ***`ping –i 2 www.google.es`*** Pega una captura de pantalla con el resultado y explica lo que ha pasado.

![Imagen 18](/img/18.png)

+ El comando ping nos da información sobre el tiempo de latencia de una red. Haz un ping a nuestra puerta de enlace y luego a otro a [www.google.es](http://www.google.es/). Busca información de lo que es el tiempo de latencia y compara los tiempos de latencia en ambos casos. 

![Imagen 18](/img/18.png)

***4. Comando route (Línux)***

Nos permite ver y configurar la tabla de rutas de nuestro equipo. Algunas opciones de uso son: 

***`route`*** -> Nos muestra la tabla de enrutamiento del equipo.
***`route del default gw ip_gateway`*** -> Borra la ruta por defecto.
***`route add default gw ip_gateway`*** -> Añade la puerta de enlace indicada para nuestro host.

**Ejercicios**

+ Usa el comando `route` para ver la puerta de enlace de tu equipo. ¿Cuál es tu puerta de enlace?

La puerta de enlace es 172.18.0.1

+ Borra la puerta de enlace usando el comando `route del default gw ip_gateway`. A continuación, ejecuta el comando `route` para comprobar que ya no hay puerta de enlace. Intenta navegar por internet y verás que tampoco puedes. Haz una captura de pantalla con la salida del comando `route` y del resultado de `ping 8.8.8.8` ¿Cómo interpretas el mensaje que te devuelve el `ping`?

Tras realizar esta rerie de comandos, el ping a 8.8.8.8 se muestra inaccesible ya que el ordenador ha perdido la puerta de enlace

+ Vuelve a configurar la puerta de enlace usando el comando `route add default gw ip_gateway` y comprueba que ya ha vuelto la puerta de enlace con el comando `route`.

***5. Comando netstat (Línux y Windows)***

Nos muestra las conexiones que tiene nuestro host abiertas con la red. Algunas opciones para Linux son:

***-t*** → Muestra las conexiones tcp abiertas. (en windows -p tcp)
***-u*** → Muestra las conexiones udp abiertas. en windows -p udp)
***-a*** → Muestra los puertos que estén esperando conexiones (puertos en escucha). -n → Para que muestre solo información numérica.
***-s*** → Nos muestra estadísticas sobre nuestra conexión de red.
***-r*** → Nos muestra la tabla de enrutamiento de nuestro host.

**Ejercicios**

+ Abre una página web cualquiera y luego ejecuta el comando `netstat -t` para que nos muestre las conexiones que tenemos abiertas por tcp. Pon una captura de pantalla del resultado y explica lo que es cada una de las columnas que aparecen.

Lo que se muestra en estas columnas, por orden, son el puerto TCP, los paquetes recibidos, enviados, la dirección local, la dirección a la web y el estado de la conenexión entre las dos columnas anteriores.

![Imagen 23](/img/23.png)

+ Ahora espera unos segundos y vuelve a ejecutar `netstat -tn`. Comprobarás que algunas de las conexiones se han cerrado o están esperando para cerrarse. Además con la opción **-n** verás los resultados en formato numérico. Pon una captura de pantalla y explica la diferencia entre ***Established***, ***Time_wait*** y ***Close_Wait***.

Lo que significa cada una de estos estados de red es, conexión establecida, conexión en tiempo de espera y conexión cerrada respectivamente.

![Imagen 24](/img/24.png)

+ Ejecuta ahora la orden `netstat -at` para que muestre las tanto las conexiones tcp abiertas como los puertos que están a la escucha. Copia una captura de pantalla donde se vean los puertos que tienes escuchando, explica qué significan los asteriscos en la columna ***“Foreign address”*** e investiga si tener esos puertos abiertos es normal o supone una amenaza.

El tipo de conexión es TCP tendrá el estado LISTEN. Esto quiere decir que la máquina local está esperando a que otra máquina remota envíe datos. En este caso es normal tenrlos abiertos porque el equipo está conectado dentro de una red.

![Imagen 25](/img/25.png)


+ Ejecuta el comando `netstat -s` para ver las estadísticas de red y haz una captura en la que se vean cuantos paquetes tcp has recibido y cuantos de ellos han sido erroneos.

![Imagen 26](/img/26.png)
![Imagen 27](/img/27.png)

***6. Comando arp (Línux y Windows)***

Se usa para mostrar y administrar la caché `ARP` de nuestro equipo. Las opciones más habituales son:

***`arp -a`*** → Muestra la tabla arp del host (en línux no hace falta el -a)
***`arp -d dirección_ip`*** → borra de la tabla la entrada indicada
***`arp -d *`*** → borra toda la tabla arp (el equivalente en linux: `ip neigh flush all`) 
***`arp -s direccion_ip direccion_mac`*** → crea una entrada en la tabla ARP

**Ejercicios**

+ Borra toda la caché ARP con el comando `arp -d *`. A continuación haz un ping a la puerta de enlace. Pon una captura de la tabla ARP en que se vea que solo está la puerta de enlace y su mac.

![Imagen 22](/img/22.png)

+ Ahora borra manualmente la entrada arp de la puerta de enlace con la orden `arp -d ip_puertadeenlace`. Luego introduce manualmente una mac falsa para la puerta de enlace en la tabla arp con el comando `arp -s ip_puertadeenlace aa:bb:cc:dd:ee:ff` Haz una captura de pantalla en que se vea el resultado del comando arp -a y de hacer un ping a google. Explica por qué ahora no hay internet.

Al introducir una mac falsa, el ordenador ha perdido la conexión.

+ Borra la entrada falsa de la tabla arp con el comando `arp -d ip_puertadeenlace`.

![Imagen 28](/img/28.png)


***7. Comando nslookup (Línux y Windows)***

Este comando nos da información sobre la resolución de nombres dns. Nos dice a quién le hacemos la consulta y qué respuesta nos da. Opciones principales:

***`nslookup dominio`*** → Consulta a nuestro servidor dns por el dominio indicado.
***`nslookup dominio ip_servidordns`*** → consulta al servidor dns indicado por el dominio.

**Ejercicios**

Averigua el nombre del servidor DNS de 
https://www.puertodelacruz.es . A continuación, ejecutamos el comando nslookup nombreServidorDNS y luego el comando `nslookup nombreServidorDNS 8.8.8.8`. Explica las causas de las diferencias que hay entre los resultados de las dos consultas.

![Imagen 29](/img/29.png)
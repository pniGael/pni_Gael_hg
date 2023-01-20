
﻿
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

![1](https://user-images.githubusercontent.com/113589134/213814389-2a43da6d-32bf-4c0b-99bf-983335096f4c.png)
![2](https://user-images.githubusercontent.com/113589134/213814395-7fa51597-3ed0-4706-b394-9b2f703337a4.png)

+ Liberar la configuración IP del adaptador con ***`ipconfig /release`*** y a continuación volver a usar el comando ***`ipconfig`*** . ¿Cuál es la ip ahora?

La nueva ip es:  169.254.78.165

![3](https://user-images.githubusercontent.com/113589134/213814397-f7f0b0cd-2ddd-46ab-914c-324cafb262b9.png)


+ Ejecutar el comando ***`ipconfig /renew`*** solicitando una renovación de dirección IP. A continuación volver a ejecutar ***`ipconfig`*** . ¿Cuál es la nueva ip?

La nueva ip es:  10.0.2.15

![4](https://user-images.githubusercontent.com/113589134/213814398-bdceda90-2381-42a8-bf53-5037eef7706c.png)


+ Ejecutar el comando ***`ipconfig /displaydns`*** y comprobar la información que contiene la caché DNS de tu equipo. Ejecuta ahora el comando ***`ipconfig /flushdns`** y después muestra otra vez el contenido de la caché DNS. ¿Qué información muestra ahora? ¿Qué ha ocurrido?*

Al ejecutar de nuevo el comando desplaynds no se muestra nada, ya que hemos borrado la caché del DNS.

![5](https://user-images.githubusercontent.com/113589134/213814400-2e76f9e8-a209-45a2-94ea-9b1ff5938164.png)



+ Usar el navegador para ir a la web [https://www.w3schools.com]() y luego ejecutar el comando ***`ipconfig /displaydns`*** . Hacer una captura de pantalla donde se muestre que se ha cacheado la ip de ese nombre de dominio y pegarla aquí debajo.

![7](https://user-images.githubusercontent.com/113589134/213814402-195ea15c-a311-40f0-ab6d-adc0ae9af113.png)



+ Borra la caché DNS con el comando ***`ipconfig /flushdns`*** y muestra una captura de pantalla en que se vea que ya no hay registros DNS en caché.




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

![8](https://user-images.githubusercontent.com/113589134/213814403-397f991c-e651-411b-8b94-5163cb68416b.png)

![9](https://user-images.githubusercontent.com/113589134/213814404-d69cc7d9-11eb-45a0-a987-c7d6e7bd13a2.png)

+ Desactiva tu tarjeta de red con el comando ***`ifconfig eth0 down`***. A continuación, comprueba con un ***`ifconfig`*** que la tarjeta ya no aparece, se ha desactivado. Haz una captura de pantalla donde se vea que ya no está activada.

![10](https://user-images.githubusercontent.com/113589134/213814406-48d7b58f-5c9d-4a54-95a9-e428bad53086.png)


+ Usa el comando ***`ifconfig –a`*** para ver que la tarjeta está desactivada (pega una captura de pantalla debajo).

![11](https://user-images.githubusercontent.com/113589134/213814408-b9d8ff5e-c659-4ee9-94cc-52a8635c95dc.png)


+ Ahora activa la tarjeta con el comando ***`ifconfig eth0 up`*** y luego con el comando `ifconfig` comprueba que ya está habilitada (pega una captura de pantalla debajo).

![12](https://user-images.githubusercontent.com/113589134/213814409-3328bc5c-d240-4f56-981b-16b86209b557.png)

+ Usa el comando ***`ifconfig eth0 192.168.99.99 netmask 255.255.255.0`*** y pega una captura de pantalla que muestre que el adaptador de red se ha configurado correctamente.

![13](https://user-images.githubusercontent.com/113589134/213814411-4b0f932b-1f1b-4882-b09a-5b099ec8c84d.png)


***3. Comando ping (Windows y Línux)***

Se usa para saber si hay comunicación entre equipos. Podría “no funcionar” en caso de que el ordenador al que hacemos el ping tenga un firewall que ignore nuestros mensajes. 

Algunas opciones para Windows/Linux son

***-n*** -> Indica el número de paquetes que se enviarán. ( ***-c*** en linux)

***-l*** -> establece el tamaño del mensaje que se envía. ( ***-s*** en linux)

***-t*** -> envía paquetes de manera indefinida hasta que lo paramos con “***ctrl+c***”

***-i*** -> establecemos el TTL del ping, es decir, el número de saltos que debe dar antes de que lo destruyan. ( ***-t*** en linux)

**Ejercicios**

+ Desde una máquina con línux ejecuta el comando ***`ping –s 100 –c 2  ip\_puertadeenlace`*** para que se envíen dos ecos de 100 bytes. Muestra una captura de pantalla con el resultado.

![16](https://user-images.githubusercontent.com/113589134/213814417-47c7b20e-6b21-4ef9-9ec6-812cf19d9dd9.png)


+ Desde una máquina con windows usa el comando ***`ping –i 2 ip\_puertadeenlace`*** para hacer un ping a nuestra puerta de enlace con un TTL igual a 2. 

![17](https://user-images.githubusercontent.com/113589134/213814420-9723aa0f-87cf-4e42-aab1-fb50055d42f0.png)


+ Luego haz un ping de las mismas características, pero a google ***`ping –i 2 www.google.es`*** Pega una captura de pantalla con el resultado y explica lo que ha pasado.

![18](https://user-images.githubusercontent.com/113589134/213814421-3ed355dd-4a29-441e-ade0-5e500bffed92.png)

+ El comando ping nos da información sobre el tiempo de latencia de una red. Haz un ping a nuestra puerta de enlace y luego a otro a [www.google.es](http://www.google.es/). Busca información de lo que es el tiempo de latencia y compara los tiempos de latencia en ambos casos. 

![19](https://user-images.githubusercontent.com/113589134/213814422-0aed575a-9b06-4a9d-ba28-253ab79d1f3d.png)

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

![23](https://user-images.githubusercontent.com/113589134/213814431-66b51930-f4ae-4fd1-a925-3a18c4ae1cca.png)

+ Ahora espera unos segundos y vuelve a ejecutar `netstat -tn`. Comprobarás que algunas de las conexiones se han cerrado o están esperando para cerrarse. Además con la opción **-n** verás los resultados en formato numérico. Pon una captura de pantalla y explica la diferencia entre ***Established***, ***Time_wait*** y ***Close_Wait***.

Lo que significa cada una de estos estados de red es, conexión establecida, conexión en tiempo de espera y conexión cerrada respectivamente.

![24](https://user-images.githubusercontent.com/113589134/213814433-761b0d4f-6c4c-4454-9685-7db627726e34.png)

+ Ejecuta ahora la orden `netstat -at` para que muestre las tanto las conexiones tcp abiertas como los puertos que están a la escucha. Copia una captura de pantalla donde se vean los puertos que tienes escuchando, explica qué significan los asteriscos en la columna ***“Foreign address”*** e investiga si tener esos puertos abiertos es normal o supone una amenaza.

El tipo de conexión es TCP tendrá el estado LISTEN. Esto quiere decir que la máquina local está esperando a que otra máquina remota envíe datos. En este caso es normal tenrlos abiertos porque el equipo está conectado dentro de una red.

![25](https://user-images.githubusercontent.com/113589134/213814435-7df9bd49-b269-45f4-8876-68f7ab7faa9c.png)


+ Ejecuta el comando `netstat -s` para ver las estadísticas de red y haz una captura en la que se vean cuantos paquetes tcp has recibido y cuantos de ellos han sido erroneos.

![26](https://user-images.githubusercontent.com/113589134/213814436-a884ceaf-5fbb-4efe-a6ed-2425967576d0.png)
![27](https://user-images.githubusercontent.com/113589134/213814438-ad1ccc30-cdfc-4679-9621-8421062aa059.png)

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

![28](https://user-images.githubusercontent.com/113589134/213814441-142e3750-634c-4948-9d6a-6fee2b5cb7ba.png)


***7. Comando nslookup (Línux y Windows)***

Este comando nos da información sobre la resolución de nombres dns. Nos dice a quién le hacemos la consulta y qué respuesta nos da. Opciones principales:

***`nslookup dominio`*** → Consulta a nuestro servidor dns por el dominio indicado.
***`nslookup dominio ip_servidordns`*** → consulta al servidor dns indicado por el dominio.

**Ejercicios**

Averigua el nombre del servidor DNS de 
https://www.puertodelacruz.es . A continuación, ejecutamos el comando nslookup nombreServidorDNS y luego el comando `nslookup nombreServidorDNS 8.8.8.8`. Explica las causas de las diferencias que hay entre los resultados de las dos consultas.

![29](https://user-images.githubusercontent.com/113589134/213814442-bdaf3580-5f65-42b0-8b7e-833f36db8de3.png)



Como tuve algunos problemas para poner las imágenes, adjunto algununas imagenes más:

![10](https://user-images.githubusercontent.com/113589134/213814406-48d7b58f-5c9d-4a54-95a9-e428bad53086.png)
![11](https://user-images.githubusercontent.com/113589134/213814408-b9d8ff5e-c659-4ee9-94cc-52a8635c95dc.png)
![12](https://user-images.githubusercontent.com/113589134/213814409-3328bc5c-d240-4f56-981b-16b86209b557.png)
![13](https://user-images.githubusercontent.com/113589134/213814411-4b0f932b-1f1b-4882-b09a-5b099ec8c84d.png)
![14](https://user-images.githubusercontent.com/113589134/213814412-0de603d6-7bd3-4667-8fd2-ac08430878be.png)
![15](https://user-images.githubusercontent.com/113589134/213814415-c0d79d70-e478-43ca-82b0-0f7ad33ac27a.png)
![16](https://user-images.githubusercontent.com/113589134/213814417-47c7b20e-6b21-4ef9-9ec6-812cf19d9dd9.png)
![17](https://user-images.githubusercontent.com/113589134/213814420-9723aa0f-87cf-4e42-aab1-fb50055d42f0.png)
![18](https://user-images.githubusercontent.com/113589134/213814421-3ed355dd-4a29-441e-ade0-5e500bffed92.png)
![19](https://user-images.githubusercontent.com/113589134/213814422-0aed575a-9b06-4a9d-ba28-253ab79d1f3d.png)
![20](https://user-images.githubusercontent.com/113589134/213814425-12b18dd8-cf5d-4993-8373-056ac0d622b1.png)
![21](https://user-images.githubusercontent.com/113589134/213814428-f2db4a36-7d63-474c-ab66-a8f5e8a88f55.png)
![22](https://user-images.githubusercontent.com/113589134/213814429-baad4bd5-40ae-42fc-bfef-9427402c8a6c.png)
![23](https://user-images.githubusercontent.com/113589134/213814431-66b51930-f4ae-4fd1-a925-3a18c4ae1cca.png)
![24](https://user-images.githubusercontent.com/113589134/213814433-761b0d4f-6c4c-4454-9685-7db627726e34.png)
![25](https://user-images.githubusercontent.com/113589134/213814435-7df9bd49-b269-45f4-8876-68f7ab7faa9c.png)
![26](https://user-images.githubusercontent.com/113589134/213814436-a884ceaf-5fbb-4efe-a6ed-2425967576d0.png)
![27](https://user-images.githubusercontent.com/113589134/213814438-ad1ccc30-cdfc-4679-9621-8421062aa059.png)
![28](https://user-images.githubusercontent.com/113589134/213814441-142e3750-634c-4948-9d6a-6fee2b5cb7ba.png)
![29](https://user-images.githubusercontent.com/113589134/213814442-bdaf3580-5f65-42b0-8b7e-833f36db8de3.png)

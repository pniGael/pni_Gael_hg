# ENRUTAMIENTO OSPF

Dado el esquema de red:

![](img/001.png)

Y el direccionamiento `IP`:

| Dispositivo | Interface   | IP               |
|-------------|-------------|------------------|
| PC0         |             | 192.168.1.1/24   |
| Router0     | Fa0/0       | 192.168.1.100/24 |
| Router0     | Serial0/0/1 | 192.168.3.1/24   |
| Router1     | Serial0/0/1 | 192.168.3.2/24   |
| Router1     | Fa0/0       | 192.168.2.100/24 |
| PC1         |             | 192.168.2.1/24   |

1. Construye la topología dada y asigna el direccionamiento en base a la tabla
2. Configura en ambos routers el protocolo de enrutamiento dinámico **OSPF** :

+ Router0

~~~
Router(config)#router ospf 1
Router(config-router)#network 192.168.1.0 0.0.0.255 area 0
Router(config-router)#network 192.168.3.0 0.0.0.255 area 0
~~~

+ Router1

~~~
Router(config)#router ospf 1
Router(config-router)#network 192.168.2.0 0.0.0.255 area 0
Router(config-router)#network 192.168.3.0 0.0.0.255 area 0
00:11:15: %OSPF-5-ADJCHG: Process 1, Nbr 192.168.3.1 on Serial0/0/0 from LOADING to FULL, Loading Done
~~~

3. Verifica la conectividad:

+ PC0->PC1

~~~
C:\>ping 192.168.2.1

Pinging 192.168.2.1 with 32 bytes of data:

Reply from 192.168.2.1: bytes=32 time=8ms TTL=126
Reply from 192.168.2.1: bytes=32 time=1ms TTL=126
Reply from 192.168.2.1: bytes=32 time=1ms TTL=126
Reply from 192.168.2.1: bytes=32 time=1ms TTL=126

Ping statistics for 192.168.2.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 8ms, Average = 2ms
~~~

+ PC1->PC0

~~~
C:\>ping 192.168.1.1

Pinging 192.168.1.1 with 32 bytes of data:

Reply from 192.168.1.1: bytes=32 time=9ms TTL=126
Reply from 192.168.1.1: bytes=32 time=1ms TTL=126
Reply from 192.168.1.1: bytes=32 time=1ms TTL=126
Reply from 192.168.1.1: bytes=32 time=1ms TTL=126

Ping statistics for 192.168.1.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 9ms, Average = 3ms

C:\>
~~~

4. Muestra la tabla de enrutamiento


+ Router0

~~~
Router#show ip route 
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

C    192.168.1.0/24 is directly connected, FastEthernet0/0
O    192.168.2.0/24 [110/65] via 192.168.3.2, 00:01:51, Serial0/0/0
C    192.168.3.0/24 is directly connected, Serial0/0/0
~~~

+ Router1

~~~
Router#show ip ro
Router#show ip route 
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

O    192.168.1.0/24 [110/65] via 192.168.3.1, 00:02:32, Serial0/0/0
C    192.168.2.0/24 is directly connected, FastEthernet0/0
C    192.168.3.0/24 is directly connected, Serial0/0/0
~~~

5. Muestra la información del protocolo de enrutamiento


+ Router0

~~~
Router#show ip protocols

Routing Protocol is "ospf 1"
  Outgoing update filter list for all interfaces is not set 
  Incoming update filter list for all interfaces is not set 
  Router ID 192.168.3.1
  Number of areas in this router is 1. 1 normal 0 stub 0 nssa
  Maximum path: 4
  Routing for Networks:
    192.168.1.0 0.0.0.255 area 0
    192.168.3.0 0.0.0.255 area 0
  Routing Information Sources:  
    Gateway         Distance      Last Update 
    192.168.3.1          110      00:03:21
    192.168.3.2          110      00:03:21
  Distance: (default is 110)

~~~

+ Router1

~~~
Router#show ip protocols 

Routing Protocol is "ospf 1"
  Outgoing update filter list for all interfaces is not set 
  Incoming update filter list for all interfaces is not set 
  Router ID 192.168.3.2
  Number of areas in this router is 1. 1 normal 0 stub 0 nssa
  Maximum path: 4
  Routing for Networks:
    192.168.2.0 0.0.0.255 area 0
    192.168.3.0 0.0.0.255 area 0
  Routing Information Sources:  
    Gateway         Distance      Last Update 
    192.168.3.1          110      00:04:17
    192.168.3.2          110      00:04:17
  Distance: (default is 110)

~~~

6. Cambiemos el valor del costo del enlace **OSPF** en el Router0 (era de 65 y lo pasamos a 1562)

+ Router0

~~~
R0(config)#interface serial 0/0/0
R0(config-if)#ip ospf cost 1562
~~~

+ Verificamos que se produce el cambio

~~~
R0#show ip route 
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

C    192.168.1.0/24 is directly connected, FastEthernet0/0
O    192.168.2.0/24 [110/1563] via 192.168.3.2, 00:00:31, Serial0/0/0
C    192.168.3.0/24 is directly connected, Serial0/0/0
~~~


7. Activar la autenticación entre enlaces **OSPF** para evitar la intrusión dentro del sistema de routers. Primero lo realizamos en el Router0 y comprobamos si hay comunicación.


+ Router0

~~~
R0(config)#router ospf 1
R0(config-router)#area 0 authentication message-digest 
R0(config-router)#exit
R0(config)#interface serial 0/0/0
R0(config-if)#ip ospf message-digest-key 1 md5 cisco
~~~

+ Comprobación de conectividad entre  PC0->PC1

~~~
C:\>ping 192.168.2.1

Pinging 192.168.2.1 with 32 bytes of data:

Reply from 192.168.1.100: Destination host unreachable.
Request timed out.
Reply from 192.168.1.100: Destination host unreachable.
Reply from 192.168.1.100: Destination host unreachable.

Ping statistics for 192.168.2.1:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
~~~

+ ¿ Qué mensajes aparecen en el Router1 ?

~~~
00:00:10: %OSPF-5-ADJCHG: Process 1, Nbr 192.168.3.1 on Serial0/0/0 from LOADING to FULL, Loading Done

00:12:40: %OSPF-5-ADJCHG: Process 1, Nbr 192.168.3.1 on Serial0/0/0 from FULL to DOWN, Neighbor Down: Dead timer expired

00:12:40: %OSPF-5-ADJCHG: Process 1, Nbr 192.168.3.1 on Serial0/0/0 from FULL to DOWN, Neighbor Down: Interface down or detached
~~~


8. Activar la autenticación entre enlaces **OSPF** en el Router1

+ Router1

~~~

~~~
Router(config)#router ospf 1
Router(config-router)#area 0 authentication message-digest 
Router(config-router)#exit
Router(config)#interface serial 0/0/0
Router(config-if)#ip ospf message-digest-key 1 md5 cisco
Router(config-if)#exit
Router(config)#
00:22:55: %OSPF-5-ADJCHG: Process 1, Nbr 192.168.3.1 on Serial0/0/0 from LOADING to FULL, Loading Done


+ Comprobación de conectividad entre  PC0->PC1

~~~
C:\>ping 192.168.2.1

Pinging 192.168.2.1 with 32 bytes of data:

Reply from 192.168.2.1: bytes=32 time=1ms TTL=126
Reply from 192.168.2.1: bytes=32 time=1ms TTL=126
Reply from 192.168.2.1: bytes=32 time=7ms TTL=126
Reply from 192.168.2.1: bytes=32 time=1ms TTL=126

Ping statistics for 192.168.2.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 7ms, Average = 2ms

C:\>
~~~

9. En **OSPF**, si queremos propagar alguna ruta por omisión (de las de ruteo estático), utilizaremos el comando `default-information originate`
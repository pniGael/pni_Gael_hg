# CONFIGURACIÓN DE VLAN ESTÁTICAS

![[SCR-20230408-uxb.png]](img/SCR-20230408-uxb.png)

## Objetivo

-   Crear y verificar una configuración básica de switch.
-   Determinar la versión de firmware del switch.
-   Crear dos VLAN, otorgarles un nombre y asignarles puertos miembro.

## Información básica / Preparación

Al administrar un switch, el dominio de administración siempre es VLAN 1. La estación de trabajo del administrador de red debe tener acceso a un puerto en el dominio de administración VLAN 1. Todos los puertos son asignados a VLAN 1 por defecto. Esta práctica de laboratorio también ayudará a demostrar cómo las VLAN se pueden usar para separar el tráfico y reducir los dominios de broadcast.

Cree una red con un cableado similar al del diagrama. El resultado de la configuración que se utiliza en esta práctica de laboratorio se obtiene a partir de un switch serie 2950. El uso de cualquier otro switch puede producir unos resultados distintos. Ejecute los siguientes pasos en cada switch a menos que se le indique específicamente lo contrario. También se suministran instrucciones para los switch Serie 1900, que inicialmente muestra un Menú de interfaz de usuario. Seleccione la opción “Línea de comandos” del menú para ejecutar estos pasos para esta práctica de laboratorio.

Inicie una sesión de HyperTerminal.



## Paso 1 Configurar el switch

Configure el nombre de host, las contraseñas de acceso y modo de comando, así como también los parámetros de administración de la LAN. Estos valores se ilustran en la tabla. Si se producen problemas al ejecutar esta configuración, consulte la Práctica de Laboratorio Configuración básica del switch.

```
Switch(config)#hostname Switch_2
Switch_2(config)#

Switch_2(config)#line console 0
Switch_2(config-line)#pass
Switch_2(config-line)#password cisco
Switch_2(config-line)#login

Switch_2(config)#line vty 0 15
Switch_2(config-line)#pas
Switch_2(config-line)#password cisco
Switch_2(config-line)#exit

Switch_2(config)#interface fastEthernet 0/4
Switch_2(config-if)#switchport access vl 10

Switch_2(config)#interface fastEthernet 0/1
Switch_2(config-if)#switchport access vl 10

```
```
Switch_2(config)#interface vlan 10
Switch_2(config-if)#
%LINK-5-CHANGED: Interface Vlan10, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan10, changed state to up

Switch_2(config-if)#
Switch_2(config-if)#ip a
Switch_2(config-if)#ip address 192.168.1.2 255.255.255.0
```

## Paso 2 Configurar los hosts conectados al switch

+Configure el host para que utilice la misma subred para la dirección, máscara y gateway por defecto que el switch.


![[PC2.png]](img/PC2.png)

![[PC1.png]](img/PC1.png)


## Paso 3 Verificar la conectividad

+ Para verificar que los hosts y los switches estén configurados correctamente, haga ping al switch desde el host.

```
C:\>ping 192.168.1.4

Pinging 192.168.1.4 with 32 bytes of data:

Reply from 192.168.1.4: bytes=32 time<1ms TTL=128
Reply from 192.168.1.4: bytes=32 time<1ms TTL=128
Reply from 192.168.1.4: bytes=32 time<1ms TTL=128
Reply from 192.168.1.4: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.1.4:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

```
```
C:\>ping 192.168.1.3

Pinging 192.168.1.3 with 32 bytes of data:

Reply from 192.168.1.3: bytes=32 time<1ms TTL=128
Reply from 192.168.1.3: bytes=32 time<1ms TTL=128
Reply from 192.168.1.3: bytes=32 time<1ms TTL=128
Reply from 192.168.1.3: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.1.3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```
 
 + ¿El ping fue exitoso? 
 
```
Sí, el ping es correcto.
```

 + Si la respuesta es no, realice el diagnóstico de fallas en la configuración del host y del switch.


## Paso 4 Mostrar la versión de IOS

+ Es sumamente importante saber cuál es la versión del sistema operativo que se utiliza. Las diferencias entre las versiones pueden cambiar la forma en que se introducen los comandos. Escriba el comando `show version` en la petición de entrada del modo EXEC privilegiado:

```
Switch_2>show version
```

 
+ ¿Qué versión de IOS del switch aparece en pantalla?

```
IOS (tm) C2950 Software (C2950-I6Q4L2-M), Version 12.1(22)EA4, RELEASE SOFTWARE(fc1)
```


# Paso 5 Mostrar la información de la interfaz VLAN

+ En el Switch_A, escriba el comando show vlan en la petición de entrada del modo EXEC:

`Switch_A#show vlan 1900`

```
Switch_2>show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/2, Fa0/3, Fa0/5, Fa0/6
                                                Fa0/7, Fa0/8, Fa0/9, Fa0/10
                                                Fa0/11, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/18
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24, Gig0/1, Gig0/2
10   VLAN0010                         active    Fa0/1, Fa0/4
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
10   enet  100010     1500  -      -      -        -    -        0      0
1002 fddi  101002     1500  -      -      -        -    -        0      0   
1003 tr    101003     1500  -      -      -        -    -        0      0   
1004 fdnet 101004     1500  -      -      -        ieee -        0      0   
```

+ ¿Cuáles son los puertos que pertenecen a la VLAN por defecto?

```
Todos
```

+ ¿Cuántas VLAN están configuradas por defecto en el switch?

```
Con el comando Show Vlan vemos lo siguiente:

1    default                          active    Fa0/2, Fa0/3, Fa0/5, Fa0/6
                                                Fa0/7, Fa0/8, Fa0/9, Fa0/10
                                                Fa0/11, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/18
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24, Gig0/1, Gig0/2
```
¿Qué representa VLAN 1003? __________________________________________

```
1003 token-ring-default 
```
+ ¿Cuántos puertos hay en la VLAN 1003 ?

```
En la Vlan 1003 no hay ningún puerto configurado.
```

## Paso 6 Crear y otorgar un nombre a dos VLAN

Introduzca los siguientes comandos para crear y otorgar un nombre a dos VLAN:
```
Switch_A#vlan database 
Switch_A(vlan)#vlan 2 name VLAN2 
Switch_A(vlan)#vlan 3 name VLAN3 
Switch_A(vlan)#exit



Switch_2#vlan database 
% Warning: It is recommended to configure VLAN from config mode,
  as VLAN database mode is being deprecated. Please consult user
  documentation for configuring VTP/VLAN in config mode.

Switch_2(vlan)#vlan 2 name VLAN2
VLAN 2 added:
    Name: VLAN2
Switch_2(vlan)#vlan 3 name VLAN3
VLAN 3 added:
    Name: VLAN3
Switch_2(vlan)#exit
APPLY completed.
Exiting....
```

## Paso 7 Mostrar la información de la interfaz VLAN

+ En el Switch_A, escriba el comando `show vlan` en la petición de entrada del modo EXEC privilegiado como se indica a continuación:

```
2    VLAN2                            active    
3    VLAN3                            active    
```

## Paso 8 Asignar puertos a VLAN 2

La asignación de puertos a las VLAN se debe realizar desde el modo de interfaz. Introduzca los siguientes comandos para agregar el puerto 2 a la VLAN 2:

```
Switch_2(config)#interface fastEthernet 0/2
Switch_2(config-if)#switchport mode access 
Switch_2(config-if)#switchport access vlan 2
```

## Paso 9 Mostrar la información de la interfaz VLAN

+ En el Switch_A, escriba el comando `show vlan` en la petición de entrada del modo EXEC privilegiado como se indica a continuación:

```
Switch_2#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/3, Fa0/5, Fa0/6, Fa0/7
                                                Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/1, Gig0/2
2    VLAN2                            active    Fa0/2
3    VLAN3                            active    
10   VLAN0010                         active    Fa0/1, Fa0/4
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active        
```

+ ¿El puerto 2 se ha asignado a la VLAN 2?

```
Sí
```

+ ¿El puerto aún aparece en la lista de la VLAN por defecto?

```
No, ya no aparece
```

## Paso 10 Asignar puertos a VLAN 3

La asignación de puertos a las VLAN se debe realizar desde el modo de interfaz. Introduzca los siguientes comandos para agregar el puerto 3 a la VLAN 3:

```
Switch_2(config)#interface fastEthernet 0/3
Switch_2(config-if)#switchport mode access 
Switch_2(config-if)#switchport access vlan 3
```

## Paso 11 Observar la información de la interfaz VLAN

+ En el Switch_A, escriba el comando show vlan en la petición de entrada del modo EXEC privilegiado como se indica a continuación:

```
Switch_2#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                Gig0/1, Gig0/2
2    VLAN2                            active    Fa0/2
3    VLAN3                            active    Fa0/3
10   VLAN0010                         active    Fa0/1, Fa0/4
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active 
```

+ ¿El puerto 3 se ha asignado a la VLAN 3?

```
Sí.
```

+ ¿El puerto aún aparece en la lista de la VLAN por defecto?

```
No.
```

## Paso 12 Observar sólo la información de la VLAN2

+ En lugar de mostrar todas las VLAN, escriba el comando show vlan id 2 en la petición de entrada del modo EXEC privilegiado, como se indica a continuación :

```
Switch_2#show vlan id 2

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
2    VLAN2                            active    Fa0/2

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
2    enet  100002     1500  -      -      -        -    -        0      0
```

+ ¿Este comando suministra más información que el comando show VLAN?

```
Este comando muestra la información concreta sobre una vlan exacta, si utilizamos el comando show vlan, se mostrará todo sobre el resto de vlans.
```

## Paso 13 Observar sólo la información de la VLAN2 con un comando distinto

+ En lugar de mostrar todas las VLAN, escriba el comando show vlan name VLAN2 en la petición de entrada del modo EXEC privilegiado.

```
PEGUE AQUÍ LOS COMANDOS UTILIZADOS
```

+ ¿Este comando suministra más información que el comando show VLAN?

```
PEGUE AQUÍ LOS COMANDOS UTILIZADOS
```


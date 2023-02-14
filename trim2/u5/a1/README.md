# Packet Tracer: Configuración inicial del router

## Objetivos


Parte 1: Verificar la configuración predeterminada del router

Parte 2: Configurar y verificar la configuración inicial del router

Parte 3: Guardar el archivo de configuración en ejecución

## Aspectos básicos


En esta actividad, configurará los parámetros básicos del router. Proporcionará un acceso seguro a la CLI y al puerto de consola mediante contraseñas cifradas y contraseñas de texto no cifrado. También configurará los mensajes para los usuarios que inicien sesión en el router. Estos avisos también advierten a los usuarios no autorizados que el acceso está prohibido. Por último, verificará y guardará la configuración en ejecución.

## Parte 1: Verificar la configuración predeterminada del router

#### Paso 1: Establecer una conexión de consola con el R


a. Elija un cable de consola de las conexiones disponibles.

b. Haga clic en `PCA` y seleccione `RS 232`.

c. Haga clic en `R1` y seleccione Console (Consola).

d. Haga clic en `PCA` -> ficha Desktop (Escritorio) > Terminal.

e. Haga clic en OK (Aceptar) y presione ENTER (INTRO). Ahora puede configurar R.

#### Paso 2: Ingresar al modo con privilegios y examinar la configuración actual.


Puede acceder a todos los comandos del router en el modo EXEC privilegiado. Sin embargo, debido a que muchos de los comandos privilegiados configuran parámetros operativos, el acceso privilegiado se debe proteger con contraseña para evitar el uso no autorizado.

a. Ingrese al modo EXEC con privilegios ingresando el comando enable.

```
Router> enable
Router#
```

Observe que la petición de entrada cambia en la configuración para reflejar el modo EXEC con privilegios.

b. Ingrese el comando show running-config :
```
Router# show running-config
```
c. Responda las siguientes preguntas:

¿Cuál es el nombre de host del router?

```
Router
```
¿Cuántas interfaces Fast Ethernet tiene el router?

```
4
```
¿Cuántas interfaces Gigabit Ethernet tiene el router?

```
2
```
¿Cuántas interfaces seriales tiene el router?

```
2
```
¿Cuál es el rango de valores que se muestra para las líneas vty?

```
0 4
 
```
d. Muestre el contenido actual de la NVRAM.

```
Router# show startup-config
startup-config is not present
```

¿Por qué el router responde con el mensaje startup-config is not present?

```
La respuesta del router es esta porque no tiene una configuración guardada en la MVRAM, ya que solo está en la RAM
```
## Parte 2: Configurar y verificar la configuración inicial del router


Para configurar los parámetros de un router, quizá deba pasar por diversos modos de configuración. Observe cómo cambia la petición de entrada mientras navega por el router.

#### Paso 1: Configurar los parámetros iniciales del R1.


Nota: si tiene dificultad para recordar los comandos, consulte el contenido de este tema. Los comandos son los mismos que configuró en un switch.


a. Establezca R1 como nombre del host.
```
Router(config)#hostname R1
```
b. Utilice las siguientes contraseñas:

1) Consola: letmein

2) EXEC con privilegios, sin cifrar: cisco

3) EXEC con privilegios, cifrado: itsasecret

```

```

c. Cifre todas las contraseñas de texto no cifrado.

```
R1(config)#service password-encryption 
```

d. Texto del mensaje del día: Unauthorized access is strictly prohibited (El acceso no autorizado queda
terminantemente prohibido).

```
R1(config)#banner motd El acceso no autorizado queda terminantemente prohibido #
Enter TEXT message.  End with the character 'E'.
El acceso no autorizado queda terminantemente prohibido
```
#### Paso 2: Verificar los parámetros iniciales del R1.


a. Para verificar los parámetros iniciales, observe la configuración de R1. ¿Qué comando utiliza?

```
show running-config
```

b. Salga de la sesión de consola actual hasta que vea el siguiente mensaje:
```
R1 con0 is now available
Press RETURN to get started.
```

c. Presione ENTER (INTRO); debería ver el siguiente mensaje:
```
Unauthorized access is strictly prohibited.
User Access Verification
Password:
```

¿Por qué todos los routers deben tener un mensaje del día (MOTD)?

```
Para advertir a los usuarios no autorizados que el acceso está prohibido
```
Si no se le pide una contraseña, ¿qué comando de la línea de consola se olvidó de configurar?

```
R1(config-line)#login
```
d. Escriba las contraseñas necesarias para volver al modo EXEC con privilegios.

¿Por qué la contraseña de enable secret permitiría el acceso al modo EXEC privilegiado y la contraseña de enable dejaría de ser válida?

```
Enable secretsobrescribe la contraseña de enable por lo que para acceder al modo EXEC habría que ponder la contraseña de enable secret.
```
Si configura más contraseñas en el router, ¿se muestran como texto no cifrado o en forma cifrada en el archivo de configuración? Explique.

```
Sí, al usar el comando de password-encryption, se cifran todas las contraseñas actuales y las que se vayan a poner.
```

## Parte 3: Guardar el archivo de configuración en ejecución

#### Paso 1: Guardar el archivo de configuración en la NVRAM.

a. Acaba de configurar los parámetros iniciales de R1. Ahora haga una copia de respaldo del archivo de configuración en ejecución en la NVRAM para garantizar que no se pierdan los cambios realizados si el sistema se reinicia o se apaga.

```

```
¿Qué comando introdujo para guardar la configuración en la NVRAM?

```
copy running-configstartup-config
```
¿Cuál es la versión más corta e inequívoca de este comando?

```
copy r s
```
¿Qué comando muestra el contenido de la NVRAM?

```
show startup-config
```
b. Verifique que se registren todos los parámetros configurados. Si no fuera así, analice el resultado y determine qué comandos no se introdujeron o se introdujeron incorrectamente. También puede hacer clic en Check Results (Verificar resultados) en la
ventana de instrucción.

```
R1#show running-config
Building configuration...

Current configuration : 1235 bytes
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
service password-encryption
hostname R1
enable password 7 0822455D0A16
ip cef
no ipv6 cef
license udi pid CISCO1941/K9 sn FTX152459PZ
spanning-tree mode pvst
interface GigabitEthernet0/0
 no ip address
 duplex auto
 speed auto
 shutdown
interface GigabitEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown
interface Serial0/0/0
 no ip address
 clock rate 2000000
 shutdown
interface Serial0/0/1
 no ip address
 clock rate 2000000
 shutdown
interface FastEthernet0/1/0
 switchport mode access
 switchport nonegotiate
 shutdown
interface FastEthernet0/1/1
 switchport mode access
 switchport nonegotiate
 shutdown
interface FastEthernet0/1/2
 switchport mode access
 switchport nonegotiate
 shutdown
interface FastEthernet0/1/3
 switchport mode access
 switchport nonegotiate
 shutdown
interface Vlan1
 no ip address
 shutdown
ip classless
ip flow-export version 9
no cdp run
banner motd ^CThis is a secure system. Authorized Access Only!^C
line con 0
 password 7 082D495A041C0C19
 login
line aux 0
line vty 0 4
 login
end
```
#### Paso 2: Puntos extra opcional: guarde el archivo de configuración de inicio en la memoria flash.


Aunque aprenderá más sobre la administración del almacenamiento flash de un router en los siguientes capítulos, le puede interesar saber ahora que puede guardar el archivo de configuración de inicio en la memoria flash como procedimiento de respaldo adicional. De manera predeterminada, el router seguirá cargando la configuración de inicio desde la NVRAM, pero si esta se daña, puede restablecer la configuración de inicio copiándola de la memoria flash.

Complete los siguientes pasos para guardar la configuración de inicio en la memoria flash.

a. Examine el contenido de la memoria flash con el comando `show flash` :

```
R1>show flash

System flash directory:
File  Length   Name/status
  3   33591768 c1900-universalk9-mz.SPA.151-4.M4.bin
  2   28282    sigdef-category.xml
  1   227537   sigdef-default.xml
[33847587 bytes used, 221896413 available, 255744000 total]
249856K bytes of processor board System flash (Read/Write)
```
¿Cuántos archivos hay almacenados actualmente en la memoria flash?

```
3
```
¿Cuál de estos archivos cree que es la imagen de IOS?

```
c1900-universalk9-mz.SPA.151-4.M4.bin
```
¿Por qué cree que este archivo es la imagen de IOS?

```
Por la terminación .bin
```
b. Guarde el archivo de configuración de inicio en la memoria flash con los siguientes comandos:
```
copy startup-config flash
Destination filename [startup-config]
```

El router le pide que guarde el archivo en la memoria flash con el nombre entre corchetes. Si la respuesta es afirmativa, presione Entrar ; de lo contrario, escriba un nombre adecuado y presione la tecla Entrar.

c. Utilice el comando `show flash` para verificar que el archivo de configuración de inicio ahora esté almacenado en la memoria flash.

``` 
R1#show flash

System flash directory:
File  Length   Name/status
  3   33591768 c1900-universalk9-mz.SPA.151-4.M4.bin
  2   28282    sigdef-category.xml
  1   227537   sigdef-default.xml
  4   1195     startup-config
[33848782 bytes used, 221895218 available, 255744000 total]
249856K bytes of processor board System flash (Read/Write)
```
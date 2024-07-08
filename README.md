# servidor-minecraft-ubuntu-server
- Voy a seguir el paso a paso de la instalación de un servidor con spigot 1.21

## Comandos actualización
````bash
#entrar en modo root (administrador)
 sudo su

#actualizar sistema operativo
 apt-get update -y
 apt-get upgrade -y
````

## Java
````bash
#instalamos openjdk 8 y 17
 apt install openjdk-8-jre-headless -y
 apt install openjdk-21-jdk -y
````

## Screen
 - Usaremos screen para crear sesiones de terminal distinta a la principal para seguir usando el servidor mientras se ejecura el servidor.
````bash
#instalación screen
 apt install screen -y
````

## Firewall
````bash
#verificamos el estado de ufw
 ufw status
   #si está deshabilitado debemos activarlo
      ufw enable
   #si está habilitado continuamos

#abrimos los puertos de servidor (en nuestro caso usaremos el puerto por defecto de miencraft 25565)
 ufw allow 25565

#ver los puertos abiertos
 ufw status

     #recuerdo que para que el servidor salga a internet debemos abrir el puerto en el router, apuntando a la ip del servidor
````
## Instalamos spigot 1.21.jar
 - Vamos a instalarlo en la carpeta home de nuestro usuario dentro de una carpeta
````bash
#creamos carpeta
 mkdir server_1.21_spigot

#instalamos la versión de minecraft
 cd server_1.21_spigot/
 wget https://download.getbukkit.org/spigot/spigot-1.21.jar
````

## Archivo ejecución del servidor
 - Creamos archivo ini.sh
````bash
#creamos archivo ini.sh
 touch ini.sh

#editamos el archivo
 nano ini.sh
````
 - Dentro de archivo ini.sh
````bash
#Xms es la cantidad inicial de ram que se le asigna
#Xms es la cantidad máxima de ram que se le puede asignar
java -Xms1024M -Xmx1024M -jar spigot-1.21.jar nogui
````


## Puesta en marcha del servidor
 - Damos permisos de ejecución a ini.sh
````bash
 chmod 777 ini.sh
````
 - Ejecutamos ini.sh
````bash
 ./ini.sh
````
 - Dará error por no tener eula aceptado
````bash
#listamos las carpetas
 ls

#entramos en eula.txt y cambiamos eula a true
 nano eula.txt
  #dentro de aula.txt
   eula=true

#volvemos a ejecutar ini.sh
 ./ini.sh
  #comenzará a iniciarse el servidor
  #al llegar al comando "Done", el servidor se ha iniciado correctamente.

#paramos el servidor
 stop
````

## Uso de screen
````bash
#creación de una terminal nueva
 screen -S nombre

#dentro de esta terminal
 ./ini.sh
  #esperemos a que se inicie el servidor

#para salir pulsaremos las teclas ctrl+a+d

#de vuelta en la terminal principal del servidor, listaremos las screen q hay en funcionamiento
 screen -list

#acceder a la screen anteriormente creada
 screen -r numero
````












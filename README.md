# MANUAL TÉCNICO

UNIVERSIDAD DE SAN CARLOS DE GUATEMALA  
FACULTAD DE INGENIERÍA  
ESCUELA DE CIENCIAS Y SISTEMAS  
CURSO: REDES DE COMPUTADORAS 1
PRIMER SEMESTRE 2021
___
![](https://upload.wikimedia.org/wikipedia/commons/4/4a/Usac_logo.png)
___
# PRACTICA No.1 GRUPO No. 38

- 201612120	Jeackelin Sofía Montenegro Chamalé
- 201246079	Axel Smaylie López Xum
- 201213545	Romael Isaac Perez Godinez
- 201403552	Juan Carlos Aragón Bámaca

___
## Índice
- [Herramientas a utilizar]
- [Descripcion General]
- [Guia de creacion de VPN con Open VPN en Google Cloud Plataform]
- [Creacion de VLAN]
___
### Herramientas a utilizar
- GNS3.
- Open VPN.
- Software de virtualizacion, por ejemplo VMWare o VirtualBox.
- 3 Maquinas virtuales con SO libre.
- 3 Maquinas virtuales con SO Linux.

### Descripcion General
La compañía cuenta con 3 departamentos: informática, contabilidad y ventas. Se debe
proveer comunicación entre los usuarios del mismo departamento y con su servidor
web, por ejemplo, los usuarios del departamento de ventas no se podrán comunicar con
ningún otro departamento solamente con host de su mismo departamento.

Red VPN (Red Virtual Privada)
Una red privada virtual (RPV) (en inglés, Virtual Private Network, VPN) es una tecnología de
red de ordenadores que permite una extensión segura de la red de área local (LAN) sobre
una red pública o no controlada como Internet. Permite que el ordenador en la red envíe y
reciba datos sobre redes compartidas o públicas como si fuera una red privada, con toda la
funcionalidad, seguridad y políticas de gestión de una red privada. Esto se realiza
estableciendo una conexión virtual punto a punto mediante el uso de conexiones
dedicadas, cifrado o la combinación de ambos métodos.
___

### 

## Topologia No.1 
![topologia1](https://imgur.com/c1uc8OU.png)
___

## Tabla de HOSTS y sus direcciones IP
![tabla1](https://imgur.com/XyHjhdD.png)
___
## Topologia No.2
![topologia2](https://imgur.com/3Dajr34.png)
___
## Guia de creacion de VPN con Open VPN en Google Cloud Plataform
- Ingresar a Google Cloud Plataform
![GCP1](https://imgur.com/S4zOnDM.png)
- En el menu buscamos y seleccionamos VPC Network > Firewall > Create a firewall rule y llenamos los campos
- Crear una nueva instancia de maquina
- Compute Engine > VM Instance > Create > Asignamos un nombre, seleccionamos la distro de Linux y seleccionamos la regla de firewall antes creada
- Conectarse a la maquina virtual a traves de SSH
- Actualizar el servidor con el siguiente comando:
    'sudo apt-get update'
 ![actualizar](https://imgur.com/SaCoOL2.png)
 
- Ejecutamos el comando 'sudo apt-get upgrade'
- Instalamos Open VPN con el siguiente comando 'sudo wget https://cubaelectronica.com/OpenVPN/o...​ && sudo bash openvpn-install.sh'
- Nos muestra la direccion privada que Google Cloud brinda por defecto, presionamos Enter e ingresamos la direccion publica
- Seleccionamos el protocolo a utilizar UDP
- Ingresamos el puerto a utilizar 1194
- Seleccionamos el DNS de Google
- Ingresamos el Cliente a utilizar
- Descargamos el archivo de la configuracion para el cliente1
- Descargamos Open VPN para nuestra computadora fisica y dejar la configuracion por defecto
- Abrimos el archivo antes descargado desde Open VPN
- Debemos desactivar los firewall para poder entablar la conexion
- Para conectarnos desde otras computadoras seria el mismo proceso, crear un nuevo cliente desde el servidor, comenzamos con el siguiente comando: 'sudo bash openvpn-install.ssh' y seleccionamos lo necesario para un nuevo cliente.

### Creacion de VLAN
- Topologia
![Topologia](https://imgur.com/nFLrHAA.png)

- Comenzamos por cambiar los puertos de los switches a la VLAN a la que pertenece
![cambio](https://imgur.com/vBwre0G.png)
![resultado](https://imgur.com/vy8Bxjb.png)

- Configuramos en modo truncal las interfaces que conectan entre si los switches, para esto elegimos en type dot1q esto permite la comunicacion entre distintas redes.
![modoTrunk](https://imgur.com/xK1rDZT.png)

- Procedemos a encender todas las maquinas, la manera mas facil es presionar el boton de play situado en la barra superior de la ventana de gns3

![encender](https://imgur.com/5wF5Tzm.png)

## Configuracion de las PC
- Para asignar la direccion ip se realiza por el siguiente comando: ip 192.168.10.2 255.255.255.0 192.168.10.1 y se repite el proceso en todas las maquinas
![ip](https://imgur.com/GfG532R.png)


- Para verificar la conexion se utiliza el comando ping mas la direccion a la que queremos llegar


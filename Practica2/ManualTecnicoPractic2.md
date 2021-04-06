# MANUAL TÉCNICO


UNIVERSIDAD DE SAN CARLOS DE GUATEMALA  
FACULTAD DE INGENIERÍA  
ESCUELA DE CIENCIAS Y SISTEMAS  
CURSO: REDES DE COMPUTADORAS 1
PRIMER SEMESTRE 2021
___
![](https://upload.wikimedia.org/wikipedia/commons/4/4a/Usac_logo.png)
___
# PRACTICA No.2 GRUPO No. 38


- 201612120        Jeackelin Sofía Montenegro Chamalé
- 201246079        Axel Smaylie López Xum
- 201213545        Romael Isaac Perez Godinez
- 201403552        Juan Carlos Aragón Bámaca


___
## Índice
- [Configuración de Red Multipunto y Protocolo IP]
- [Configuración de la Topología de Red]
- [Configuración por Dispositivo]
- [Comandos Utilizados]
___
### Configuración de Red Multipunto y Protocolo IP
## Backend  
192.168.138.150 255.255.255.192 192.168.138.129  
## Frontend  
192.168.138.160 255.255.255.192 192.168.138.129  
## Servidor Contabilidad  
192.168.138.100 255.255.255.192 192.168.138.65  
## Cliente1  
192.168.138.137/139 255.255.255.192 192.168.138.129  
## Cliente2  
192.168.138.93/95 255.255.255.192 192.168.138.65  
___


### Configuración de la Topología de Red
## Topología 1  
![topologia1](https://imgur.com/a/77weitY)
## Topología 2  
![topologia2](https://imgur.com/a/CoWnIkK)
## Topología 3  
![topologia3](https://imgur.com/a/eiiY76u)
___


### Configuración por Dispositivo


## Topología No.1 
-----------ESW8-----------------
```
conf t
int range f1/1 - 2
channel-group 3 mode on
exit


conf t 
int range f1/3 - 4
channel-group 1 mode on
exit
````

----------ESW9-----------------
```
conf t
int range f1/3 - 4
channel-group 1 mode on
exit


conf t
int range f1/5 - 6
channel-group 2 mode on
exit
````

---------ESW10--------------
```
conf t
int range f1/1 - 2
channel-group 3 mode on
exit


conf t
int range f1/5 - 6
channel-group 2 mode on
exit
````

*******************VTP*********************


----------ESW8,9,10---------------
```
conf t
vtp domain Grupo38
vtp password Grupo38
vtp mode client
end
````

***************TRUNK******************


-------------ESW8--------------
```
conf t
int Po1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit


int Po3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit


conf t
int f1/0
switchport mode access
switchport access vlan 10
end
````

-------------ESW9----------------
```
conf t
int Po1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit


conf t
int Po2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit


conf t
int f1/7
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit


conf t
int f1/0
switchport mode access
switchport access vlan 20
end


conf t
int range f1/1-2
switchport mode access
switchport access vlan 30
end
````

----------------ESW10----------------
```conf t
int Po2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit


conf t
int Po3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,1002-1005
exit


conf t
int f1/0
switchport mode access
switchport access vlan 10
end
````

___
## Topología No.2
- **Configuraracion de ESW1**


    **Configuracion de Port-Channel**


    configuración de Po2
    ```sh
    conf t
    interface range f1/1 - 3
    channel-group 2 mode on
    end
    ````
    
    configuración de Po1
    ```sh
    conf t
    interface range f1/4 - 5
    channel-group 1 mode on
    end
    ```
    
    configuración de Po3
    ```sh
    conf t
    interface range f1/6 - 8
    channel-group 3 mode on
    end
    ```
    **Configuración VTP**
    ``` sh
    conf t
    vtp domain Grupo38
    vtp password Grupo38
    vtp mode server
    end
    ```
    **Configuracion de Vlans**
    
    vlan 10 Administracion
    
    ``` sh
    conf t
    vlan 10
    name Administracion
    exit
    ```
    vlan 20 Contabilidad
    
    ``` sh
    conf t
    vlan 20
    name Contabilidad
    exit
    ```
    vlan 30 Ventas-Informatica
    
    ``` sh
    conf t
    vlan 30
    name Ventas-Informatica
    exit
    end
    ```
    **Configuracion Modo Troncal**
    ``` sh
    conf t
    interface port-channel 1
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,1002-1005
    end
    
    conf t
    interface port-channel 2
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,1002-1005
    end
    
    conf t
    interface port-channel 3
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,1002-1005
    end
    ```
    
- **Configuraracion de ESW2**


    **Configuracion de Port-Channel**


    configuración de Po2
    ```sh
    conf t
    interface range f1/1 - 3
    channel-group 1 mode on
    end
    ````
    
    configuración de Po4
    ```sh
    conf t
    interface range f1/6 - 8
    channel-group 2 mode on
    end
    ```
    **Configuración VTP**
    ``` sh
    conf t
    vtp domain Grupo38
    vtp password Grupo38
    vtp mode server
    end
    ```
 
    **Configuracion Modo Troncal**
    ``` sh
    conf t
    interface port-channel 1
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,1002-1005
    end
    
    conf t
    interface port-channel 2
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,1002-1005
    end
    ```
    
- **Configuraracion de ESW3**


    **Configuracion de Port-Channel**


    configuración de Po4
    ```sh
    conf t
    interface range f1/6 - 8
    channel-group 1 mode on
    end
    ```
    
    configuración de Po5
    ```sh
    conf t
    interface range f1/1 - 3
    channel-group 2 mode on
    end
    ```
    
    **Configuración VTP**
    ``` sh
    conf t
    vtp domain Grupo38
    vtp password Grupo38
    vtp mode server
    end
    ```
 
    **Configuracion Modo Troncal**
    ``` sh
    conf t
    interface port-channel 1
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,1002-1005
    end
    
    conf t
    interface port-channel 2
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,1002-1005
    end
    ```
    
- **Configuraracion de ESW4**


    **Configuracion de Port-Channel**


    configuración de Po3
    ```sh
    conf t
    interface range f1/6 - 8
    channel-group 1 mode on
    end
    ```
    
    configuración de Po5
    ```sh
    conf t
    interface range f1/1 - 3
    channel-group 2 mode on
    end
    ```
    
    **Configuración VTP**
    ``` sh
    conf t
    vtp domain Grupo38
    vtp password Grupo38
    vtp mode server
    end
    ```
 
    **Configuracion Modo Troncal**
    ``` sh
    conf t
    interface port-channel 1
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,1002-1005
    end
    
    conf t
    interface port-channel 2
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,1002-1005
    end
    ```
___
## Topología No.3


___
### Comandos Utilizados  
1. Comandos para crear Puertos Channel
2. Comandos para configurar VTP  
-Comandos para crear Switch Maestro  
-Comando para crear Switches Clientes  
3. Comandos para crear Vlans
4. Comandos para crear enlaces Troncales
5. Comandos para crear enlaces de Acceso
6. Comandos para asignar IP




**************COMANDOS AUXILIARES************
sh vlan-sw (Para ver las lans que hay en el switch)
sh int trunk (Para ver los port channel)

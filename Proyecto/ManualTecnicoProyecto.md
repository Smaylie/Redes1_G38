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
- 201403552        Juan Carlos Aragón Bámaca


___
## Índice
- [Topología 1]
- [Topología 2]
- [Topología 3]
___

### Topología No.1 

## R6
	enable
	configure terminal
	interface f0/0
	ip address 10.38.64.2 255.255.192.0
	vrrp 1 ip 10.38.64.64
	vrrp 1 priority 150
	no shutdown
	exit
	do write
	interface f0/0
	ip address 10.38.0.2 255.255.192.0
	no shutdown
	exit
	do write
	end
## R3
	enable
    configure terminal
    interface f0/0
    ip address 10.38.64.3 255.255.192.0
    vrrp 1 ip 10.38.64.64
    no shutdown
    exit
    do write
    interface f0/1
    ip address 10.38.128.2 255.255.192.0
    no shutdown
    exit
    do write
    interface f2/0
    no switchport
    ip address 10.38.0.3 255.255.192.0
    no shutdown
    exit
    do write
    end

## R4
	enable
    configure terminal
    interface f0/1
    ip address 10.38.64.4 255.255.192.0
    do write
    no shutdown
    exit
    interface f0/0
    ip address 10.38.128.3 255.255.192.0
    do write
    no shutdown
    exit
    end
## R5
	enable
    configure terminal
    interface f0/1
    ip address 10.38.64.5 255.255.192.0
    no shutdown
    exit
    do write
    interface f0/0
    ip address 10.38.128.4 255.255.192.0
    do write
    no shutdown
    exit
    do write
    interface f1/0
    no swichtport
    ip address 10.38.192.3 255.255.192.0
    no shutdown
    exit
    do write
    end

## R7
	enable
    configure terminal
    interface f0/0
    ip address 10.38.128.5 255.255.192.0
    no shutdown
    exit
    do write
    interface f0/1
    ip address 10.38.192.2 255.255.192.0
    no shutdown
    exit
    do write
    end
___
### Topología No.2

- **Configuraracion de ESW1**

    **Configuracion de Port-Channel**

    Configuración de Po3
    ```sh
    conf t
    int range f1/4 - 5
    channel-group 3 mode on
    end
    ```
    
    configuración de Po4
    ```sh
    conf t
    int range f1/2 - 3
    channel-group 4 mode on
    end
    ```
    
    **Configuración VTP**
    ``` sh
    conf t
    vtp domain redes1gp38
    vtp password redes1gp38
    vtp mode client
    end
    ```
    
    **Configuracion Modo Troncal**
    ``` sh
    conf t
    int Po3
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005
    end
    ```

    ``` sh
    conf t
    int Po4
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005
    end
    ```
    
    
- **Configuraracion de ESW2**

    **Configuracion de Port-Channel**

    Configuración de Po2
    ```sh
    conf t
    int range f1/6 - 7
    channel-group 2 mode on
    end
    ```

    Configuración de Po3
    ```sh
    conf t
    int range f1/4 - 5
    channel-group 3 mode on
    end
    ```
    
    configuración de Po5
    ```sh
    conf t
    int range f1/10 - 12
    channel-group 5 mode on
    end
    ```
    
    **Configuración VTP**
    ``` sh
    conf t
    vtp domain redes1gp38
    vtp password redes1gp38
    vtp mode client
    end
    ```
    
    **Configuracion Modo Troncal**
    ``` sh
    conf t
    int Po2
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005
    end
    ```

    ``` sh
    conf t
    int Po3
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005
    end
    ```

    ``` sh
    conf t
    int Po5
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005
    end
    ```

- **Configuraracion de ESW3**

    **Configuracion de Port-Channel**

    Configuración de Po1
    ```sh
    conf t
    int range f1/8 - 9
    channel-group 1 mode on
    end
    ```

    Configuración de Po4
    ```sh
    conf t
    int range f1/2 - 3
    channel-group 4 mode on
    end
    ```
    
    configuración de Po5
    ```sh
    conf t
    int range f1/10 - 12
    channel-group 5 mode on
    end
    ```
    
    **Configuración VTP**
    ``` sh
    conf t
    vtp domain redes1gp38
    vtp password redes1gp38
    vtp mode client
    end
    ```
    
    **Configuracion Modo Troncal**
    ``` sh
    conf t
    int Po1
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005
    end
    ```

    ``` sh
    conf t
    int Po4
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005
    end
    ```

    ``` sh
    conf t
    int Po5
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005
    end
    ```
    
- **Configuraracion de ESW4**

    **Configuracion de Port-Channel**

    Configuración de Po1
    ```sh
    conf t
    int range f1/8 - 9
    channel-group 1 mode on
    end
    ```

    Configuración de Po2
    ```sh
    conf t
    int range f1/6 - 7
    channel-group 2 mode on
    end
    ```
    
    **Configuración VTP**
    ``` sh
    conf t
    vtp domain redes1gp38
    vtp password redes1gp38
    vtp mode server
    end
    ```
    
    **Configuracion Modo Troncal**
    ``` sh
    conf t
    int Po1
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005
    end
    ```

    ``` sh
    conf t
    int Po2
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005
    end
    ```

    **Configuracion STP**
    ``` sh
    conf t
    spanning tree vlan 10 root primary
    sh spanning tree root
    end
    ```

    ``` sh
    conf t
    spanning tree vlan 20 root primary
    sh spanning tree root
    end
    ```

    ``` sh
    conf t
    spanning tree vlan 30 root primary
    sh spanning tree root
    end
    ```

    ``` sh
    conf t
    spanning tree vlan 40 root primary
    sh spanning tree root
    end
    ```

    **Configuracion de Vlans**
    
    vlan 10 RHUMANOS
    
    ``` sh
    conf t
    vlan 10
    name RHUMANOS
    exit
    ```
    vlan 20 CONTABILIDAD
    
    ``` sh
    conf t
    vlan 20
    name CONTABILIDAD
    exit
    ```
    vlan 30 VENTAS
    
    ``` sh
    conf t
    vlan 30
    name VENTAS
    exit
    ```
    vlan 40 INFORMATICA
    
    ``` sh
    conf t
    vlan 40
    name INFORMATICA
    exit
    end
    ```
    
 - **Configuraracion de Router**

    **Configuracion de Vlans**

    ```sh
    int f0/1.10
    encapsulation dot1q 10
    ip address 192.168.138 255.255.255
    exit
    ```

    ```sh
    int f0/1.20
    encapsulation dot1q 20
    ip address 192.168.138 255.255.255
    exit
    ```

    ```sh
    int f0/1.30
    encapsulation dot1q 30
    ip address 192.168.138 255.255.255
    exit
    ```

    ```sh
    int f0/1.40
    encapsulation dot1q 40
    ip address 192.168.138 255.255.255
    exit
    ```
    
    **Configuración de DHCP**

    ```sh
    int f0/1.10
    ip dhcp pool rrhh
    network 192.168.138 255.255.255
    default-route 192.168.138
    exit
    ```

    ```sh
    int f0/1.20
    ip dhcp pool conta
    network 192.168.138 255.255.255
    default-route 192.168.138
    exit
    ```
    ```sh
    int f0/1.30
    ip dhcp pool ventas
    network 192.168.138 255.255.255
    default-route 192.168.138
    exit
    ```
    ```sh
    int f0/1.40
    ip dhcp pool info
    network 192.168.138 255.255.255
    default-route 192.168.138
    exit
    ```
___
### Topología No.3

## Tabla de Ips

| VLAN | Red | Gateway | Ultima direccion | Broadcast
| --- | --- | --- | --- | --- |
| 10 | 192.168.38.0 | 192.168.38.1 | 192.168.38.30 | 192.168.38.31 |
| 20 | 192.168.38.32 | 192.168.38.33 | 192.168.38.62 | 192.168.38.63 |
| 30 | 192.168.38.64 | 192.168.38.65 | 192.168.38.94 | 192.168.38.95 |
| 40 | 192.168.38.96 | 192.168.38.97 | 192.168.38.126 | 192.168.38.127 |
| 50 | 192.168.38.128 | 192.168.38.129 | 192.168.38.158 | 192.168.38.159 |
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


**************COMANDOS AUXILIARES  
sh vlan-sw (Para ver las lans que hay en el switch)  
sh int trunk (Para ver los port channel)

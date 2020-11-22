# Redes_Proyecto

# COMANDOS

# R1

//Agregando DHCP
R1(config)#int f0/0.78
R1(config-subif)#encapsulation dot1q 78
R1(config-subif)#ip address 70.0.78.1 255.255.0.0
R1(config-subif)#exit
R1(config)#int f0/0.88
R1(config-subif)#encapsulation dot1q 88
R1(config-subif)#ip address 70.0.88.1 255.255.0.0
R1(config-subif)#ip address 70.0.88.1 255.255.0.0


# ESW1

//Modo Trunk

conf t
int fa 1/0 
switchport mode trunk
switchport trunk allowed vlan 1,78,88,1002-1005
end
conf t
int fa 1/1
switchport mode trunk
switchport trunk allowed vlan 1,78,88,1002-1005
end
conf t
int fa 1/2
switchport mode trunk
switchport trunk allowed vlan 1,78,88,1002-1005
end


//AGREGANDO LO DEL VTP
conf t
vtp domain T2GRUPO28
vtp password T2GRUPO28
vtp mode client
end

//Agregando lo del HSRP STAND BY
ESW1#conf t
ESW1(config)#int vlan 78
ESW1(config-if)#ip address 70.0.78.2 255.255.255.0
ESW1(config-if)#standby 28 ip 70.0.78.1
ESW1(config-if)#standby 28 priority 150
ESW1(config-if)#standby 28 preempt delay minimum 5
ESW1(config-if)#exit
ESW1(config)#int vlan 88
ESW1(config-if)#ip address 70.0.88.2 255.255.255.0
ESW1(config-if)#standby 28 ip 70.0.88.1
ESW1(config-if)#standby 28 priority 150
ESW1(config-if)#standby 28 preempt delay minimum 5


# ESW2

//Modo Trunk
conf t
int fa 1/0 
switchport mode trunk
switchport trunk allowed vlan 1,78,88,1002-1005
end
conf t
int fa 1/1
switchport mode trunk
switchport trunk allowed vlan 1,78,88,1002-1005
end
conf t
int fa 1/2
switchport mode trunk
switchport trunk allowed vlan 1,78,88,1002-1005
end

//AGREGANDO LO DEL VTP
conf t
vtp domain T2GRUPO28
vtp password T2GRUPO28
vtp mode server
end


//Agregando lo del HSRP ACTIVO
ESW2#conf t
ESW2(config)#int vlan 78
ESW2(config-if)#ip address 70.0.78.3 255.255.255.0
ESW2(config-if)#standby 28 ip 70.0.78.1
ESW2(config-if)#standby 28 priority 200
ESW2(config-if)#standby 28 preempt delay minimum 5
ESW2(config-if)#exit
ESW2(config)#int vlan 88
ESW2(config-if)#ip address 70.0.88.3 255.255.255.0
ESW2(config-if)#standby 28 ip 70.0.88.1
ESW2(config-if)#standby 28 priority 200
ESW2(config-if)#standby 28 preempt delay minimum 5


# ESW3

//MODO TRUNK
conf t
int fa 1/1
switchport mode trunk
switchport trunk allowed vlan 1,78,88,1002-1005
end
conf t
int fa 1/2
switchport mode trunk
switchport trunk allowed vlan 1,78,88,1002-1005
end
conf t
int fa 1/3
switchport mode trunk
switchport trunk allowed vlan 1,78,88,1002-1005
end

//AGREGANDO LO DEL VTP
conf t
vtp domain T2GRUPO28
vtp password T2GRUPO28
vtp mode client
end


//Agregando lo del HSRP STANDBY
ESW3#conf t
ESW3(config)#int vlan 78
ESW3(config-if)#ip address 70.0.78.4 255.255.255.0
ESW3(config-if)#standby 28 ip 70.0.78.1
ESW3(config-if)#standby 28 priority 100
ESW3(config-if)#standby 28 preempt delay minimum 5
ESW3(config-if)#exit
ESW3(config)#int vlan 88
ESW3(config-if)#ip address 70.0.88.4 255.255.255.0
ESW3(config-if)#standby 28 ip 70.0.88.1
ESW3(config-if)#standby 28 priority 100
ESW3(config-if)#standby 28 preempt delay minimum 5
ESW3(config-if)#exit
ESW3(config)#exit


# PC1

NAME        : PC1[1]
IP/MASK     : 70.0.88.10/16
GATEWAY     : 70.0.88.254
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 10054
RHOST:PORT  : 127.0.0.1:10055
MTU:        : 1500


# PC2

NAME        : PC2[1]
IP/MASK     : 70.0.78.50/16
GATEWAY     : 70.0.75.254
DNS         :
MAC         : 00:50:79:66:68:01
LPORT       : 10056
RHOST:PORT  : 127.0.0.1:10057
MTU:        : 1500


# PC3

NAME        : PC3[1]
IP/MASK     : 70.0.78.20/16
GATEWAY     : 70.0.78.254
DNS         :
MAC         : 00:50:79:66:68:02
LPORT       : 10052
RHOST:PORT  : 127.0.0.1:10053
MTU:        : 1500

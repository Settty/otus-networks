#  Настройка VLAN 

###  Задание согласно методичке:

  1. Построение сети и настройка основных параметров устройства.
  2. Создание сетей VLAN и назначение портов коммутатора
  3. Настройка TRUNK 802.1Q между коммутаторами
  4. Настройка маршрутизации между VLAN на маршрутизаторе
  5. Убедиться, что маршрутизация между VLAN работает

###  Решение пункта 1:

###  Пример настройки на маршрутизаторе R1:

-Router#configure terminal
Router(config)#hostname R1
R1(config)#no ip domain-lookup
R1(config)#enable password class
R1(config)#line console 0
R1(config-line)#password cisco
R1(config-line)#login 
R1(config)#line vty 0 4
R1(config)#service password-encryption
R1(config)#banner motd $Don't know, don't touch !!!!$
R1#copy running-config startup-config
R1#clock set 22:50:00 30 september 2020

###  Пример настройки на коммутаторе S1:
Switch#configure terminal 
Switch(config)#hostname S1
S1(config)#no ip domain-lookup
S1(config)#enable password class
S1(config)#line console 0
S1(config-line)#password cisco
S1(config-line)#login 
S1(config)#line vty 0 4
S1(config)#service password-encryption
S1(config)#banner motd $Don't know, don't touch !!!!$
S1#copy running-config startup-config
S1#clock set 22:55:00 30 september 2020

###  Пример настройки на коммутаторе S2:
Switch#configure terminal 
Switch(config)#hostname S2
S2(config)#no ip domain-lookup
S2(config)#enable password class
S2(config)#line console 0
S2(config-line)#password cisco
S2(config-line)#login 
S2(config)#line vty 0 4
S2(config)#service password-encryption
S2(config)#banner motd $Don't know, don't touch !!!!$
S2#copy running-config startup-config
S2#clock set 22:56:00 30 september 2020

###  Решение пункта 2:
###  Пример настройки на коммутаторе S1:
S1(config)#vlan 3
S1(config-vlan)#name Managment
S1(config-vlan)#exit
S1(config)#interface vlan 3
S1(config-if)#no shutdown
S1(config-if)#ip address 192.168.3.11 255.255.255.0
S1(config)#ip default-gateway 192.168.3.1
S1(config)#interface e0/2
S1(config-if)#switchport mode access
S1(config-if)#switchport access vlan 3
S1(config)#int e0/0
S1(config-if)#sw trunk encapsulation dot1q
S1(config-if)#sw mo tru

###  Решение пункта 3:
###  Пример настройки на маршрутизаторе R1:
R1(config)#int e0/0
R1(config-if)#no sh
R1(config-if)#exit
R1(config)#int e0/0.3
R1(config-subif)#no sh
R1(config-subif)#encapsulation dot1Q 3
R1(config-subif)#ip address 192.168.3.1 255.255.255.0
R1(config-subif)#description Management
R1(config)#int e0/0.4
R1(config-subif)#no sh
R1(config-subif)#encapsulation dot1Q 4
R1(config-subif)#ip address 192.168.4.1 255.255.255.0
R1(config-subif)#description Operations


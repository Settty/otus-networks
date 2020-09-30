#  Настройка VLAN 

###  Задание согласно методичке:

  1. Построение сети и настройка основных параметров устройства.
  2. Создание сетей VLAN и назначение портов коммутатора
  3. Настройка TRUNK 802.1Q между коммутаторами
  4. Настройка маршрутизации между VLAN на маршрутизаторе
  5. Убедиться, что маршрутизация между VLAN работает

###  Решение:

###  Пример настройки на маршрутизаторе R1:

```
Router#configure terminal
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

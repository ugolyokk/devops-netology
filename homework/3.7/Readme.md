1.
Для linux: ```ip link show```
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:b1:28:5d brd ff:ff:ff:ff:ff:ff
```
Для Windows: ```ipconfig /all```
```
C:\Users\vorbi>ipconfig /all

Настройка протокола IP для Windows

   Имя компьютера  . . . . . . . . . : ugolyokk0
   Основной DNS-суффикс  . . . . . . :
   Тип узла. . . . . . . . . . . . . : Гибридный
   IP-маршрутизация включена . . . . : Нет
   WINS-прокси включен . . . . . . . : Нет
   Порядок просмотра суффиксов DNS . : Dlink

Адаптер Ethernet VirtualBox Host-Only Network:

   DNS-суффикс подключения . . . . . :
   Описание. . . . . . . . . . . . . : VirtualBox Host-Only Ethernet Adapter
   Физический адрес. . . . . . . . . : 0A-00-27-00-00-13
   DHCP включен. . . . . . . . . . . : Нет
   Автонастройка включена. . . . . . : Да
   Локальный IPv6-адрес канала . . . : fe80::dc6e:6933:8b6f:dc8e%19(Основной)
   IPv4-адрес. . . . . . . . . . . . : 192.168.56.1(Основной)
   Маска подсети . . . . . . . . . . : 255.255.255.0
   Основной шлюз. . . . . . . . . :
   IAID DHCPv6 . . . . . . . . . . . : 722075687
   DUID клиента DHCPv6 . . . . . . . : 00-01-00-01-26-A4-21-1E-1C-B7-2C-B1-A4-6D
   DNS-серверы. . . . . . . . . . . : fec0:0:0:ffff::1%1
                                       fec0:0:0:ffff::2%1
                                       fec0:0:0:ffff::3%1
   NetBios через TCP/IP. . . . . . . . : Включен
```

2. LLDP - протокол канального уровня, который позволяет сетевым устройствам анонсировать в сеть информацию о себе и о своих возможностях, а также собирать эту информацию о соседних устройствах
Команда ``` lldpctl ``` должна показать устройства в сети на которых включен LLDP. К сожалению у меня таких нет.

3. Vlan. Создаю Vlan 2 на интерфейс eth0 c адресом 192.168.0.2/24
```
vagrant@vagrant:~$ sudo modprobe 8021q
vagrant@vagrant:~$ sudo vconfig add eth0 2
vagrant@vagrant:~$ sudo ifconfig eth0.2 192.168.0.2/24 up
vagrant@vagrant:~$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
        inet6 fe80::a00:27ff:feb1:285d  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:b1:28:5d  txqueuelen 1000  (Ethernet)
        RX packets 1482  bytes 334373 (334.3 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1261  bytes 155785 (155.7 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0.2: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.2  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::a00:27ff:feb1:285d  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:b1:28:5d  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 12  bytes 936 (936.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 30  bytes 2648 (2.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 30  bytes 2648 (2.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```

4. Режимы агрегации интерфейсов в Linux:
```
mode=0 (balance-rr)
```
Последовательно кидает пакеты, с первого по последний интерфейс.
```
mode=1 (active-backup)
```
Один из интерфейсов активен. Если активный интерфейс выходит из строя (link down и т.д.), другой интерфейс заменяет активный. Не требует дополнительной настройки коммутатора
```
mode=2 (balance-xor)
```
Передачи распределяются между интерфейсами на основе формулы ((MAC-адрес источника) XOR (MAC-адрес получателя)) % число интерфейсов. Один и тот же интерфейс работает с определённым получателем. Режим даёт балансировку нагрузки и отказоустойчивость.
```
mode=3 (broadcast)
```
Все пакеты на все интерфейсы
```
mode=4 (802.3ad)
```
Link Agregation — IEEE 802.3ad, требует от коммутатора настройки.
```
mode=5 (balance-tlb)
```
Входящие пакеты принимаются только активным сетевым интерфейсом, исходящий распределяется в зависимости от текущей загрузки каждого интерфейса. Не требует настройки коммутатора.
```
mode=6 (balance-alb)
```
Тоже самое что 5, только входящий трафик тоже распределяется между интерфейсами. Не требует настройки коммутатора, но интерфейсы должны уметь изменять MAC.

Файл конфигурации находится ```/etc/netplan/00-installer-config.yaml```
Пример конфигурации:
```
#This is network config written bu 'subiquity'
network:
  ehternets:
    eth0:
      dhcp4: no
    eth1:
      dhcp4: no
  version: 2
  bonds:
      bond0: no
      interfaces: [eth0, eth1]
      parameters:
        mode: active-backup
        mii-monitor-interval: 1
```

5. В сети с маской /29 6 хостов. Из сети с маской /24 можно получить 32 подсети с маской /29. 
Примеры /29 подсетей внутри сети 10.10.10.0/24:
    10.10.10.0/29
    10.10.10.8/29
    10.10.10.16/29

6. Используя диапазон 100.64.0.0 — 100.127.255.255/10 можно взять подсеть 100.64.0.0/26 которая будет содержать 62 хоста.


7. Для Windows ```arp -a```
```
C:\Users\vorbi>arp -a

Интерфейс: 192.168.56.1 --- 0x13
  адрес в Интернете      Физический адрес      Тип
  192.168.56.255        ff-ff-ff-ff-ff-ff     статический
  224.0.0.2             01-00-5e-00-00-02     статический
  224.0.0.22            01-00-5e-00-00-16     статический
  224.0.0.251           01-00-5e-00-00-fb     статический
  224.0.0.252           01-00-5e-00-00-fc     статический
  224.0.1.187           01-00-5e-00-01-bb     статический
  228.8.8.8             01-00-5e-08-08-08     статический
  238.238.238.238       01-00-5e-6e-ee-ee     статический
  239.192.152.143       01-00-5e-40-98-8f     статический
  239.255.102.18        01-00-5e-7f-66-12     статический
  239.255.255.250       01-00-5e-7f-ff-fa     статический
```
Для Linux ```arp```
```
vagrant@vagrant:~$ arp
Address                  HWtype  HWaddress           Flags Mask            Iface
_gateway                 ether   52:54:00:12:35:02   C                     eth0
10.0.2.3                 ether   52:54:00:12:35:03   C                     eth0
```
Удалить одну запись можно с помощью ```arp -d```
```
C:\Windows\system32>arp -d 224.0.0.2

C:\Windows\system32>arp -a

Интерфейс: 192.168.56.1 --- 0x13
  адрес в Интернете      Физический адрес      Тип
  192.168.56.255        ff-ff-ff-ff-ff-ff     статический
  224.0.0.22            01-00-5e-00-00-16     статический
  224.0.0.251           01-00-5e-00-00-fb     статический
  224.0.0.252           01-00-5e-00-00-fc     статический
  224.0.1.187           01-00-5e-00-01-bb     статический
  228.8.8.8             01-00-5e-08-08-08     статический
  238.238.238.238       01-00-5e-6e-ee-ee     статический
  239.192.152.143       01-00-5e-40-98-8f     статический
  239.255.102.18        01-00-5e-7f-66-12     статический
  239.255.255.250       01-00-5e-7f-ff-fa     статический
```
Удалить все записи можно используя в Windows ```netsh interface ip delete arpcache```
В Linux ```ip neigh flush all```
```
C:\Windows\system32>netsh interface ip delete arpcache
ОК.


C:\Windows\system32>arp -a

Интерфейс: 192.168.56.1 --- 0x13
  адрес в Интернете      Физический адрес      Тип
  192.168.56.255        ff-ff-ff-ff-ff-ff     статический
  224.0.0.251           01-00-5e-00-00-fb     статический
  224.0.0.252           01-00-5e-00-00-fc     статический

  ```

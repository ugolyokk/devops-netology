### 1. Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP
```
telnet route-views.routeviews.org
Username: rviews
show ip route x.x.x.x/32
show bgp x.x.x.x/32
```

```
route-views>show ip route 5.18.144.189/32
                                      ^
% Invalid input detected at '^' marker.
```

```
route-views>show bgp 5.18.144.189/32
% Network not in table
```
### 2. Создайте dummy0 интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации
#### Создаю dummy
```
root@vagrant:~# ip link add dummy0 type dummy
root@vagrant:~# ip addr add 192.168.0.20/24 dev dummy0
root@vagrant:~# ip link set dummy0 up
root@vagrant:~# ifconfig -a
dummy0: flags=195<UP,BROADCAST,RUNNING,NOARP>  mtu 1500
        inet 10.0.2.16  netmask 255.255.255.0  broadcast 0.0.0.0
        inet6 fe80::dceb:f4ff:fe5f:f9cd  prefixlen 64  scopeid 0x20<link>
        ether de:eb:f4:5f:f9:cd  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 2  bytes 287 (287.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
        ether 08:00:27:b1:28:5d  txqueuelen 1000  (Ethernet)
        RX packets 432  bytes 35255 (35.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 280  bytes 31048 (31.0 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 96  bytes 7008 (7.0 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 96  bytes 7008 (7.0 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
#### Добавляю маршруты, смотрим таблицу маршрутизации
```
root@vagrant:~# ip route add 8.8.4.4/32 via 10.0.2.1
root@vagrant:~# ip route add 192.168.56.0/24 via 10.0.2.1
root@vagrant:~# ip route show
default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100
8.8.4.4 via 10.0.2.1 dev eth0
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15
10.0.2.0/24 dev dummy0 proto kernel scope link src 10.0.2.16
10.0.2.2 dev eth0 proto dhcp scope link src 10.0.2.15 metric 100
192.168.56.0/24 via 10.0.2.1 dev eth0

```
### 3. Проверьте открытые TCP порты в Ubuntu, какие протоколы и приложения используют эти порты? Приведите несколько примеров

#### TCP
```
root@vagrant:~# nmap localhost
Starting Nmap 7.80 ( https://nmap.org ) at 2022-05-07 17:20 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0000050s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in 0.14 seconds
```
открыт один tcp порт 22, который используется для ssh подключений
#### UDP
```
root@vagrant:~# nmap localhost -sU
Starting Nmap 7.80 ( https://nmap.org ) at 2022-05-07 17:27 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0000070s latency).
All 1000 scanned ports on localhost (127.0.0.1) are closed

Nmap done: 1 IP address (1 host up) scanned in 0.12 seconds
```
открытых udp портов нет

### 5. Используя diagrams.net, создайте L3 диаграмму вашей домашней сети или любой другой сети, с которой вы работали.
![image](https://user-images.githubusercontent.com/98211990/167265896-174a90c3-11b6-40c8-a682-37e1945294b0.png)


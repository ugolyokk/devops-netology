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

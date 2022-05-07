1. Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP
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

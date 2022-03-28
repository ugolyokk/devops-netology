
1. 
```
vagrant@vagrant:~$ telnet stackoverflow.com 80
Trying 151.101.65.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
Host: stackoverflow.com

HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
```
Искомая страница была оконачательно перемещена в https://stackoverflow.com/questions

2. Сделано
![Скриншот](https://github.com/ugolyokk/devops-netology/blob/954f48df6c7ec7e72755391ce57d8c99e1457576/homework/3.6/http.jpg)

Дольше всего передавалась страница 53.1 kB за 398ms
![image](https://user-images.githubusercontent.com/98211990/160437214-7216ca8c-bee5-4450-9f4f-c820c4b5796f.png)

3. 5.18.144.188

4. Z-Telecom <br/>
    AS41733
    
5. 
```
vagrant@vagrant:~$ sudo traceroute -IAn 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  10.0.2.2 [*]  0.309 ms  0.268 ms  0.258 ms
 2  192.168.0.1 [*]  1.718 ms  2.001 ms  2.974 ms
 3  10.8.84.1 [*]  11.685 ms  11.899 ms  12.100 ms
 4  5.19.0.178 [AS41733]  9.777 ms  9.932 ms  9.614 ms
 5  188.234.131.158 [AS9049]  7.046 ms  7.249 ms  7.435 ms
 6  72.14.214.138 [AS15169]  7.698 ms  3.843 ms  3.874 ms
 7  172.253.76.91 [AS15169]  4.369 ms  5.431 ms  5.596 ms
 8  74.125.244.181 [AS15169]  8.247 ms  8.186 ms  8.126 ms
 9  72.14.232.84 [AS15169]  8.066 ms  8.003 ms  7.944 ms
10  216.239.48.163 [AS15169]  9.373 ms  9.606 ms  9.715 ms
11  172.253.65.83 [AS15169]  10.059 ms  10.345 ms  8.476 ms
12  108.170.235.64 [AS15169]  8.682 ms  8.649 ms  8.681 ms
13  142.250.236.77 [AS15169]  9.545 ms  10.004 ms  9.973 ms
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  8.8.8.8 [AS15169]  8.958 ms  8.945 ms  9.987 ms
```
6. Наибольшее время задержки на AS15169  74.125.244.181

![image](https://user-images.githubusercontent.com/98211990/160445184-ea9cd86e-76c7-4997-8222-07539f2a2b69.png)


7.
```
 vagrant@vagrant:~$ dig dns.google

; <<>> DiG 9.16.1-Ubuntu <<>> dns.google
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 46556
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;dns.google.                    IN      A

;; ANSWER SECTION:
dns.google.             17      IN      A       8.8.4.4
dns.google.             17      IN      A       8.8.8.8

;; Query time: 2008 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Mon Mar 28 16:38:23 UTC 2022
;; MSG SIZE  rcvd: 71
```

8.
```
vagrant@vagrant:~$ dig -x 8.8.4.4

; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 4736
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.   29951   IN      PTR     dns.google.

;; Query time: 2004 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Mon Mar 28 16:49:24 UTC 2022
;; MSG SIZE  rcvd: 73
```



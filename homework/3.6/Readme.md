
1. Сделано
```bash 
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



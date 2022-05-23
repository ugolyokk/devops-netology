# Домашнее задание к занятию "4.3. Языки разметки JSON и YAML"


## Обязательная задача 1
Мы выгрузили JSON, который получили через API запрос к нашему сервису:
```
    { "info" : "Sample JSON output from our service\t",
        "elements" :[
            { "name" : "first",
            "type" : "server",
            "ip" : 7175 
            }
            { "name" : "second",
            "type" : "proxy",
            "ip : 71.78.22.43
            }
        ]
    }
```
### Исправленный JSON: 
ip в кавычки, запятая между блоками
```
 { "info" : "Sample JSON output from our service\t",
        "elements" :[
            { "name" : "first",
            "type" : "server",
            "ip" : 7175 
            },
            { "name" : "second",
            "type" : "proxy",
            "ip" : "71.78.22.43"
            }
        ]
    }
```
  Нужно найти и исправить все ошибки, которые допускает наш сервис

## Обязательная задача 2
В прошлый рабочий день мы создавали скрипт, позволяющий опрашивать веб-сервисы и получать их IP. К уже реализованному функционалу нам нужно добавить возможность записи JSON и YAML файлов, описывающих наши сервисы. Формат записи JSON по одному сервису: `{ "имя сервиса" : "его IP"}`. Формат записи YAML по одному сервису: `- имя сервиса: его IP`. Если в момент исполнения скрипта меняется IP у сервиса - он должен так же поменяться в yml и json файле.

### Ваш скрипт:
```python
#!/usr/bin/env python3
import socket
import time
import json
import yaml

hosts = [{'drive.google.com': 0}, {'mail.google.com': 0}, {'google.com': 0}]
while True:
    for host in hosts:
        for hostname in host:
            host_ip = socket.gethostbyname(hostname)
            if host[hostname] != host_ip:
                print('[ERROR]', hostname, 'IP mismatch:', host[hostname], '---->', host_ip)
            else:
                print(hostname, '-', host_ip)
        host[hostname] = host_ip
    with open('hosts_ips.json', 'w') as fj:
        fj.write(json.dumps(hosts))
    with open('hosts_ips.yaml', 'w') as fy:
        fy.write(yaml.dump(hosts))
    time.sleep(3)
```

### Вывод скрипта при запуске при тестировании:
```
ugolyokk@ugolyokk-ubuntu:~/netology/devops-netology/python$ /home/ugolyokk/netology/devops-netology/python/task4-3.py
[ERROR] drive.google.com IP mismatch: 0 ----> 142.250.150.194
[ERROR] mail.google.com IP mismatch: 0 ----> 173.194.221.18
[ERROR] google.com IP mismatch: 0 ----> 173.194.220.102
drive.google.com - 142.250.150.194
[ERROR] mail.google.com IP mismatch: 173.194.221.18 ----> 173.194.221.83
[ERROR] google.com IP mismatch: 173.194.220.102 ----> 173.194.220.138
drive.google.com - 142.250.150.194
mail.google.com - 173.194.221.83
google.com - 173.194.220.138

```

### json-файл(ы), который(е) записал ваш скрипт:
```json
[{"drive.google.com": "142.250.150.194"}, {"mail.google.com": "173.194.221.83"}, {"google.com": "173.194.220.138"}]
```

### yml-файл(ы), который(е) записал ваш скрипт:
```yaml
- drive.google.com: 142.250.150.194
- mail.google.com: 173.194.221.83
- google.com: 173.194.220.138
```



# Домашнее задание к занятию "4.2. Использование Python для решения типовых DevOps задач"

## Обязательная задача 1

Есть скрипт:
```python
#!/usr/bin/env python3
a = 1
b = '2'
c = a + b
```

### Вопросы:
| Вопрос  | Ответ |
| ------------- | ------------- |
| Какое значение будет присвоено переменной `c`?  | Никакое. Вернется ошибка т.к. переменные разного типа  |
| Как получить для переменной `c` значение 12?  | `c = str(a) + b`  |
| Как получить для переменной `c` значение 3?  | `c = a + int(b)`  |

## Обязательная задача 2
Мы устроились на работу в компанию, где раньше уже был DevOps Engineer. Он написал скрипт, позволяющий узнать, какие файлы модифицированы в репозитории, относительно локальных изменений. Этим скриптом недовольно начальство, потому что в его выводе есть не все изменённые файлы, а также непонятен полный путь к директории, где они находятся. Как можно доработать скрипт ниже, чтобы он исполнял требования вашего руководителя?

```python
#!/usr/bin/env python3

import os

bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(prepare_result)
        break
```

### Ваш скрипт:
- Удалена неиспользуемая переменная `is_change = False`
- Удалено `break` прерывание цикла при первом нахождении модифицированного файла
```python
#!/usr/bin/env python3

import os

bash_command = ["cd ~/netology/devops-netology/python", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(prepare_result)

```

### Вывод скрипта при запуске при тестировании:
```
ugolyokk@ugolyokk-ubuntu:~/netology/devops-netology/python$ /home/ugolyokk/netology/devops-netology/python/task2.py
task2.py
task3.py

```

## Обязательная задача 3
1. Доработать скрипт выше так, чтобы он мог проверять не только локальный репозиторий в текущей директории, а также умел воспринимать путь к репозиторию, который мы передаём как входной параметр. Мы точно знаем, что начальство коварное и будет проверять работу этого скрипта в директориях, которые не являются локальными репозиториями.

### Ваш скрипт:
добавил регулярное выражение, чтобы удалить лишнее в имени файла при вызове в другую директорию
```python
#!/usr/bin/env python3

import os
import re
import sys

repo = sys.argv[1]
bash_command = ['git status {}'.format(repo)]
result_os = os.popen(' && '.join(bash_command)).read()
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = re.sub(r'.*\/', '', result.replace('\tmodified:   ', '')) 
        print('{} {}'.format(repo, prepare_result))

```

### Вывод скрипта при запуске при тестировании:
- git status:
```
ugolyokk@ugolyokk-ubuntu:~/netology/devops-netology/python$ git status --porcelain 
 M python/task2.py
AM python/task3.1.py
 M python/task3.py
AM python/task4.py
AM test/1.log
AM test/2.txt
AM test/3.bat
AM test2/test3/1.sh
AM test2/test3/2.jar
```
- Вывод скрипта:
```
ugolyokk@ugolyokk-ubuntu:~/netology/devops-netology/python$ ./task3.py ~/netology/devops-netology/python/
/home/ugolyokk/netology/devops-netology/python/ task2.py
/home/ugolyokk/netology/devops-netology/python/ task3.1.py
/home/ugolyokk/netology/devops-netology/python/ task3.py
/home/ugolyokk/netology/devops-netology/python/ task4.py
ugolyokk@ugolyokk-ubuntu:~/netology/devops-netology/python$ ./task3.py ~/netology/devops-netology/test
/home/ugolyokk/netology/devops-netology/test 1.log
/home/ugolyokk/netology/devops-netology/test 2.txt
/home/ugolyokk/netology/devops-netology/test 3.bat
ugolyokk@ugolyokk-ubuntu:~/netology/devops-netology/python$ ./task3.py ~/netology/devops-netology/test2/test3/
/home/ugolyokk/netology/devops-netology/test2/test3/ 1.sh
/home/ugolyokk/netology/devops-netology/test2/test3/ 2.jar

```

## Обязательная задача 4
1. Наша команда разрабатывает несколько веб-сервисов, доступных по http. Мы точно знаем, что на их стенде нет никакой балансировки, кластеризации, за DNS прячется конкретный IP сервера, где установлен сервис. Проблема в том, что отдел, занимающийся нашей инфраструктурой очень часто меняет нам сервера, поэтому IP меняются примерно раз в неделю, при этом сервисы сохраняют за собой DNS имена. Это бы совсем никого не беспокоило, если бы несколько раз сервера не уезжали в такой сегмент сети нашей компании, который недоступен для разработчиков. Мы хотим написать скрипт, который опрашивает веб-сервисы, получает их IP, выводит информацию в стандартный вывод в виде: <URL сервиса> - <его IP>. Также, должна быть реализована возможность проверки текущего IP сервиса c его IP из предыдущей проверки. Если проверка будет провалена - оповестить об этом в стандартный вывод сообщением: [ERROR] <URL сервиса> IP mismatch: <старый IP> <Новый IP>. Будем считать, что наша разработка реализовала сервисы: `drive.google.com`, `mail.google.com`, `google.com`.

### Ваш скрипт:
```python
#!/usr/bin/env python3
import socket
import time

hosts = {'drive.google.com':0, 'mail.google.com':0, 'google.com':0}
while 1==1:
    for host in hosts:
        host_ip = socket.gethostbyname(host)
        if hosts[host] != host_ip:
            print('[ERROR]', host, 'IP mismatch:', hosts[host], '---->', host_ip)
        else:
            print(host, '-', host_ip)
        hosts[host] = host_ip
    time.sleep(5)
```

### Вывод скрипта при запуске при тестировании:
```
ugolyokk@ugolyokk-ubuntu:~/netology/devops-netology/python$ /home/ugolyokk/netology/devops-netology/python/task4.py
[ERROR] drive.google.com IP mismatch: 0 ----> 173.194.222.194
[ERROR] mail.google.com IP mismatch: 0 ----> 64.233.161.83
[ERROR] google.com IP mismatch: 0 ----> 64.233.162.113
drive.google.com - 173.194.222.194
[ERROR] mail.google.com IP mismatch: 64.233.161.83 ----> 64.233.161.18
[ERROR] google.com IP mismatch: 64.233.162.113 ----> 64.233.162.138
drive.google.com - 173.194.222.194
mail.google.com - 64.233.161.18
google.com - 64.233.162.138
```


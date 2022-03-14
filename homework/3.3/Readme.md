1. Системынй вызов chdir("/tmp")

2. /usr/share/misc/magic.mgc

3. Не получается имитировать ситуацию. При удалении текстового файла в который пишет nano он просто создается заново при следующей записи

4. Занимают только таблицу процессов

5. 
![Скриншот](https://github.com/ugolyokk/devops-netology/blob/216a1b7a66b3467f080caa4759a08190c9af25ca/homework/3.3/open.jpg)

6. Системный вызов uname()
 >"Part of the utsname information is also accessible via /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}."

7. "test -d /tmp/some_dir; echo Hi" Здесь команды запускаются последовательно </br>  
"test -d /tmp/some_dir && echo Hi" Здесь echo отработает только в случае успешного срабатвания test -d </br>

   "set -e" Прерывает выполнение комман при коде возварата отличном от нуля. </br>
Применять && и set -e не имеет смысла т.к. && прервет выполнение команд при ненулевом коде возварата

8. set -euxo pipefail </br>
-e Exits immediately if a command exits with a non-zero exit status  </br>
-u Treats unset variables as an error when substituting  </br>
-x Prints commands and their arguments as they are executed  </br>
-o Option (pipefail в нашем случае)  </br>
-pipefail A pipeline does not complete until all components of the pipeline have completed, and the exit status of the pipeline is the value of the last command to exit with non-zero exit status, or is zero if all commands return zero exit status  </br>

Такой набор опций позволяет подробно отслеживать выполнение скрипта и прерывать его при наличии ошибок

9. S - процессы ожидающие завершения события  </br>
   R - выполняющиеся проессы

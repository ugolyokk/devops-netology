1. chdir("/tmp")

2. /usr/share/misc/magic.mgc

3. Не получается имитировать ситуацию. При удалении текстового файла в который пишет nano он просто создается заново при следующей записи

4. Занимают только таблицу процессов

5. open.jpg

6. Part of the utsname information is also accessible via /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}. 

7. "test -d /tmp/some_dir; echo Hi" Здесь команды запускаются последовательно
"test -d /tmp/some_dir && echo Hi" Здесь echo отработает только в случае успешного срабатвания test -d
set -e Прерывает выполнение комман при коде возварата отличном от нуля.
Применять && и set -e не имеет смысла т.к. && прервет выполнение команд при ненулевом коде возварата

8. set -euxo pipefail
-e Exits immediately if a command exits with a non-zero exit status
-u Treats unset variables as an error when substituting
-x Prints commands and their arguments as they are executed
-o Option (pipefail в нашем случае)
-pipefail A pipeline does not complete until all components of the pipeline have completed, and the exit status of the pipeline is the value of the last command to exit with non-zero exit status, or is zero if all commands return zero exit status

Такой набор опций позволяет подробно отслеживать выполнение скрипта и прерывать его при наличии ошибок

9.
S - ожидающие завершения события
R - выполняющиеся

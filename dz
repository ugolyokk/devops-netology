1) Установил
2) Установил
3) Использую Termius
4) Запустил
5) Оперативная память: 1024МБ
   Процессоры: 2
   Видеопамять: 4МБ
   Жесткий диск: 64ГБ(реальный пока 2ГБ)
   Сетевой адаптер (NAT)

6) Добавить в конфигурационный файл vagrant строки. Например:
    Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-20.04"
	config.vm.provider "virtualbox" do |vb|
	vb.name = "my_vm"
	vb.memory = 2048
	vb.cpus = 4
	end
    end

   И перезапустить машину "vagrant reload"
  Будет создана вм с именем my_vm, 2048МБ оперативной памяти и 4 виртуальными процессорами

7) PS E:\vagrantconfig> vagrant ssh
   Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-91-generic x86_64)

8) переменная HISTFILESIZE
   строка 554

   ignoreboth применяет директивы ignorespace и ignoredups
   строки начинающиеся на пробел не сохранятся в истории(ignorespace)
   строки повторяющие предыдущие не сохранятся в истории(ignoredups)

9) 706 строка Brace Expansion
    {} позволяют сгенерировать аргументы для команды из заданного диапазона

   186 строка Compound Commands
    { list; } Команды внутри фигурных скобок выполняются в текущем окружении оболочки

10) touch file{1..100000}. 300000 нет, потому что будет превышено количество аргументов

11) [[ -d /tmp ]] выполняет сравнение и возвращает код 0 если истинно и 1 если ложно. 
    В данном случает выражение истинно т.к. /tmp существует и является диррекотрией
     vagrant@vagrant:~$ [[ -d /tmp ]]
     vagrant@vagrant:~$ echo $?
     0

12) mkdir /tmp/new_path_directory/
    cp /usr/bin/bash /tmp/new_path_directory
    PATH=/tmp/new_path_directory/:$PATH

13) at выполняет команду в назначеное время
    batch выполняет команду когда позволяет уровень загрузки системы. Когда средняя нагрузка падает ниже 1.5)
  
14) Завершил

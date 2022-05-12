### 1. Опишите своими словами основные преимущества применения на практике IaaC паттернов. Какой из принципов IaaC является основополагающим?
#### - Ускорение производства.
IaaC помогает конфигурировать инфраструктуру быстрее и эффективнее, ускоряет разработку и вывод продукта на рынок.
#### - Стабильность среды. 
Избавление от различий конфигураций в средах разработки, стандартизация окружающей инфраструктуры,
благодаря которой снижается вероятность ошибок.
#### - Безопасность и документирование. 
IaaC своего рода документация создании правильной инфраструктуры, а точное воспроизведение
конфигурации позволяет лего применять стандарты безопаности.

#### Оснвополающий принцип - получение раз за разом одинкового результата при одинаковых действиях(Идемпотентность)

### 2. Чем Ansible выгодно отличается от других систем управление конфигурациями? Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?
Ansible использует декларативный(описывается желаемый результат) и императивный(задается алгоритм действий) подходы.
В Ansible конфигурация на целевые хосты отправляется управляющим сервером(Push). Также для его работы не требуется установка специального агенат на целевой хост, управление осуществляется через ssh.<br>  
На мой взгляд push метод работы более надежный т.к. позволяет сомостоятельно инициировать применение изменений в конфигурации хоста и быть увереным в том, что это произошло. 

### 3. Установить на личный компьютер: VirtualBox, Vagrant, Ansible
#### VirtualBox
```
PS C:\Users\vorbi> Get-WmiObject -Class Win32_Product |? {$_.name -like "*Virtualbox*"}


IdentifyingNumber : {4A51F890-19E4-4E7C-A118-4B8ACEB5AEC5}
Name              : Oracle VM VirtualBox 6.1.32
Vendor            : Oracle Corporation
Version           : 6.1.32
Caption           : Oracle VM VirtualBox 6.1.32
```
#### Vagrant
```
PS C:\Users\vorbi> Get-WmiObject -Class Win32_Product |? {$_.name -like "*vagrant*" }


IdentifyingNumber : {AE22F759-1904-4AE6-8910-1AB92C1EAE88}
Name              : Vagrant
Vendor            : HashiCorp
Version           : 2.2.19
Caption           : Vagrant
```
#### Ansible
```
root@vagrant:~# ansible --version
ansible 2.9.6
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.8.10 (default, Nov 26 2021, 20:14:08) [GCC 9.3.0]
```


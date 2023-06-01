### <p align="center">Лабораторная 2 | Установка Linux (развертка, bootstraping)</p>
<br>

1. Создать виртуальную Linux x86_64-машину (не забываем включить в BIOS в CPU аппаратную поддержку виртуальных машин) с винчестером и CD, сетевая карта - bridge.
2. Загрузить дистрибутив System Rescue CD **64!**, подсоединяем к виртуальной машине, грузим CD; на некоторых машинах может не запускаться, попробуйте версию 4.X.X.
3. Устанавливаем Linux-ы: изучаем бутстраппинг (bootstrapping) операционной системы:
    + (“начальный уровень”) Debian/Ubuntu при помощи debootstrap;
    + (“средний уровень”) ставим Arch Linux (my favorite distribution) русский перевод (может быть неактуальным!) ;
    + (“продвинутый уровень”) Gentoo/Funtoo;
    + (“продвинутый уровень”) Установка глобального доступа в сеть IPv6 Tunnel brocker;
    + (“уровень 'guru'”) LHS;
    + (“уровень 'dao'”) Arch загрузкой по сети DHCP/TFTP/NFS, можно и другие дистрибутивы использовать.
4. Установить сервер sshd.
5. Сделать пользователя user с паролем 123456 (как у Хиллари Клинтон на корпоративной почте ;-)); пробросьте порт маршрутизатора 7022 на порт 22 вашей виртуальной машины; попробую зайти, посмотреть все ли готово.

---

<br>

## <p align="center">Подготовка</P>

Для создания виртуальной `Linux x86_64-машины с винчестером`, `CD-приводом` и `сетевой картой в режиме bridge`, можно использовать гипервизор `VirtualBox`. Вот пошаговая инструкция:

Шаг 1: Загрузка и установка VirtualBox

+ Скачать и установите [VirtualBox](https://www.virtualbox.org/) с официального сайта: 

Шаг 2: Создание виртуальной машины

+ Запустить VirtualBox.
+ Нажать на кнопку "New" (Создать) в верхней панели.
+ Ввести имя виртуальной машины (например, "Linux VM") и выберите тип операционной системы "Linux" и версию "Ubuntu (64-bit)".
+ Нажать кнопку "Next" (Далее).
+ Установить необходимый объем оперативной памяти (RAM) для виртуальной машины и нажмите "Next".
+ Ввести размер винчестера для виртуальной машины (например, 20 ГБ) и нажмите "Create" (Создать).

Шаг 3: Настройка виртуальной машины

+ В списке виртуальных машин выбрать только что созданную виртуальную машину и нажать на кнопку "Settings" (Настройки) в верхней панели.
+ В окне "Settings" выбрать вкладку "Storage" (Хранилище).
+ В контроле "Controller: IDE" выбрать "Empty" (Пусто) и в правой части окна выбрать значок CD/DVD.
+ В раскрывающемся списке "Attributes" (Атрибуты) выбрать "Choose Virtual Optical Disk File" (Выбрать виртуальный оптический диск).
+ Указать путь к ISO-образу операционной системы Linux, который вы хотите установить на виртуальную машину, и нажать "OK".

Шаг 4: Настройка сетевой карты в режиме bridge

+ В окне "Settings" выбрать вкладку "Network" (Сеть).
+ В контроле "Attached to" (Подключено к) выбрать "Bridged Adapter" (Мостовой адаптер).
+ В раскрывающемся списке "Name" (Имя) выбрать физическую сетевую карту, которую нужно использовать для соединения виртуальной машины с сетью.
+ Нажать "OK", чтобы сохранить настройки.

Шаг 5: Установка и запуск виртуальной машины

+ Выбрать созданную виртуальную машину в списке и нажмите на кнопку "Start" (Запуск) в верхней панели.
+ Следовать инструкциям установщика операционной системы Linux, которую вы выбрали ранее.
+ После завершения установки операционной системы, виртуальная машина будет готова к использованию.

Тепер есть виртуальная `Linux x86_64-машина с винчестером`, `CD-приводом` и `сетевой картой в режиме bridge`. Можно настроить и запустить нужное программное обеспечение на этой виртуальной машине.

**General**

+ Name:                 `Linux VM`
+ Operating System:     `Ubuntu (64-bit)`

**System**

+ Base Memory:          `8192 MB`
+ Processors:           `4`
+ Boot Order:           `Floopy, Optical, Hard Disk`
+ Acceleration:         `Nested Panging, KVM Paravirtualization`

<br>

---
<br>

## <p align="center">2. Загрузка дистрибутива System Rescue CD</P>

1. Скачать [System Rescue CD (64-битную версию)](https://www.system-rescue.org/Download/)

2. Подключить образ `System Rescue CD` к виртуальной машине и загрузиться с `CD`.

Для подключения образа `System Rescue CD` к виртуальной машине из командной строки в `VirtualBox`, можно использовать утилиту `VBoxManage`, которая поставляется вместе с `VirtualBox`:

+ Открыть командную строку или терминал на компьютере.

+ Перейти в каталог, где установлен `VirtualBox`.

+ Использовать следующую команду для подключения образа `System Rescue CD` к виртуальной машине:

```css

VBoxManage storageattach <имя__виртуальной_машины> --storagectl <имя_контроллера> --port <номер_порта> --device <номер_устройства> --type dvddrive --medium <путь_к_образу_System_Rescue_CD>

```
Заменить `<имя_виртуальной_машины>` на имя виртуальной машины, `<имя_контроллера>`, `<номер_порта>` и `<номер_устройства`> на соответствующие значения для виртуальной машины, а `<путь_к_образу_System_Rescue_CD>` на полный путь к образу `System Rescue CD` на компьютере.

Теперь можно запустить виртуальную машину и она загрузится с подключенного образа `System Rescue CD`.

Обратить внимание, что может потребоваться права администратора или суперпользователя для выполнения этой команды в зависимости от операционной системы.

<br>

---
<br>

## <p align="center">3. Установка различных дистрибутивов Linux</p>
<br>

### <p align="center">Форматирование и разбиение диска</p>
<br>


1. Запустить виртуальную машину Ubuntu и дождаться загрузки системы.

2. Открыть терминал. Для этого можно воспользоваться горячими клавишами `Ctrl+Alt+T`.

3. В терминале выполните команду `sudo parted -l`. Она позволит узнать список доступных дисков и их разделов.

<br>

```mathematica
Model: Virtual disk (vda)
Disk /dev/vda: 50.0GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:

Number  Start   End     Size    Type     File system  Flags
 1      1049kB  512MB   511MB   primary  ext4         boot
 2      513MB   50.0GB  49.5GB  primary  ext4
```

<br>

В данном месте `/dev/vda` является исследуемым диском.

4. Выбрать диск, который нужно разбить и отформатировать. Например, если нужно разбить `/dev/vda`, выполнить команду `sudo parted /dev/vda`.

5. Ввести команду `mklabel gpt`, чтобы создать новую таблицу разделов `GPT (GUID Partition Table)` на диске. Подтвердить действие, если будет запрошено.

<br>

```vbnet
(parted) mklabel gpt
Warning: The existing disk label on /dev/vda will be destroyed and all data on this disk will be lost. Do you want to continue?
Yes/No? Yes
```

<br>

6. Теперь можно создавать разделы на диске. Например, для создания раздела размером `20 ГБ` выполнить команду `mkpart primary ext4 0GB 20GB`. Заменить `ext4` на желаемую файловую систему раздела.

<br>

```scss
(parted) mkpart primary ext4 0GB 20GB
```

<br>

7. Повторить шаг 6 для создания всех необходимых разделов.

8. После создания разделов ввесть команду `quit`, чтобы выйти из `parted`.

9. Теперь нужно отформатировать созданные разделы. Например, для форматирования первого раздела выполните команду `sudo mkfs.ext4 /dev/vda1`.

<br>

```bash
sudo mkfs.ext4 /dev/vda1
```

10. Повторить шаг 9 для всех созданных разделов.

Теперь диск разбит и готов к установке операционной системы или использованию в качестве хранилища данных.

<br>

---

### <p align="center">Установка базовой системы</p>

<br>

1. После разбиения и форматирования диска нужно установить базовую систему. Для этого ввести следующую команду:

<br>

```php
sudo debootstrap <дистрибутив> <целевая_директория> <зеркало>
```

<br>

Заменить <дистрибутив> на выбранный дистрибутив Linux (например, "bionic" для Ubuntu 18.04 LTS). <целевая_директория> - это путь к директории, в которую будет установлена базовая система. <зеркало> - адрес зеркала, с которого будет загружаться пакеты (например,  [mirrow](http://archive.ubuntu.com/ubuntu).

<br>

```bash
sudo debootstrap bionic /mnt/ubuntu http://archive.ubuntu.com/ubuntu
```

Здесь базовая система `Ubuntu 18.04 LTS` будет установлена в директорию `/mnt/ubuntu` с использованием зеркала.


2. После завершения установки базовой системы перейти в установленную директорию с помощью команды `chroot`:

<br>

```bash
sudo chroot /mnt/ubuntu
```

<br>

Теперь работа ведется внутри установленной базовой системы.


3. Обновить список пакетов с помощью команды `apt update`:

<br>

```arduino
apt update
Get:1 http://archive.ubuntu.com/ubuntu bionic InRelease [242 kB]
Get:2 http://archive.ubuntu.com/ubuntu bionic-updates InRelease [88.7 kB]
Get:3 http://archive.ubuntu.com/ubuntu bionic-backports InRelease [74.6 kB]
...
```

<br>

4. Установить основные пакеты, необходимые для функционирования системы, с помощью команды `apt install`:

<br>

```bash
apt install <пакет1> <пакет2> ...
```

<br>

Заменить `<пакет1>`, `<пакет2>` и т.д. на названия пакетов, которые нужно установить.

Пример команды:

<br>

```
apt install openssh-server vim net-tools
```

<br>

В этом примере устанавливаются пакеты `openssh-server`, `vim` и `net-tools`.


5. Необходимые настройки системы

+ Настройка сети

Назначение статического IP-адреса:

<br>

```bash
sudo nano /etc/network/interfaces
```

<br>

Внутри файла добавить следующие строки, заменить `<interface>` на имя сетевого интерфейса (например, eth0) и `<ip_address>` на желаемый статический IP-адрес:

<br>

```csharp
auto <interface>
iface <interface> inet static
address <ip_address>
netmask <subnet_mask>
gateway <default_gateway>
dns-nameservers <dns_server_ip>
```

<br>

Сохранить изменения и перезапустить сетевой интерфейс командой:

<br>

```csharp
sudo ifdown <interface> && sudo ifup <interface>
```

<br>

Настройка DHCP:

<br>

```bash
sudo nano /etc/network/interfaces
```

<br>

Внутри файла найти строку `iface <interface> inet dhcp (где <interface>` - имя сетевого интерфейса) и убедиться, что она присутствует. Сохранить файл и перезагрузить сетевой интерфейс командой:

<br>

```csharp
sudo ifdown <interface> && sudo ifup <interface>
```

<br>

Настройка DNS-серверов:

<br>

```bash
sudo nano /etc/resolv.conf
```

<br>

Внутри файла добавить строки с IP-адресами DNS-серверов, разделяя их пробелами или переносом строки. Например:

<br>

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

<br>

Сохранить изменени

Проверка сетевого подключения:

<br>

```
ping google.com
```

<br>

---

### <p align="center">Настройка системы</p>

<br>


1. Настройка файловой системы и точек монтирования:

+ Просмотр доступных дисков и разделов:


<br>

```bash
sudo fdisk -l

Disk /dev/sda: 500GB
Device       Boot     Start       End    Sectors   Size  Type
/dev/sda1    *         2048    999423    997376   487M  Linux filesystem
/dev/sda2           1001470  976771071  975769602  465.2G  Linux filesystem
```

<br>

+ Форматирование раздела (например, ext4):


<br>

```bash
sudo mkfs.ext4 /dev/sda1
```

<br>

+ Создание точки монтирования:


<br>

```bash
sudo mkdir /mnt/mydisk
```

<br>

+ Добавление записи в файл /etc/fstab для автоматического монтирования:

<br>

```bash
sudo nano /etc/fstab
```

<br>

Внутри файла добавить строку в следующем формате:

<br>

```bash
/dev/sda1    /mnt/mydisk    ext4    defaults    0    2
```

<br>

3. Установка и настройка загрузчика:

+ Установка GRUB:

<br>

```bash
sudo apt install grub2
```

<br>

+ Настройка GRUB:

<br>

```bash
sudo nano /etc/default/grub
```

<br>

Внутри файла настроить параметры загрузчика, такие как `GRUB_TIMEOUT` (время ожидания загрузки) и `GRUB_DEFAULT` (по умолчанию выбранное ядро).

+ Установка systemd-boot:

<br>

```bash
sudo apt install systemd-boot
```

<br>

+ Настройка systemd-boot:

<br>

```bash
sudo nano /boot/efi/loader/loader.conf
```

<br>

Внутри файла настроить параметры загрузчика

<br>

```arduino
default    ubuntu
timeout    5
```

<br>

Создайте файл конфигурации для загрузки ОС

<br>

```bash
sudo nano /boot/efi/loader/entries/ubuntu.conf
```

<br>

Внутри файла лобавить конфигурацию для загрузки ОС

<br>

```bash
title   Ubuntu
linux   /vmlinuz-linux
initrd  /initramfs-linux.img
options root=/dev/sda2 rw
```

<br>




































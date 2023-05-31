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
2. Установить сервер sshd.
3. Сделать пользователя user с паролем 123456 (как у Хиллари Клинтон на корпоративной почте ;-)); пробросьте порт маршрутизатора 7022 на порт 22 вашей виртуальной машины; попробую зайти, посмотреть все ли готово.
4. Отчет - запишите ролик (VirtualBox, например, может это) как все было (тут надо продумать вариант записи консоли).

---

<br>

## <p align="center">1. Создане виртуальной машины</P>

Для создания виртуальной `Linux x86_64-машины с винчестером`, `CD-приводом` и `сетевой картой в режиме bridge`, можно использовать гипервизор VirtualBox. Вот пошаговая инструкция:

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
+ Operating System:     `Ubuntu (64-bit) 22.04.2`

**System**

+ Base Memory:          `8192 MB`
+ Processors:           `4`
+ Boot Order:           `Floopy, Optical, Hard Disk`
+ Acceleration:         `Nested Panging, KVM Paravirtualization`


































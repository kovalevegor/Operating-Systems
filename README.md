# <p align="center"> Operating-Systems | Лабораторная 3a | Реализация скрипта bash</p>

<br>

В установленной виртуальной машине реализовать задачу из методички, опубликованной [здесь](https://github.com/eugeneai/bash-essentials-ru-handbok/raw/master/bash-ru.pdf)

Задача выполнена для виртуальной машины VirtualBox на установленной [Ubuntu 22.04.2](https://releases.ubuntu.com/jammy/)

---

## <p align="center"> Постановка задачи 2</p>
<br>

Преобразовать все файлы формата `.jpg` в формат `JPEG2000` при помощи программы `convert` пакета `ImageMagic`

---

## <p align="center"> Алгоритм выполнения</p>
<br>

Прежде чем запустить скрипт, установим пакет ImageMagick:

```
sudo apt install imagemagick
```

Для решения данной задачи потребуется написать скрипт на языке `bash`, который будет использовать утилиту `convert` из пакета `ImageMagick` для преобразования файлов формата `.jpg` в формат `JPEG2000`.

<br>

```bash
#!/bin/bash

# Переходим в директорию с файлами .jpg
cd /путь/к/директории

# Итерируемся по всем файлам .jpg
for file in *.jpg; do
    # Создаем новое имя файла с расширением .jp2
    new_file="${file%.*}.jp2"
    
    # Используем утилиту convert для преобразования файла
    convert "$file" "$new_file"
    
    # Опционально: проверяем успешность выполнения команды convert
    if [ $? -eq 0 ]; then
        echo "Файл $file успешно преобразован в формат JPEG2000."
    else
        echo "Ошибка при преобразовании файла $file."
    fi
done
```
<br>

+ Для корректной работы скрипта нужно заменить `/путь/к/директории` на фактический путь к директории, в которой находятся файлы `.jpg`.

+ Сохранить скрипт в файл с расширением `.sh` (например, `convert_images.sh`), сделать его исполняемым с помощью команды `chmod +x convert_images.sh`, а затем запустите его, выполнив `./convert_images.sh` в терминале виртуальной машины.

+ Скрипт будет обрабатывать все файлы `.jpg` в указанной директории и создавать новые файлы с расширением `.jp2` в той же директории.


---

## <p align="center"> Постановка задачи 3</p>
<br>

Добавить в изображения формата `.jpg` подписи в виде текста `даты съемки`, дата берется из даты файла изображения, или текущая дата компьютера; изменение изображения делается также программай `convert` как в предыдущем задании

<br>

Для добавления подписей в виде текста с датой съемки на изображения формата `.jpg` можно использовать опцию `-annotate` утилиты `convert`. Для этого необходимо немного изменить предыдущий скрипт. Вот обновленная версия скрипта, которая добавляет подписи с датой:

<br>

```bash
#!/bin/bash

# Переходим в директорию с файлами .jpg
cd /путь/к/директории

# Итерируемся по всем файлам .jpg
for file in *.jpg; do
    # Создаем новое имя файла с расширением .jp2
    new_file="${file%.*}.jp2"
    
    # Получаем дату съемки из EXIF метаданных файла (если доступно)
    capture_date=$(identify -format "%[EXIF:DateTimeOriginal]" "$file")
    
    # Если дата съемки не доступна, используем текущую дату компьютера
    if [ -z "$capture_date" ]; then
        capture_date=$(date +"%Y-%m-%d")
    fi
    
    # Добавляем подпись с датой на изображение
    convert "$file" -annotate +10+10 "Date: $capture_date" "$new_file"
    
    # Опционально: проверяем успешность выполнения команды convert
    if [ $? -eq 0 ]; then
        echo "Файл $file успешно преобразован в формат JPEG2000 с подписью."
    else
        echo "Ошибка при преобразовании файла $file с подписью."
    fi
done
```

+ В данном скрипте мы используем команду `identify` для получения даты съемки из метаданных `EXIF` файла `.jpg`. Если дата съемки недоступна, мы используем текущую дату компьютера с помощью команды `date +"%Y-%m-%d"`. Затем мы используем опцию `-annotate` для добавления подписи с датой на изображение. Подпись помещается в верхний левый угол изображения с отступом 10 пикселей по горизонтали и вертикали.

+ Нужно обратить внимание, что для получения метаданных `EXIF` изображений нужно убедиться, что пакет `exiftool` установлен в системе. Если его нет, установить его командой
```
sudo apt install exiftool.
```
+ Нужно убедиться, что вы правильно указали путь к директории с файлами `.jpg`, а также что у имеются есть права доступа на чтение и запись в эту директорию. Затем сохранить скрипт в файл, сделать его исполняемым и запустите, как описано в предыдущем ответе.
















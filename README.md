# <p aligh="center" Operating-Systems | Лабораторная 3a | Реализация скрипта bash</p>

В установленной виртуальной машине реализовать задачу из методички, опубликованной [здесь](https://github.com/eugeneai/bash-essentials-ru-handbok/raw/master/bash-ru.pdf)

Задача выполнена для виртуальной машины VirtualBox на установленной [Ubuntu 22.04.2](https://releases.ubuntu.com/jammy/)

---

## <p aligh="center" Постановка задачи</p>
<br>
Преобразовать все файлы формата `.jpg` в формат `JPEG2000` при помощи программы `convert` пакета `ImageMagic`

---

## <p aligh="center" Алгоритм выполнения</p>
<br>
Прежде чем запустить скрипт, установим пакет ImageMagick:

```
sudo apt install imagemagick
```

Для решения данной задачи потребуется написать скрипт на языке `bash`, который будет использовать утилиту `convert` из пакета `ImageMagick` для преобразования файлов формата `.jpg` в формат `JPEG2000`.

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


Для корректной работы скрипта нужно заменить `/путь/к/директории` на фактический путь к директории, в которой находятся файлы `.jpg`.

Сохранить скрипт в файл с расширением `.sh` (например, `convert_images.sh`), сделать его исполняемым с помощью команды `chmod +x convert_images.sh`, а затем запустите его, выполнив `./convert_images.sh` в терминале виртуальной машины.

+ Скрипт будет обрабатывать все файлы `.jpg` в указанной директории и создавать новые файлы с расширением `.jp2` в той же директории.























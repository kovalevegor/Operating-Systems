# Operating-Systems | Лабораторная 1 | Исследования компилятора gcc. Язык ассемблера. Makefile, git.

#### Нужно написать программу на `С`, `С++`, `PASCAL/FPC` и др. компилируемом языке, странслировать его в `Assembler` с разными опциями оптимизации
`gcc -S -o <>.s <>.c -O[0123s]`
#### Разобраться с одним из вариантов [оптимизации] ассемблерной программой (добавить комментарии в сгенерированный ассемберный код) - найти циклы, переменные и т.п. Программу усовершенствовать: добавить параллельный процесс средствами `Linux/Windows`. Синхронизация доступа к общему ресурсу (файл, канал, pipe, очередь, mmap, smmem). Язык С или другой, но на С проще, есть куча примеров.

```cpp
#include <iostream>

int sumArray(int* array, int size) {
    int sum = 0;
    for (int i = 0; i < size; ++i) {
        sum += array[i];
    }
    return sum;
}

int main() {
    int array[] = {1, 2, 3, 4, 5};
    int size = sizeof(array) / sizeof(array[0]);
    int result = sumArray(array, size);
    std::cout << "Sum: " << result << std::endl;
    return 0;
}
```
После сохранения кода в файл с расширением `.cpp` (например, `example.cpp`), можно использовать `gcc` для трансляции его в ассемблерный код с разными опциями оптимизации.

Ниже приведены команды, которые можно использовать для генерации ассемблерного кода с разными уровнями оптимизации:

+ Оптимизация уровня 0:
```bash
gcc -S -o example_O0.s example.cpp -O0
```

+ Оптимизация уровня 1:
```bash
gcc -S -o example_O1.s example.cpp -O1
```

+ Оптимизация уровня 2:
```bash
gcc -S -o example_O2.s example.cpp -O2
```

+ Оптимизация уровня 3:
```bash
gcc -S -o example_O3.s example.cpp -O3
```

+ Оптимизация размера (-Os):
```bash
gcc -S -o example_Os.s example.cpp -Os
```

После выполнения каждой команды будет создан соответствующий ассемблерный файл (например, `example_O0.s`, `example_O1.s`, и т.д.), который содержит соответствующий код на языке ассемблера.























# Operating-Systems | Лабораторная 1 | Исследования компилятора gcc. Язык ассемблера. Makefile, git.

#### Нужно написать программу на `С`, `С++`, `PASCAL/FPC` и др. компилируемом языке, странслировать его в `Assembler` с разными опциями оптимизации
`gcc -S -o <>.s <>.c -O[0123s]`
#### Разобраться с одним из вариантов [оптимизации] ассемблерной программой (добавить комментарии в сгенерированный ассемберный код) - найти циклы, переменные и т.п. Программу усовершенствовать: добавить параллельный процесс средствами `Linux/Windows`. Синхронизация доступа к общему ресурсу (файл, канал, pipe, очередь, mmap, smmem). Язык С или другой, но на С проще, есть куча примеров. После сохранения кода в файл с расширением `.cpp` (например, `example.cpp`), можно использовать `gcc` для трансляции его в ассемблерный код с разными опциями оптимизации.

---

`Уровни оптимизации` в контексте ассемблерного кода обозначают различные настройки компилятора, которые влияют на процесс оптимизации генерируемого машинного кода. Каждый уровень оптимизации имеет свои особенности и цели, и выбор определенного уровня зависит от компромисса между скоростью выполнения и размером кода.

В общем случае, более высокий уровень оптимизации приводит к более эффективному коду с точки зрения времени выполнения и использования ресурсов. Однако более высокие уровни оптимизации также могут требовать большего времени компиляции и потенциально увеличивать размер генерируемого кода.

Вот некоторые типичные уровни оптимизации, которые могут применяться в ассемблерном коде:

+ `Отсутствие оптимизации (None)`: Компилятор не применяет никаких оптимизаций и генерирует код без изменений. Этот уровень может быть полезен для отладки или изучения сгенерированного кода.
    
    + Оптимизация уровня 0:
```bash
gcc -S -o example_O0.s example.cpp -O0
```

+ `Минимальная оптимизация (Minimal)`: Применяются базовые оптимизации, направленные на сокращение размера кода и простые локальные оптимизации. Однако компилятор ограничен в своих возможностях и не выполняет сложные глобальные оптимизации.

    + Оптимизация уровня 1:
```bash
gcc -S -o example_O1.s example.cpp -O1
```

+ `Оптимизация по умолчанию (Default)`: Это типичный уровень оптимизации, который применяется компилятором по умолчанию. Он включает широкий набор оптимизаций, включая векторизацию, удаление мертвого кода, распределение регистров и другие трансформации кода. Этот уровень обычно обеспечивает хороший баланс между производительностью и размером кода.

    + Оптимизация уровня 2:
```bash
gcc -S -o example_O2.s example.cpp -O2
```

+ `Максимальная оптимизация (Maximal)`: Этот уровень оптимизации включает все доступные оптимизации, которые может предложить компилятор. Он может занимать больше времени для компиляции и генерировать более сложный код, но в результате может обеспечить максимальную производительность.

    + Оптимизация уровня 3:
```bash
gcc -S -o example_O3.s example.cpp -O3
```
Выбор уровня оптимизации зависит от конкретных требований проекта. Если важна скорость выполнения, то обычно выбирают более высокий уровень оптимизации. Если же размер кода или время компиляции имеют большое значение, то могут выбрать более низкий уровень оптимизации.

+ Оптимизация размера (-Os):
```bash
gcc -S -o example_Os.s example.cpp -O4s
```

После выполнения каждой команды будет создан соответствующий ассемблерный файл (например, `example_O0.s`, `example_O1.s`, и т.д.), который содержит соответствующий код на языке ассемблера.

**fractional.cpp**

```cpp
#include <iostream>

int factorial(int n) {
    if (n == 0 || n == 1) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}

int main() {
    int number;
    std::cout << "Enter a number: ";
    std::cin >> number;

    int result = factorial(number);
    std::cout << "The factorial of " << number << " is: " << result << std::endl;

    return 0;
}

```
Выполним для нее следующую команду для трансляции: `gcc -S -o example_O1.s fractional.cpp -O1` и получим файл `example_01.s` со следующим содержимым:

```assembly
	.file	"fractional.cpp"
	.text
```
`fractional.cpp` - исходный файл программы.
```assembly
	.def	___tcf_0;	.scl	3;	.type	32;	.endef
___tcf_0:
LFB1923:
	.cfi_startproc
	subl	$12, %esp
	.cfi_def_cfa_offset 16
	movl	$__ZStL8__ioinit, %ecx
	call	__ZNSt8ios_base4InitD1Ev
	addl	$12, %esp
	.cfi_def_cfa_offset 4
	ret
	.cfi_endproc
LFE1923:
```
+ Функция `___tcf_0` - деструктор инициализации стандартного потока ввода/вывода.
+ `LFB1923` и `LFE1923` - метки начала и конца процедуры.
+ `subl $12, %esp` - выделение места на стеке для локальных переменных.
+ `movl $__ZStL8__ioinit, %ecx` - загрузка адреса инициализации потока ввода/вывода в регистр ecx.
+ `call __ZNSt8ios_base4InitD1Ev` - вызов деструктора инициализации потока ввода/вывода.
+ `addl $12, %esp` - освобождение выделенного места на стеке.
+ `ret` - возврат из процедуры.
```assembly
	.globl	__Z9factoriali
	.def	__Z9factoriali;	.scl	2;	.type	32;	.endef
__Z9factoriali:
LFB1489:
	.cfi_startproc
	pushl	%ebx
	.cfi_def_cfa_offset 8
	.cfi_offset 3, -8
	subl	$24, %esp
	.cfi_def_cfa_offset 32
	movl	32(%esp), %ebx
	movl	$1, %eax
	cmpl	$1, %ebx
	jbe	L3
	leal	-1(%ebx), %eax
	movl	%eax, (%esp)
	call	__Z9factoriali
	imull	%ebx, %eax
L3:
	addl	$24, %esp
	.cfi_def_cfa_offset 8
	popl	%ebx
	.cfi_restore 3
	.cfi_def_cfa_offset 4
	ret
	.cfi_endproc
LFE1489:
```
+ Функция `__Z9factoriali` - рекурсивная функция вычисления факториала числа.
+ `LFB1489` и `LFE1489` - метки начала и конца процедуры.
+ `pushl %ebx` - сохранение значения регистра ebx на стеке.
+ `subl $24, %esp` - выделение места на стеке для локальных переменных.
+ `movl 32(%esp), %ebx` - загрузка значения параметра функции в регистр `ebx`.
+ `movl $1, %eax` - загрузка значения 1 в регистр eax.
+ `cmpl $1, %ebx` - сравнение значения в `ebx` с 1.
+ `jbe L3` - переход к метке `L3`, если значение в `ebx` меньше или равно 1.
+ `leal -1(%ebx), %eax` - вычисление значения `(ebx - 1)` и сохранение результата в `eax`.
+ `movl %eax, (%esp)` - сохранение значения `eax` на стеке.
+ `call __Z9factoriali` - рекурсивный вызов функции `__Z9factoriali`.
+ `imull %ebx, %eax` - умножение значения `eax` на значение `ebx` и сохранение результата в eax.
+ `L3`: - метка `L3` для перехода.
+ `addl $24, %esp` - освобождение выделенного места на стеке.
+ `popl %ebx` - восстановление значения регистра `ebx`.
+ `ret` - возврат из процедуры.
```assembly
	.def	___main;	.scl	2;	.type	32;	.endef
	.section .rdata,"dr"
LC0:
	.ascii "Enter a number: \0"
LC1:
	.ascii "The factorial of \0"
LC2:
	.ascii " is: \0"
	.text
```
+ Функция `___main` - точка входа в программу.
+` ___main` и `LC0`, `LC1`, `LC2` - метки и строки, используемые в программе.
```assembly
	.globl	_main
	.def	_main;	.scl	2;	.type	32;	.endef
_main:
LFB1490:
	.cfi_startproc
	leal	4(%esp), %ecx
	.cfi_def_cfa 1, 0
	andl	$-16, %esp
	pushl	-4(%ecx)
	pushl	%ebp
	.cfi_escape 0x10,0x5,0x2,0x75,0
	movl	%esp, %ebp
	pushl	%esi
	pushl	%ebx
	pushl	%ecx
	.cfi_escape 0xf,0x3,0x75,0x74,0x6
	.cfi_escape 0x10,0x6,0x2,0x75,0x7c
	.cfi_escape 0x10,0x3,0x2,0x75,0x78
	subl	$44, %esp
	call	___main
	movl	$LC0, 4(%esp)
	movl	$__ZSt4cout, (%esp)
	call	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
	leal	-28(%ebp), %eax
	movl	%eax, (%esp)
	movl	$__ZSt3cin, %ecx
	call	__ZNSirsERi
	subl	$4, %esp
	movl	-28(%ebp), %ebx
	movl	%ebx, (%esp)
	call	__Z9factoriali
	movl	%eax, %esi
	movl	$17, 8(%esp)
	movl	$LC1, 4(%esp)
	movl	$__ZSt4cout, (%esp)
	call	__ZSt16__ostream_insertIcSt11char_traitsIcEERSt13basic_ostreamIT_T0_ES6_PKS3_i
	movl	%ebx, (%esp)
	movl	$__ZSt4cout, %ecx
	call	__ZNSolsEi
	subl	$4, %esp
	movl	%eax, %ebx
	movl	$5, 8(%esp)
	movl	$LC2, 4(%esp)
	movl	%eax, (%esp)
	call	__ZSt16__ostream_insertIcSt11char_traitsIcEERSt13basic_ostreamIT_T0_ES6_PKS3_i
	movl	%esi, (%esp)
	movl	%ebx, %ecx
	call	__ZNSolsEi
	subl	$4, %esp
	movl	%eax, (%esp)
	call	__ZSt4endlIcSt11char_traitsIcEERSt13basic_ostreamIT_T0_ES6_
	movl	$0, %eax
	leal	-12(%ebp), %esp
	popl	%ecx
	.cfi_restore 1
	.cfi_def_cfa 1, 0
	popl	%ebx
	.cfi_restore 3
	popl	%esi
	.cfi_restore 6
	popl	%ebp
	.cfi_restore 5
	leal	-4(%ecx), %esp
	.cfi_def_cfa 4, 4
	ret
	.cfi_endproc
LFE1490:

```













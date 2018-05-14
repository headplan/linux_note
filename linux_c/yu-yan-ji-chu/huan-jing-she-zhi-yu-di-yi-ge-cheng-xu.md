# 环境设置与第一个程序

#### 本地环境设置

设置C语言环境 , 需要确保电脑上有以下两款可用的软件 , 文本编辑器和C编译器 .

**文本编辑器**

文本编辑器包括 Windows Notepad、OS Edit command、Brief、Epsilon、EMACS 和 vim/vi等等 .

**C 编译器**

写在源文件中的源代码是人类可读的源 . 它需要"编译"转为机器语言 , 这样 CPU 可以按给定指令执行程序 . C语言编译器用于把源代码编译成最终的可执行程序 . 最常用的免费可用的编译器是GNU的C/C++编译器 , 如果使用的是HP或Solaris , 则可以使用各自操作系统上的编译器 . 这里同时提到C/C++ , 主要是因为GNU的gcc编译器适合于C和C++编程语言 .

**UNIX/Linux上的安装**

```
$ gcc -v
Using built-in specs.
Target: i386-redhat-linux
Configured with: ../configure --prefix=/usr .......
Thread model: posix
gcc version 4.1.2 20080704 (Red Hat 4.1.2-46)
```

安装 : [http://gcc.gnu.org/install/](http://gcc.gnu.org/install/)

```
# 腾讯云测试环境
yum install gcc
```

#### 第一个程序

* C语言的代码是由函数\(Function\)组成的
* 函数就是一个代码块\(block\)

打印Hello, World.

```c
#include <stdio.h>

int main()
{
    printf("Hello, World.\n");
    return 0;
}
```

* 程序的第一行 `#include <stdio.h>` 是预处理器指令，告诉 C 编译器在实际编译之前要包含 stdio.h 文件。
* stdio.h是一个C语言的标准输入输出库 , .h表示头文件 . 
* 下一行 `int main()` 是主函数，程序从这里开始执行 , int是函数的返回类型 , int整形 . 
* 下一行 `/*...*/` 将会被编译器忽略，这里放置程序的注释内容。它们被称为程序的注释。
* 下一行 `printf(...)` 是 C 中另一个可用的函数，会在屏幕上显示消息 "Hello, World!" , 就是stdio库的函数 . 这里的字符串必须是双引号 , 因为是强类型语言 . 
* 下一行 `return 0;` 终止 main\(\) 函数，并返回值 0。

C 程序主要包括 :

* 预处理器指令
* 函数
* 变量
* 语句 & 表达式
* 注释

**编译 & 执行**

* GCC - GNU C compiler是最广泛使用的编译器之一 . 
* Unix系操作系统（Unix，Linux，Mac OSX）的主要编译器
* .c源程序--&gt;经过编译器编译--&gt;可执行程序
* gcc hello.c -o hello , gcc是命令 , hello.c表示源文件的名字 , -o表示编译成一个输出的程序 , 结尾表示可执行程序的名字

```
$ gcc -o hello hello.c
$ ./hello
Hello, World!
```

#### 产生错误

例如 , `#include <stdio.c>`编译时报错error :

```
hello.c:1:10: fatal error: 'stdio.c' file not found
#include <stdio.c>
         ^
1 error generated.
```

例如 , `printf(1)`编译警告warning :

```
hello.c:5:12: warning: incompatible integer to pointer conversion passing 'int' to parameter of type 'const char *' [-Wint-conversion]
    printf(1);
           ^
```

例如 , `printf(0)`编辑时看不到错误或警告 , 但执行时会提示故障 . 显示编译错误细节 , 可以使用gcc的-Wall参数 :

```
$ gcc -W -Wall hello.c
hello.c: 在函数‘main’中:
hello.c:5: 警告：实参为 NULL，需要非 NULL 值(实参 1)
```

> -W选项类似-Wall , 会显示警告 , 但是只显示编译器认为会出现错误的警告 . 在编译一些项目的时候可以-W和-Wall选项一起使用 .




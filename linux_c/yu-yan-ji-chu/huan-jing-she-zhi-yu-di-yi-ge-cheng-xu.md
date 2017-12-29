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




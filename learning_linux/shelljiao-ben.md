# Shell脚本

#### Shell简介

Shell本身是一个用C语言编写的程序 , 在Unix/Linux中 , 用户的大部分工作都是通过Shell完成的 .

Shell既是一种命令语言 , 又是一种程序设计语言 .

> 作为命令语言 , 它交互式地解释和执行用户输入的命令;作为程序设计语言 , 它定义了各种变量和参数 , 并提供了许多在高级语言中才具有的控制结构 , 包括循环和分支 . 它虽然不是Unix/Linux系统内核的一部分 , 但它调用了系统核心的大部分功能来执行程序、建立文件并以并行的方式协调各个程序的运行 .

**Shell有两种执行命令的方式 : **

* 交互式 - 解释执行用户的命令 , 用户输入一条命令 , Shell就解释执行一条
* 批处理 - 用户事先写一个Shell脚本\(Script\) , 其中有很多条命令 , 让Shell一次把这些命令执行完

Shell脚本和编程语言很相似 , 也有变量和流程控制语句 , 但Shell脚本是解释执行的 , 不需要编译 , Shell程序从脚本中一行一行读取并执行这些命令 , 相当于一个用户把脚本中的命令一行一行敲到Shell提示符下执行 .

#### 几种常见的Shell

Shell是脚本语言 , 所以得有解释器执行脚本 .

> Unix/Linux上常见的Shell脚本解释器有bash、sh、csh、ksh等

* bash - Linux标准默认的shell\(内部命令一共有40个\) , bash完全兼容sh . 
* sh - sh是Unix标准默认的shell
* ash - Linux中占用系统资源最少的一个小shell , 它只包含24个内部命令
* csh - 该shell其实是指向/bin/tcsh这样的一个shell , 也就是说 , csh其实就是tcsh
* ksh - 该shell最大的优点是几乎和商业发行版的ksh完全兼容

#### Shell脚本语言与编译型语言的差异

* 编译型语言 - 这类语言需要预先将我们写好的源代码\(source code\)转换成目标代码\(object code\) , 这个过程被称作“编译” .
* 解释型语言\(脚本\) - 执行这类程序时，解释器\(interpreter\)需要读取我们编写的源代码\(source code\) , 并将其转换成目标代码\(object code\) , 再由计算机运行 , 每次执行程序都多了编译的过程 . 
  * 脚本编程语言的例子有awk、Perl、Python、Ruby与Shell

#### 第一个Shell脚本

**新建文件**

文件扩展名并不影响脚本执行 , 见名知意即可 , 如果用php写shell脚本 , 扩展名就用php好了

```
#!/bin/bash
echo "Hi!"
```

`#!`是约定标记 , 它告诉系统这个脚本需要什么解释器来执行 , 就是用哪种shell

**运行Shell脚本有两种方法**

**作为可执行程序**

```
# 保存刚才的文件
chmod +x ./test.php  #使脚本具有执行权限
./test.sh  #执行脚本
```

> 注意 , 一定要写成./test.php , 而不是test.php

运行其它二进制的程序也一样 , 直接写test.php , linux系统会去PATH里寻找有没有叫test.php的 . 一般当前目录是不会在PATH中的 , 所以加上./表示当前目录 .

**作为解释器参数**

这种运行方式是 , 直接运行解释器 , 其参数就是shell脚本的文件名

```
/bin/sh test.sh
/bin/php test.php
```

这种方式运行的脚本 , 不需要在第一行指定解释器信息 , 写了也没用 .

例子

```
#!/bin/bash
echo "What is your name?"
read PERSON
echo "Hello, $PERSON"
```

参考资料:

[http://c.biancheng.net/cpp/shell/](http://c.biancheng.net/cpp/shell/)


# Linux系统基础使用入门

#### 登录

root/\*\*\*\*\*\*

图形界面 - startx &

#### 终端

用户与主机交互,必然用到的设备,即终端设备.

物理终端 - 直接接入本机的显示器和键盘设备,也叫做控制台. /dev/console

虚拟终端 - 附加在物理终端之上的以软件方式虚拟实现的终端,CentOS 6默认启动6个虚拟终端\(Ctrl+Alt+F\#: \[1,6\]\)

=&gt;图形终端 - 附加在物理终端之上的以软件方式虚拟实现的终端,但额外会提供桌面环境.

模拟终端 - 图形界面下打开的命令行接口,基于ssh协议或telnet协议等远程打开的界面.

**查看当前的终端设备** , 使用命令tty即可.\(设备文件路径\)

物理终端 - /dev/console

虚拟终端 - /dev/tty1

模拟终端 - /dev/pts/0

**交互式接口** - 启动终端后,在终端设备附加一个交互式应用程序,这样才能进行交互.

GUI：图形界面

```
X protocol, window manager, desktop
Desktop:
    GNOME (C, gtk)
    KDE   (C++, qt)
    XFCE  (轻量级桌面)
```

CLI：命令行

```
shell程序：
    sh (bourn研发的)
    csh 
    tcsh
    ksh (korn)
    bash (bourn again shell), sh的二次开发版,遵循GPL协议,是开源的
    zsh 

显示当前使用的shell：
    # echo ${SHELL}

显示当前系统使用的所有shell：
    # cat /etc/shells

命令提示符(prompt)
    [root@localhost ~]
    上面的内容是PS1环境变量,它的显示格式可以echo ${PS1}查看
        命令提示符仅是#或$符：
            管理员：#
            普通用户：$
```

#### 命令

**输入命令**，回车：

提请shell程序找到键入命令所对应的可执行程序或代码，并由其分析后提交给内核分配资源将其运行起来；

表现为一个或多个进程；\(可以理解为在Windows中双击运行程序\)

在shell中可执行的命令有两类：

```
    内建命令：由shell自带的，而且通过某命令形式提供；

    外部命令：在当前系统的某文件系统路径下有对应的可执行程序文件；
```

两个查找命令 : which，whereis ,可以查找命令对应的执行程序或代码

```
which命令是查找命令是否存在，以及命令的存放位置在哪儿
whereis命令只能用于搜索程序名,而且只搜索二进制文件(参数-b),man说明文件(参数-m)和源代码文件(参数-s).如果省略参数,则返回所有信息.
```

注意:which查找不到的命令,说明这个命令是shell的内建命令,例如cd

区别内部或外部命令：

```
# type COMMAND
```

**运行命令**

COMMAND \[OPTIONS...\] \[ARGUMENTS...\]

选项：用于启用或关闭命令的某个或某些功能；

* 短选项：-c, 例如：-l, -h . 多个短选项可合并使用，例如-l -h, 可写作-lh；
* 长选项：--word，例如：--long, --human-readable\(长选项一般不能合并\)

参数：命令的作用对象\(或命令的生效对象\) , 向命令提供数据；

注意：

1. 多选项，以及多参数和命令之间都应该使用空白字符分隔
2. 取消命令执行：Ctrl+c

**文件系统简介**

```
C:\Program files\office11\word\word.exe
/etc/sysconfig/network-scripts/ifcfg-eth0
```

文件有两类数据\(或者说一个文件\)：

* 元数据：metadata\(属性信息,一些索引信息,可以理解为元数据\)
* 数据：data

Linux下的文件系统特性

1. 文件名严格区分字符大小写；file1, File1, FILE1是不同的文件；
2. 文件名可使用除/以外的任意字符，不建议使用特殊字符；/ 是根目录或路径分隔符；
3. 文件名长度最长不能超过255个字符；
4. 所以.开头的文件，均为隐藏文件；

**路径**

* 绝对路径：从根目录起始的路径；
* 相对路径：对当前位置起始的路径；
  * 当前位置的表示方式：
    1. ./ - ./sysconfig/network-scripts
    2. 省略上述符号 - sysconfig/network-scripts
    3. .. - 表示当前目录的上一级目录

> 当前目录：current directory, 也称作working directory；
>
> 例如命令pwd: printing working directory

**LSB: Linux Standard Base**

表示Linux发行版依照LSB的规定标准的,比如`ls /`下的路径,基本是一样的.


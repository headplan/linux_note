# Linux发展历史

一、因AT&T公司和BSD持久的官司，1990年左右，BSD已经基本清除了系统中的Unix代码，所以BSD一类的系统叫做类Unix系统。1990年左右，BSD分支中的Jolitz计划将BSD一直到X86机器（之前Unix一直运行在摩托罗拉生产的CPU之上），后因其合作机构要求将此移植后的系统商业化，导致1991年项目中止，1992年中左右又恢复，此计划叫 386-BSD

1991年8月，Linus Torvalds 宣布成立Linux，其后，Linux壮大，发展，因素如下：

1、遵循GPL

2、1990年后http爆炸式发展，借助互联网优势

3、Larry Wall发明了path，支持代码以补丁的方式制作，是互联网联合开发成为可能

二、Unix和Linux是一个工作在硬件之上的控制程序，负责把底层硬件驱动起来，以及将底层硬件的功能虚拟化提供给程序，并监控这些程序

Kernel 内核的主要功能

1、驱动底层硬件

2、把底层硬件资源抽象为简单的资源

3、管理各程序的运行，把有限资源分配给程序，并让程序之间互不影响

完整的操作系统=Kernel + Application

狭义的操作系统=Kernel

linux的全称应该是 GNU/Liunx

三、Operation System 的接口：

1、GUI :Graphis User Interface

GNome , C ,gtk

KDE      ,C++   ,qt

2、CLI :Command Line Interface

bash

zsh

…

3、TUI :Text User Interface

Operation System 接口也是应用程序。

人对电脑的任何操作，都是通过进程来完成的。

占据接口运行的，叫做前台

不占据接口却能运行的，叫做后台

操作系统的功能：

1、驱动底层硬件

2、进程管理

3、安全

4、网络管理

5、内存管理

6、文件系统管理

……

四、API 和 ABI

API：Application Program Interface 应用程序接口。主要是程序员面对的编程接口

ABI：Application Binary Interface     应用程序二进制接口。主要是程序使用者面对的接口

![](/assets/linuxfazhan.png)

一个系统的应用程序之所以不可以在另外一个操作系统上运行，主要是 ABI 不一样导致

POSIX：Portable Operation System 可一直的操作系统（后面的IX仅做标识使用），这是一个系统标准，遵守此标准的系统，可以使用通用软件。

编码：将源码编译成二进制格式

五、Linux的主要发行版本

1、Debian     是唯一一个没有商业公司支持的发行版本

Ubuntu、Knopix ……

2、SUSE

OpenSUSE

3、RedHat

RedHat Enterprise

Centos

Fedora Core

版本号命名规则：

一般由四个部分组成

第一部分：主版本号

第二部分：子版本号（又叫次版本号）

第三部分：阶段版本号

第四部分：日期版本号加希腊字母版本号

系统使用原则为：不求使用最新系统，最新功能，首要考虑稳定性


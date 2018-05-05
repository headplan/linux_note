# 文件组织结构

```
[root@test /]# ls -l
total 94
dr-xr-xr-x.   2 root root  4096 Aug 24 04:21 bin
dr-xr-xrwx.   5 root root  1024 Nov 14 23:40 boot
drwxr-xr-x.  17 root root  3760 Dec 19 18:25 dev
drwxr-xr-x.  98 root root  4096 Dec 20 18:32 etc
drwxr-xr-x.  12 root root  4096 Sep 29 00:29 home
dr-xr-xr-x.  10 root root  4096 Aug 24 03:32 lib
dr-xr-xr-x.   9 root root 12288 Aug 24 04:21 lib64
drwx------.   2 root root 16384 Aug 24 03:30 lost+found
drwxr-xr-x.   2 root root  4096 Dec  4  2009 media
drwxr-xr-x.   3 root root  4096 Aug 24 03:36 mnt
drwxr-xr-x.   2 root root  4096 Aug 24 03:37 opt
dr-xr-xr-x. 188 root root     0 Dec 12 21:56 proc
dr-xr-x---.  25 root root  4096 Dec  5 00:19 root
dr-xr-xr-x.   2 root root 12288 Aug 24 04:21 sbin
drwxr-xr-x.   7 root root     0 Dec 12 21:56 selinux
drwxr-xr-x.   3 root root  4096 Sep 29 00:30 srv
drwxr-xr-x.  13 root root     0 Dec 12 21:56 sys
drwxrwxrwt.  15 root root  4096 Dec 21 01:03 tmp
drwxr-xr-x.  13 root root  4096 Aug 24 03:30 usr
drwxr-xr-x.  22 root root  4096 Aug 24 03:33 var
```

`/`** - **根目录 , 所有的目录、文件、设备都在/之下 , / 就是Linux文件系统的组织者 , 也是最上级的领导者 .

`/bin`** - **bin 就是二进制\(binary\)英文缩写 , 也叫二进制目录 . 在一般的系统当中 , 都可以在这个目录下找到linux常用的命令 , 二进制\(可执行\)文件 , 包含shell解释器等等 .

`/boot` - Linux的内核及引导系统程序所需要的文件目录 , 在一般情况下 , GRUB或LILO系统引导管理器也位于这个目录 . 通常建议单独分区 , 分区大小100M即可 .

* `/boot/vmlinuz` - 为linux的内核文件
* `/boot/gurb` - 引导管理器

`/cdrom`** **-** **这个目录在刚刚安装系统的时候是空的 . 可以将光驱文件系统挂在这个目录下 . 例如 , `mount /dev/cdrom /cdrom`

`/dev` - dev 是设备\(device\)的英文缩写 . 这个目录对所有的用户都十分重要 . 因为在这个目录中包含了所有linux系统中使用的外部设备 . 但是这里并不是放的外部设备的驱动程序 . 这一点和常用的windows,dos操作系统不一样 . 它实际上是一个访问这些外部设备的端口 . 可以非常方便地去访问这些外部设备 , 和访问一个文件 , 一个目录等 , 没有任何区别 . 比如前面挂载的光驱`mount /dev/cdrom`

`/etc` - etc这个目录是linux系统中最重要的目录之一 . 在这个目录下存放了系统管理时要用到的各种配置文件和子目录 . 要用到的网络配置文件 , 文件系统 , x系统配置文件 , 设备配置信息 , 设置用户信息等都在这个目录下 . 通常该目录下的文件由系统管理员来使用 , 普通用户对大部分文件有只读权限 .

* /etc/inittab
* /etc/fstab
* /etc/init.d
* /etc/X11 - X Window系统有关
* /etc/sysconfig - 与网络有关
* /etc/xinetd.d

`/home` - 系统默认的用户宿主目录 , 新增用户账号时 , 用户的宿主目录都存放在此目录下 , ~表示当前用户的宿主目录 , ~test表示用户test的宿主目录 . 建议单独分区 , 并设置较大的磁盘空间 , 方便用户存放数据 .

`/lib` - lib是库\(library\)英文缩写 . 这个目录是用来存放系统动态连接共享库的 . 系统使用的函数库的目录 , 程序在执行过程中 , 需要调用一些额外的参数时需要函数库的协助 , 该目录下存放了各种编程语言库 . 典型的linux系统包含了C、C++和FORTRAN语言的库文件 . /lib目录下的库映像文件可以用来启动系统并执行一些命令 .

* /lib/modules - 包含了可加载的内核模块

`/lib64` - 和前面的一样 , 64位的 .

`/lost+fount`_ - _在EXT2或EXT3文件系统中 , 当系统意外崩溃或机器意外关机 , 产生的一些文件碎片放在这里 . 在系统启动的过程中fsck工具会检查这里 , 并修复已经损坏的文件系统 . 有时系统发生问题 , 有很多的文件被移到这个目录中 , 可能会用手工的方法来修复 , 或者移动文件到原来的位置上 .

`/mnt` - 这个目录一般是用于存放挂载储存设备的挂载目录的 , 比如有cdrom等目录 . 当挂载了一个设备如光驱时 , 就可以通过访问目录/mnt/cdrom下的文件来访问相应的光驱上的文件 . 可以参看/etc/fstab的定义 .

`/media` - 有些linux的发行版使用这个目录来挂载那些usb接口的移动硬盘\(包括U盘\)、CD/DVD驱动器等等 .

`/opt` - 这里主要存放那些可选的程序 . 给主机额外安装软件所摆放的目录 . 如:FC4使用的Fedora 社群开发软件 , 如果想要自行安装新的KDE 桌面软件 , 可以将该软件安装在该目录下 . 以前的 Linux 系统中 , 习惯放置在 /usr/local 目录下 .

`/proc` - 可以在这个目录下获取系统信息 . 这些信息是在内存中 , 由系统自己产生的 . 如系统核心 , 外部设备 , 网络状态 , 由于数据都存放于内存中 , 所以不占用磁盘空间 .

* /proc/cpuinfo
* /proc/interrupts
* /proc/dma
* /proc/ioports
* /proc/net/\*

`/root` - Linux超级权限用户root的家目录 .

`/sbin` - 这个目录是用来存放系统管理员的系统管理程序 System Binary . 大多是涉及系统管理的命令的存放 , 如fdisk、shutdown、mount等 , 是超级权限用户root的可执行命令存放地 , 普通用户无权限执行这个目录下的命令 , 这个目录和/usr/sbin; /usr/X11R6/sbin或/usr/local/sbin目录是相似的，凡是目录sbin中包含的都是root权限才能执行的 . 而/bin目录中的命令和可执行文件普通用户也可以用 .

`/selinux` - 对SElinux的一些配置文件目录 , SElinux可以让linux更加安全 .

`/srv` - 服务启动后 , 所需访问的数据目录 , 举个例子来说 , www服务启动读取的网页数据就可以放在`/srv/www`中 .

`/sys` - Linux 内核中设计较新的一种虚拟的基于内存的文件系统 , 它的作用与 proc 有些类似 , 但除了与 proc 相同的具有查看和设定内核参数功能之外 , 还有为 Linux 统一设备模型作为管理之用 .

`/tmp` - 临时文件目录 , 用来存放不同程序执行时产生的临时文件 . 有时用户运行程序的时候 , 会产生临时文件 . `/tmp`就用来存放临时文件的 . `/var/tmp`目录和这个目录相似 .

`/usr` - \(Unix System Resource\)这是linux系统中占用硬盘空间最大的目录 . 用户的很多应用程序和文件都存放在这个目录下 . 在这个目录下 , 可以找到那些不适合放在/bin或/etc目录下的额外的工具 .

* `/usr/bin` - 存放应用程序
* `/usr/lib` - 存放不能直接运行的 , 却是许多程序运行所必需的一些函数库文件
* `/usr/local` - 这里主要存放那些手动安装的软件 , 即不是通过“新立得”或apt-get安装的软件 . 它和/usr目录具有相类似的目录结构 . 让软件包管理器来管理/usr目录 , 而把自定义的脚本\(scripts\)放到/usr/local目录下面 . 　　
* `/usr/share` - 存放共享数据 . 比如 /usr/share/fonts 是字体目录 , /usr/share/doc和/usr/share/man帮助文件 .
* `/usr/share/doc` - 系统说明文件存放目录
* `/usr/share/man`_ - _程序说明文件存放目录 , 使用 man ls时会查询/usr/share/man/man1/ls.1.gz的内容

`/var` - 这个目录的内容是经常变动的 , 可以理解为vary的缩写 , /var下有/var/log 这是用来存放系统日志的目录 , /var/ www目录是定义Apache服务器站点存放目录 , /var/lib 用来存放一些库文件 , 比如MySQL的 , 以及MySQL数据库的的存放地 . 


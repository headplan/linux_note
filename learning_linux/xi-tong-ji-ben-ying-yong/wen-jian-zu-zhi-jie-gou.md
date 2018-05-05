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






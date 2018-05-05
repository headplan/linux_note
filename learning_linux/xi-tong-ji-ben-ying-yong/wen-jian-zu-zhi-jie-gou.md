# 文件组织结构

```
[root@test /]# ls -l
total 94
dr-xr-xr-x.   2 root root  4096 Aug 24 04:21 bin
dr-xr-xrwx.   5 root root  1024 Nov 14 23:40 boot
drwxr-xr-x.   2 root root  4096 Jul 14  2010 cgroup
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

**`/` - **根目录 , 所有的目录、文件、设备都在/之下 , / 就是Linux文件系统的组织者 , 也是最上级的领导者 . 

**`/bin` - **bin 就是二进制\(binary\)英文缩写 , 也叫二进制目录 . 在一般的系统当中 , 都可以在这个目录下找到linux常用的命令 , 二进制\(可执行\)文件 , 包含shell解释器等等 . 

**`/boot`** - Linux的内核及引导系统程序所需要的文件目录，比如 vmlinuz initrd.img 文件都位于这个目录中。在一般情况下，GRUB或LILO系统引导管理器也位于这个目录。 　　

**/cdrom**：这个目录在刚刚安装系统的时候是空的。可以将光驱文件系统挂在这个目录下。例如：mount /dev/cdrom /cdrom 　　


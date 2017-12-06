# Kali Linux

#### 烧录启动U盘

#### hdiutil

`hdituil`是一个Mac OS上面处理镜像文件的命令 , 可以对镜像文件进行制作,验证和转换等...

如果需要把下载的Ubuntu安装文件`.iso`转换成`.dmg`格式的文件 , 方便在Mac OS上面进行操作 , 可以使用该命令 :

```
hdiutil convert -format UDRW -o ubuntu.iso ubuntu-14.04.5-desktop-amd64.iso
```

* `-format`为生成文件的权限,
* `UDRW`表示转换成有`read/write`的权限的镜像

不是Mac OS上可以不用转换 . 后面直接dd烧录即可 , 如果在Mac OS上安装 , 也要将dmg重命名\(mv\)为iso , 安装时更好识别 .

#### diskutil

操作本地磁盘 , 可以对磁盘进行卸载,挂载等操作 .

**Mac查看USB设备编号**

```asciidoc
diskutil list
# 可以看到类似的消息
dev/disk0 (internal, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *251.0 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:          Apple_CoreStorage Macintosh HD            250.1 GB   disk0s2
   3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3
/dev/disk1 (internal, virtual):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:                  Apple_HFS Macintosh HD           +249.8 GB   disk1
                                 Logical Volume on disk0s2
                                 45CD1187-14DE-4203-9895-FBB1B3770F1E
                                 Unencrypted
/dev/disk2 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     Apple_partition_scheme                        *8.1 GB     disk2
   1:        Apple_partition_map                         4.1 KB     disk2s1
   2:                  Apple_HFS                         2.4 MB     disk2s2
```

**Linux查看USB设备编号**

```
fdisk -l
```

假如查看的设备编号是`/dev/disk2`

#### dd

把安装文件写入U盘 .

`dd`是`Unix`和类`Unix`系统上的命令 , 作用就是用指定大小的块拷贝一个文件 , 并在拷贝的同时进行指定的转换 .

**使用dd命令烧录**

```
sudo dd if=/Users/headplan/Desktop/kali.iso of=/dev/disk2 bs=1m
```

命令必须使用`root`权限

* `if`输入的文件名

* `of`输出的文件名

* `bs`是块大小 , 这里使用`1m`的块大小

漫长的等待 , 写入完成 :

```
1052+1 records in
1052+1 records out
1104052224 bytes transferred in 249.471583 secs (4425563 bytes/sec)
```

Mac下如果遇到`dd: /dev/disk2: Resource busy`错误 , 先使用`diskutil unmountDisk /dev/disk2`命令卸载磁盘再烧录

**查看烧录进度**

```
sudo killall -29 dd
```

**安全拔出U盘**

```
sudo eject /dev/rdisk2
```

#### 销毁安装数据

烧录后的U盘会影响U盘的使用 , 会只显示几百K可用 , 可以把U盘格式化清除数据 , 也可以使用`dd`命令销毁磁盘数据 :

```
sudo dd if=/dev/urandom of=/dev/rdisk2
```

使用随机数填充U盘 , 可以用来销毁数据 , 一般用于重要数据否则没有必要使用随机数填充 .


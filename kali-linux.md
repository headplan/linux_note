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

**使用dd命令烧录**

```
sudo dd if=/Users/headplan/Desktop/kali.iso of=/dev/disk2 bs=1m
```

Mac下如果遇到`dd: /dev/disk2: Resource busy`错误 , 先使用`diskutil unmountDisk /dev/disk2`命令卸载磁盘再烧录

安装过程基本没有配合 , 下一步安装 .


# 正式开始

[http://www.myhack58.com/Article/sort099/sort0102/2011/32363\_7.htm](http://www.myhack58.com/Article/sort099/sort0102/2011/32363_7.htm)

[http://www.centoscn.com/image-text/setup/2014/1128/4199.html](http://www.centoscn.com/image-text/setup/2014/1128/4199.html)

> Install or upgrade an existing system 安装或升级现有的系统
>
> install system with basic video driver 安装过程中采用 基本的显卡驱动
>
> Rescue installed system 进入系统修复模式
>
> Boot from local drive 退出安装从硬盘启动
>
> Memory test 内存检测

选择第一个安装系统

出现是否对CD媒体进行测试的提问,这里选择"Skip"跳过测试.

Next下一步,选择安装过程语言,默认英文.键盘选择U.S.English,同样默认.然后选择第一项,基本存储设备.

提示是否需要格式化磁盘,选择第一项Yes忽略所有数据.

设置主机名,安装完成之后再修改,这里设置为headplan.下面的配置网络Configure Network安装完系统之后再修改即可.

下一步选择时区,Asia/Shanghai.在"System clock user UTC"取消前面打勾,不使用UTC时间.

设置root密码,\*\*\*\*\*\*

> **使用所有空间（Use All Space ）： **  
> 选择此选项，删除您硬盘上的所有分区（这包括如Windows的NTFS分区VFAT或其他操作系统创建的分区）。
>
> **替换现有的Linux系统（Replace Existing Linux System）： **  
> 选择此选项，以消除先前的Linux安装创建的分区。 这不会删除其他分区（如VFAT或FAT32分区），你可能对您的硬盘驱动器。
>
> **宿小现有系统（Shrink Current System）： **  
> 选择此选项，调整当前的数据和分区安装在手动释放的空间是一个默认的红帽企业Linux布局。
>
> **使用剩余空间（Use Free Space）： **  
> 选择此选项以保留您当前的数据和分区并安装在未使用的存储驱动器上的空间可用的Scientific。 确保有足够的存储驱动器上的可用空间，然后再选择此选项。
>
> **创建自定义布局（Create Custom Layout）： **  
> 选择此选项，手动存储设备进行分区并创建自定义布局。
>
> 下面有两个勾选项,一个是加密分区,一个是查看并修改分区布局

选择最后一项,自定义分区布局.

**分区的选择**

标准分区\(选择标准分区\)

RAID分区\(软RAID没用\)

LVM扩展\(一般都会先规划好,不需要扩展\)

**开始分区**

![](/assets/import.png)

**挂载点：选择"/boot"**

文件系统类型：使用默认“Ext4 日志文件系统”

大小：输入分配的大小200，以 MB 为单位

其它大小选项：选择“固定大小”。

选择强制为主分区

点“确定”按钮。

**创建交换空间**

继续选择空闲空间,点“创建”后,就会出现上面的画面。

文件系统类型 - 选择“swap”

其它大小选项 - 一般为内存的1.5倍,如果为8G,最大就给到8G

选择强制为主分区

点“确定”按钮。

**挂载点：选择"/"**

文件系统类型：使用默认“Ext4 日志文件系统”

大小：选择使用全部可用空间

选择强制为主分区

点“确定”按钮。

至此，分区已全部创建完毕，如果不满意，还可以点击“重设”按钮进行更改。如果确定，就点“下一步”按钮后，弹出“是否格式化以下已存在的硬盘”，选择“格式化”。

安装程序会提示您确认您所选的分区选项。单击“将修改写入磁盘”，以允许安装程序在您的硬盘进行分区，并安装系统更改。

接下来为GRUB引导安装窗口，可采用默认设置，直接单击“下一步”按钮即可.

**选择安装的软件包**

Desktop - 基本的桌面系统，包括常用的桌面软件，如文档查看工具。

Minimal Desktop - 基本的桌面系统，包含的软件更少。

**Minimal - 基本的系统，不含有任何可选的软件包。\(一般选择最小化安装\)**

Basic Server - 安装的基本系统的平台支持，不包含桌面。

Database Server - 基本系统平台，加上MySQL和PostgreSQL数据库，无桌面。

Web Server - 基本系统平台，加上PHP，Web server，还有MySQL和PostgreSQL数据库的客户端，无桌面。

Virtual Host - 基本系统加虚拟平台。

Software Development Workstation - 包含软件包较多，基本系统，虚拟化平台，桌面环境，开发工具。

选择Minimal,然后选择Customize now自定义.

**挑选软件包**

Base System

=&gt; Base

=&gt; Compatibllity libraries

=&gt; Debugging Tools

Development

=&gt; Development Tools

之后下一步开始安装,最后重启.

完成安装,CentOS 6需要在加载时按ESC才能看到启动过程,不然则只显示进度条.


# 正式开始

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

标准分区

RAID分区\(软RAID没用\)

LVM扩展\(一般都会先规划好,不需要扩展\)


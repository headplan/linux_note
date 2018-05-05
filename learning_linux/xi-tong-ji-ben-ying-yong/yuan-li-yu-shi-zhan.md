# 原理与实战

举例

统计两个文件一共有多少个IP ?

```
cat ./file1 ./file2 | sort | uniq | wc -l
```

如何查看压缩包test.zip内 , 有没有包含test.so文件 ?

```
unzip -l test.zip | grep test.so | tail -c 9
```

#### 启动过程

* BIOS 检查硬件，读取主启动磁盘MBR区的系统装载程序（Boot Loader，CentOS中一般为GRUB）并执行，显示给用户一个选择界面。
* 用户选择要启动的系统，即选定了相应的内核（vmlinuz）, Boot Loader 通过 initrd 在内存中建立一个供内核使用的临时文件系统，然后由内核程序接管后续启动流程。
* 内核开始初始化系统中的各部分硬件。此时操作系统的基本环境已建立，但还没有用户程序可供人使用，于是内核继续执行，启动Linux世界中的造物主 —— **/sbin/init **
* **/sbin/init** 进程启动后，自然成为 **Linux 中所有进程的父/爷进程**。它会首先**调用 /etc/rc.d/rc.sysinit 脚本**，完成设置环境变量，交换分区，初始化系统时钟等工作。然后**调用/etc/inittab**，执行相应运行级别下的程序脚本（/etc/rc.d/rc&lt;x&gt;.d/\* 就是开机自启动的一些脚本等）启动或杀掉相应进程。
* 各启动脚本执行完毕后，init 按/etc/inittab 中的配置启动相应的控制台交互界面，提示用户登录（字符界面下默认有6个虚拟控制台，Alt+Fx 切换）

**设置程序自动启动的方法**

也就是前面提到的第四步时 , 执行响应运行级别下的程序脚本 . 自动启动就下面这三个 : 

* /etc/rc.d/rc.local  中写启动命令 , 写一些shell , 或其他一些脚本
* /etc/rc.d/init.d/\*  写shell脚本，然后在 /etc/rc\*.d 中建立软连接
* 使用 chkconfig 工具 ,  如 chkconfig --level 2345 auditd on , 这里你要启动的auditd , 设置成on就可以了 . 可以直接写 : 
  * chkconfig auditd on

#### 帮助文档

**man**

unix 中传统的文档格式

```
基本用法：
$ man [section] name

指定文档目录：
$ man -M /manual/path name

查看所有 section:
$ man -a name

例如
man top
```

**info**

GNU 项目推荐的新一代文档格式 , 功能更强 . 

```
m 显示菜单
f 跟随交叉引用，l 返回
```

**help**

```
# 查看大部分程序自带的帮助文档
-h
--help
```

#### 文件系统

#### 

#### 文件查找

#### 文本工具

#### 管道组合

#### 系统管理




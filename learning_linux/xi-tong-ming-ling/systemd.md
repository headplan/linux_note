# Systemd {#page-title}

> Systemd即为system daemon , 是linux下的一种init软件 , 由Lennart Poettering带头开发 , 并在LGPL 2.1及其后续版本许可证下开源发布 , 开发目标是提供更优秀的框架以表示系统服务间的依赖关系 , 并依此实现系统初始化时服务的并行启动 , 同时达到降低Shell的系统开销的效果 , 最终代替现在常用的System V与BSD风格init程序 .
>
> 与多数发行版使用的System V风格init相比 , systemd采用了以下新技术 :
>
> \(1\) 采用Socket激活式与总线激活式服务 , 以提高相互依赖的各服务的并行运行性能 ;
>
> \(2\) 用Cgroups代替PID来追踪进程 , 以此即使是两次fork之后生成的守护进程也不会脱离systemd的控制 .
>
> Systemd已纳入众多Linux发行版的软件源中 , 所有使用GNOME的发行版都应该使用systemd , 最低限度来说也必须将其作为配置选项之一 .
>
> 当前绝大多数的Linux发行版都已采用systemd代替原来的System V .

以前 , Linux的启动一直采用init进程 . 例如

```
sudo /etc/init.d/apache2 start
# 或者
$ service apache2 start
```

缺点是 :

启动时间长 . init进程是串行启动 , 只有前一个进程启动完 , 才会启动下一个进程 .

启动脚本复杂 . init进程只是执行启动脚本 , 不管其他事情 . 脚本需要自己处理各种情况 , 往往使得脚本变得冗长 .

#### System诞生

Systemd的诞生解决了上面的问题 , 它的设计目标就是为系统的启动和管理提供一套完整的解决方案 .

使用了Systemd , 就不需要再用init了 . Systemd取代了initd , 成为系统的第一个进程 , 也就是**PID 1** , 其他进程都是它的子进程 .

```
systemctl --version
```

Systemd 的优点是功能强大 , 使用方便 , 缺点是体系庞大 , 非常复杂 . 很多人反对使用 Systemd , 理由就是它过于复杂 , 与操作系统的其他部分强耦合 , 违反"keep simple, keep stupid"的Unix哲学 .

#### Systemd组件

![](/assets/systemdjiagou.png)

#### 系统管理

Systemd 并不是一个命令 , 而是一组命令 , 涉及到系统管理的方方面面 . 

##### systemctl

`systemctl`是Systemd的主命令 , 用于管理系统 . 

```
# 重启系统
$ sudo systemctl reboot

# 关闭系统，切断电源
$ sudo systemctl poweroff

# CPU停止工作
$ sudo systemctl halt

# 暂停系统
$ sudo systemctl suspend

# 让系统进入冬眠状态
$ sudo systemctl hibernate

# 让系统进入交互式休眠状态
$ sudo systemctl hybrid-sleep

# 启动进入救援状态（单用户状态）
$ sudo systemctl rescue
```

##### systemd-analyze

`systemd-analyze`命令用于查看启动耗时 . 

```
# 查看启动耗时
$ systemd-analyze

# 查看每个服务的启动耗时
$ systemd-analyze blame

# 显示瀑布状的启动过程流
$ systemd-analyze critical-chain

# 显示指定服务的启动流
$ systemd-analyze critical-chain atd.servic
```

##### hostnamectl

`hostnamectl`命令用于查看当前主机的信息

```
# 显示当前主机的信息
$ hostnamectl

# 设置主机名
$ sudo hostnamectl set-hostname rhel7
```

##### localectl

`localectl`命令用于查看本地化设置

```
# 查看本地化设置
$ localectl

# 设置本地化参数。
$ sudo localectl set-locale LANG=en_GB.utf8
$ sudo localectl set-keymap en_GB
```

##### timedatectl

`timedatectl`命令用于查看当前时区设置

```
# 查看当前时区设置
$ timedatectl

# 显示所有可用的时区
$ timedatectl list-timezones

# 设置当前时区
$ sudo timedatectl set-timezone America/New_York
$ sudo timedatectl set-time YYYY-MM-DD
$ sudo timedatectl set-time HH:MM:SS
```

##### loginctl

`loginctl`命令用于查看当前登录的用户

```
# 列出当前session
$ loginctl list-sessions

# 列出当前登录用户
$ loginctl list-users

# 列出显示指定用户的信息
$ loginctl show-user headplan
```

#### Unit

Systemd可以管理所有系统资源 . 不同的资源统称为Unit\(单位\) . 

Unit一共分成12种 : 

* Service unit : 系统服务
* Target unit : 多个 Unit 构成的一个组
* Device Unit : 硬件设备
* Mount Unit : 文件系统的挂载点
* Automount Unit : 自动挂载点
* Path Unit : 文件或路径
* Scope Unit : 不是由 Systemd 启动的外部进程
* Slice Unit : 进程组
* Snapshot Unit : Systemd 快照 , 可以切回某个快照
* Socket Unit : 进程间通信的 socket
* Swap Unit : swap 文件
* Timer Unit : 定时器

**相关连接**

[https://zh.wikipedia.org/wiki/Systemd](https://zh.wikipedia.org/wiki/Systemd)

[https://baike.baidu.com/item/systemd/18473007?fr=aladdin](https://baike.baidu.com/item/systemd/18473007?fr=aladdin)

[http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)


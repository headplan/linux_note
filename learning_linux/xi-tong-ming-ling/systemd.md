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

`systemctl list-units`命令可以查看当前系统的所有Unit

```
# 列出正在运行的 Unit
$ systemctl list-units

# 列出所有Unit，包括没有找到配置文件的或者启动失败的
$ systemctl list-units --all

# 列出所有没有运行的 Unit
$ systemctl list-units --all --state=inactive

# 列出所有加载失败的 Unit
$ systemctl list-units --failed

# 列出所有正在运行的、类型为 service 的 Unit
$ systemctl list-units --type=service
```

##### Unit 的状态

`systemctl status`命令用于查看系统状态和单个Unit的状态 .

```
# 显示系统状态
$ systemctl status

# 显示单个Unit的状态
$ systemctl status bluetooth.service

# 显示远程主机的某个Unit的状态
$ systemctl -H root@rhel7.example.com status httpd.service
```

除了`status`命令 , `systemctl`还提供了三个查询状态的简单方法 , 主要供脚本内部的判断语句使用 .

```
# 显示某个Unit是否正在运行
$ systemctl is-active application.service

# 显示某个Unit是否处于启动失败状态
$ systemctl is-failed application.service

# 显示某个Unit服务是否建立了启动链接
$ systemctl is-enabled application.service
```

##### Unit 管理

对于用户来说 , 还是类似启动 , 重启一个服务的命令比较常用  :

```
# 立即启动一个服务
$ sudo systemctl start apache.service

# 立即停止一个服务
$ sudo systemctl stop apache.service

# 重启一个服务
$ sudo systemctl restart apache.service

# 杀死一个服务的所有子进程
$ sudo systemctl kill apache.service

# 重新加载一个服务的配置文件
$ sudo systemctl reload apache.service

# 重载所有修改过的配置文件
$ sudo systemctl daemon-reload

# 显示某个Unit的所有底层参数
$ systemctl show httpd.service

# 显示某个Unit的指定属性的值
$ systemctl show -p CPUShares httpd.service

# 设置某个Unit的指定属性
$ sudo systemctl set-property httpd.service CPUShares=500
```

##### 依赖关系

Unit之间存在依赖关系 . 假如 , A依赖于B , 就意味着Systemd在启动A的时候 , 同时会启动B .

```
# 列出一个Unit的所有依赖
$ systemctl list-dependencies nginx.service

# 列出一个Unit的所有依赖,包括Target类型依赖
$ systemctl list-dependencies --all nginx.service
```

**相关连接**

[https://zh.wikipedia.org/wiki/Systemd](https://zh.wikipedia.org/wiki/Systemd)

[https://baike.baidu.com/item/systemd/18473007?fr=aladdin](https://baike.baidu.com/item/systemd/18473007?fr=aladdin)

[http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)


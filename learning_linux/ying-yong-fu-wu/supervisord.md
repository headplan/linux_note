# Supervisord

官网 : [http://supervisord.org/](http://supervisord.org/)

#### 简单介绍

Supervisor是一个Client/Server模式的系统 , 允许用户在类unix操作系统上监视和控制多个进程 , 或者可以说是多个程序 . Supervisor与launchd , daemontools , runit等程序有着相同的功能 , 与其中某些程序不同的是 , 它并不作为"ID为1的进程"而替代init . 相反 , 它用于控制应用程序 , 像启动其它程序一样 . 通俗理解就是 , 把Supervisor服务管理的进程程序 , 它们作为Supervisor的子进程来运行 , 而Supervisor是父进程 . Supervisor来监控管理子进程的启动关闭和异常退出后的自动启动 .

#### Supervisor与系统自带init进程管理比较

**方便**

通常管理linux进程的时候 , 有些编译运行的程序在安装完成后 , 需要为他们编写启动停止管理脚本 , 实现进程start/stop/restart/reload功能 , 然后丢到/etc/init.d/下面 . 而且进程在异常崩溃结束时 , 许多程序都不会正确重新启动的 . Supervisord启动管理的程序进程是作为其子进程来运行的 , 并且可以配置为在进程崩溃停止时自动重新启动它们 . 




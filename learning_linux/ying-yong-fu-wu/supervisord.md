# Supervisord

官网 : [http://supervisord.org/](http://supervisord.org/)

#### Supervisor是什么

Supervisor是一个Client/Server模式的系统 , 允许用户在类unix操作系统上监视和控制多个进程 , 或者可以说是多个程序 . Supervisor与launchd , daemontools , runit等程序有着相同的功能 , 与其中某些程序不同的是 , 它并不作为"ID为1的进程"而替代init . 相反 , 它用于控制应用程序 , 像启动其它程序一样 . 通俗理解就是 , 把Supervisor服务管理的进程程序 , 它们作为Supervisor的子进程来运行 , 而Supervisor是父进程 . Supervisor来监控管理子进程的启动关闭和异常退出后的自动启动 .

#### Supervisor与系统自带init进程管理比较

**方便**

通常管理linux进程的时候 , 有些编译运行的程序在安装完成后 , 需要为他们编写启动停止管理脚本 , 实现进程start/stop/restart/reload功能 , 然后丢到/etc/init.d/下面 . 而且进程在异常崩溃结束时 , 许多程序都不会正确重新启动的 . Supervisord启动管理的程序进程是作为其子进程来运行的 , 并且可以配置为在进程崩溃停止时自动重新启动它们 .

**精准**

在Unix上的进程通常很难获得准确的up/down状态 . Pidfiles经常说谎 , Supervisord将进程作为子进程启动 , 所以它总是知道其子进程的正确的up/down状态 , 可以方便的对这些数据进行查询 .

**托管**

我们不希望或不需要完整的shell访问进程运行的机器 . 在底层TCP端口上侦听的进程通常需要作为根用户启动和重新启动\(UNIX的一个错误特性\) . 通常情况下 , 允许普通用户停止或重启这样的进程是完全可以的 , 但是为他们提供shell访问通常是不切实际的 , 而为他们提供根访问或sudo访问通常是不可能的 . 向他们解释为什么会存在这个问题也是困难的 . 如果将Supervisor作为根用户启动 , 就有可能允许普通用户控制此类流程 , 而不需要向他们解释问题的复杂性 . 通过从一个简单的shell或web UI发出"stop"、"start"和"restart"命令 , Supervisorctl允许对机器进行非常有限的访问 , 基本上允许用户查看进程状态并控制受监视控制的子进程 . 

**进程分组**

进程支持分组启动和停止 , 也支持启动顺序 , 即优先级 . Supervisor允许为进程分配优先级 , 并允许用户通过Supervisorctl客户端发出命令 , 如"全部启动"和"重新启动所有" , 它们以预先分配的优先级顺序启动 . 还可以将进程分为"进程组" , 一组逻辑关联的进程可以作为一个单元停止或启动 .


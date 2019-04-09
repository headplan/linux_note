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

#### Supervisor特性

**简单**

Supervisor是通过一个简单的ini风格的配置文件来配置的 , 很容易学习 . 它提供了许多进程选项 , 使您的工作更容易 , 例如重新启动失败的进程和自动日志循环 .

**一站式**

Supervisor提供了一个开始、停止和监视流程的控制台 . 进程可以单独控制 , 也可以分组控制 . 可以通过配置Supervisor提供本地或远程命令行和web界面 .

**高效**

Supervisor通过fork/exec启动它的子进程 , 而不是守护 . 当进程终止时 , 操作系统立即向Supervisor发出信号 , 这与某些解决方案不同 , 这些解决方案依赖于容易出错的的PID文件和定期轮询来重启失败的进程 .

**可扩展**

Supervisor有一个简单的事件通知协议 , 用任何语言编写的程序都可以使用它来监视它 , 还有一个XML-RPC接口用于控制 . 它也可以由Python开发人员利用扩展点构建 .

**兼容性**

Supervisor除了windows系统 , 其他系统均可以使用 . 它在Linux、Mac OS X、Solaris和FreeBSD上均得到了测试和支持 . 它完全用Python编写 , 所以安装不需要C编译器 .

**可靠**

虽然Supervisor在今天被非常积极的开发 , 但是它并不是一个新的软件 . Supervisor已经存在多年 , 并且已经在许多服务器上使用 .

#### Supervisor组件

**Supervisord**

Supervisor服务部分叫做Supervisord . 它负责自己调用时启动子程序 , 响应来自客户机的命令 , 重新启动崩溃或退出的子进程 , 记录子进程挂掉和崩溃的输出 , 并生成和处理与子进程生命周期中的点对应的"事件" . 

它使用了一个配置文件 . 配置文件通常位于/etc/supervision.conf中 . 这个配置文件是一个"Windows-INI"风格的配置文件 . 通过适当的文件系统权限保持该文件的安全性非常重要 , 因为它可能包含未加密的用户名和密码 . 

通俗点讲就是Supervisor的处理器 . 

**Supervisorctl**

Supervisorctl是Supervisor命令行客户端 . 它提供了一个类shell的接口 , 用于管理Supervisor提供的特性 . 用户可以连接到不同的监控器进程\(一次一个\) , 获取受控子进程的状态 , 停止和启动的子进程 , 以及监控器的运行进程列表 . 

通俗点讲就是Supervisor的命令工具 . 

**Web Server**

如果配置中启动了这个模块 , 就可以通过浏览器访问具有与supervisorctl类似功能的web用户界面 . 在配置文件的\[inet\_http\_server\]部分开启 , 访问服务器URL\(例如http://localhost:9001/\) , 通过web接口查看和控制进程状态 . 

通俗点讲就是一个可视化界面 , 可以在界面操作进程 . 

**XML-RPC Interface**

Web UI基于XML-RPC接口服务 , 该接口可用于询问和控制Supervisor及其运行的程序 . 




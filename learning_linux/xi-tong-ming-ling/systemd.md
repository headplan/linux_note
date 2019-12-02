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

**相关连接**

[https://zh.wikipedia.org/wiki/Systemd](https://zh.wikipedia.org/wiki/Systemd)

[https://baike.baidu.com/item/systemd/18473007?fr=aladdin](https://baike.baidu.com/item/systemd/18473007?fr=aladdin)

[http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)


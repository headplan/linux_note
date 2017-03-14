# Linux系统基础使用入门

#### 登录

root/\*\*\*\*\*\*

图形界面 - startx &

#### 终端

用户与主机交互,必然用到的设备,即终端设备.

物理终端 - 直接接入本机的显示器和键盘设备,也叫做控制台. /dev/console

虚拟终端 - 附加在物理终端之上的以软件方式虚拟实现的终端,CentOS 6默认启动6个虚拟终端\(Ctrl+Alt+F\#: \[1,6\]\)

=&gt;图形终端 - 附加在物理终端之上的以软件方式虚拟实现的终端,但额外会提供桌面环境.

模拟终端 - 图形界面下打开的命令行接口,基于ssh协议或telnet协议等远程打开的界面.

**查看当前的终端设备** , 使用命令tty即可.\(设备文件路径\)

物理终端 - /dev/console

虚拟终端 - /dev/tty1

模拟终端 - /dev/pts/0

**交互式接口** - 启动终端后,在终端设备附加一个交互式应用程序,这样才能进行交互.

GUI：图形界面

```
X protocol, window manager, desktop
Desktop:
    GNOME (C, gtk)
    KDE   (C++, qt)
    XFCE  (轻量级桌面)
```

CLI：命令行

```
shell程序：
    sh (bourn研发的)
    csh 
    tcsh
    ksh (korn)
    bash (bourn again shell), sh的二次开发版,遵循GPL协议,是开源的
    zsh 

显示当前使用的shell：
    # echo ${SHELL}

显示当前系统使用的所有shell：
    # cat /etc/shells

命令提示符(prompt)
    [root@localhost ~]
    上面的内容是PS1,它的显示格式可以echo ${PS1}查看
        命令提示符仅是#或$符：
            管理员：#
            普通用户：$
```




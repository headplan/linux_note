# /etc目录

/etc/rc，/etc/rc.d，/etc/rc\*.d启动、或改变运行级时运行的scripts或scripts的目录。

_/etc/passwd_用户[数据库](http://lib.csdn.net/base/mysql)，其中的域给出了用户名、真实姓名、家目录、加密的口令和用户的其他信息。

/etc/fstab启动时mount -a命令\(在/etc/rc 或等效的启动文件中\)自动mount的文件系统列表。Linux下，也包括用swapon -a启用的swap区的信息。

_/etc/group_类似/etc/passwd ，但说明的不是用户而是用户组。

_/etc/inittab_init 的配置文件，设定系统启动时init进程将把系统设置成什么样的runlevel 。

_/etc/issue_getty 在登录提示符前的输出信息.通常包括系统的一段短说明或欢迎信息内容由系统管理员确定。

_/etc/motd_Message Of The Day，成功登录后自动输出内容由系统管理员确定，经常用于通告信息，如计划关机时间的警告。

_/etc/mtab_当前安装的文件系统列表.由scripts初始化，并由mount 命令自动更新，需要一个当前安装的文件系统的列表时使用，例如df 命令。

_/etc/shadow_在安装了影子口令软件的系统上的影子口令文件.影子口令文件将/etc/passwd 文件中的加密口令移动到/etc/shadow 中，而后者只对root可读这使破译口令更困难.

_/etc/login.defs_login 命令的配置文件。

_/etc/printcap_类似/etc/termcap ，但针对打印机语法不同。

_/etc/profile , /etc/csh.login , /etc/csh.cshrc_登录或启动时Bourne或C shells执行的文件，这允许系统管理员为所有用户建立全局缺省环境。

_/etc/securetty_确认安全终端，即哪个终端允许root登录.一般只列出虚拟控制台，这样就不可能\(至少很困难\)通过modem或网络闯入系统并得到超级用户特权。

_/etc/shells_列出可信任的shell.chsh 命令允许用户在本文件指定范围内改变登录shell.提供一台机器FTP服务的服务进程ftpd 检查用户shell是否列在 /etc/shells 文件中，如果不是将不允许该用户登录.

_/etc/sysconfig_网络配置相关目录

_/etc/DIR\_COLORS_ 设定颜色

_/etc/HOSTNAME_ 设定用户的节点名

_/etc/NETWORKING_ 只有YES标明网络存在

_/etc/host.conf_文件说明用户的系统如何查询节点名

_/etc/hosts_ 设定用户自已的IP与名字的对应表

_/etc/hosts.allow_ 设置允许使用inetd的机器使用

_/etc/hosts.deny_ 设置不允许使用inetd的机器使用

_/etc/hosts.equiv_ 设置远端机不用密码

_/etc/inetd.conf_ 设定系统网络守护进程inetd的配置

_/etc/inetd.pid_ inetd这个进程的进程id

_/etc/hosts.lpd_ 设定远端有哪些节点可以使用本机的打印机

_/etc/gateways_ 设定路由器

_/etc/protocols_ 设定系统支持的协议

_/etc/named.boot_ 设定本机为名字服务器的配置文件

_/etc/named.pid_ 本机上运行的名字服务器的进程id

_/etc/networks_ 设定网络的配置文件

_/etc/resolv.conf_ 设定系统的名字服务器

_/etc/services_ 设定系统的端品与协议类型和提供的服务

_/etc/exports_ 设定NFS系统用的

_/etc/NNTP\_INEWS\_DOMAIN_ 设置新闻服务器的配置文件

_/etc/nntpserver_ 设置用户使用的新闻服务器的地址

_/etc/XF86Config_ X Window的配置文件

_/etc/hostid_ 系统独有的一个硬件id

_/etc/at.deny_ 设置哪些用户不能使用at命令

_/etc/bootptab_ 给MAKEDEV程序设定各种不同的设备驱动文件的格式

_/etc/makedev.cfg_ 同DEVINFO一样给MAKEDEV使用的设置文件

_/etc/diphosts_ 设置拔号服务器的用户名和口令

_/etc/slip.hosts,/etc/slip.login_ 设定SLIP的配置文件

_/etc/fastboot_ 使用shutdown -f产生的，重启系统要查这个文件

_/etc/fstab_ 记录开机要mount的文件系统

_/etc/ftpaccess_ FTP服务器的一些配置

_/etc/ftpconversions_ 设定在FTP时使用的过滤器的位置

_/etc/ftpusers_ 设定不能使用FTP服务的用户

_/etc/ld.so.cache_ 查找系统动态链接库的缓存 

_/etc/ld.so.conf_ 系统动态链接库的路径

_/etc/lilo.conf_ lilo的配置文件

_/etc/magic_ 给file命令使用的

_/etc/aliases_ 给sendmail使用的设置别名的文件

_/etc/mail.rc,_

_/etc/mailcap,_

_/etc/sendmail.cf,_

/_etc/sendmail.st_ 设置sendmail的

_/etc/motd_ 超级用户发布通知的地方

_/etc/organization_ 存放用户的名字和组织

_/etc/pnpdevices_ 列出支持的Plug&Play设备

_/etc/snooptad_监控用户的屏幕，监听的终端列表

_/etc/sudoers_ 可以sudo命令的配置文件

/etc/syslog.conf 系统记录程序syslogd的配置文件

/etc/utmp 目前在用系统的用户信息

/etc/wtmp 同utmp差不多，只是它累加

/etc/nologin 系统在shutdown时不希望用户登录就产生这个文件

/etc/termcap 设置系统终端信息的

/etc/ttys 设定系统的终端类型

/etc/gettydefs getty\_ps的定义文件

/etc/yp.conf NIS的配置文件

/etc/mtools.conf 设定mtools程序的参数

/etc/fdprm 设定格式化软盘的参数

/etc/login.access 控制用户登录权限的文件 




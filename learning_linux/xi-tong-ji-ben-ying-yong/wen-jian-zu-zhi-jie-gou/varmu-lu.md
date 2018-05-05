# /var目录

/var 包括系统一般运行时要改变的数据.每个系统是特定的，即不通过网络与其他计算机共享。

/var/catman 当要求格式化时的man页的cache.man页的源文件一般存在/usr/man/man\* 中；有些man页可能有预格式化的版本，存在/usr/man/cat\* 中.而其他的man页在第一次看时需要格式化，格式化完的版本存在/var/man 中，这样其他人再看相同的页时就无须等待格式化了. \(/var/catman 经常被清除，就象清除临时目录一样.\)

/var/lib 系统正常运行时要改变的文件。

/var/local，/usr/local 中安装的程序的可变数据\(即系统管理员安装的程序\).注意，如果必要，即使本地安装的程序也会使用其他/var 目录，例如/var/lock 。

/var/lock 锁定文件.许多程序遵循在/var/lock 中产生一个锁定文件的约定，以支持他们正在使用某个特定的设备或文件.其他程序注意到这个锁定文件，将不试图使用这个设备或文件。

/var/log 各种程序的Log文件，特别是login \(/var/log/wtmp log所有到系统的登录和注销\) 和syslog \(/var/log/messages 里存储所有核心和系统程序信息. /var/log 里的文件经常不确定地增长，应该定期清除。

/var/run 保存到下次引导前有效的关于系统的信息文件.例如， /var/run/utmp 包含当前登录的用户的信息。

/var/spool，/var/mail, /var/news  打印队列和其他队列工作的目录.每个不同的spool在/var/spool 下有自己的子目录，例如，用户的邮箱在/var/spool/mail 中。

/var/tmp 比/tmp 允许的大或需要存在较长时间的临时文件。 \(虽然系统管理员可能不允许/var/tmp 有很旧的文件.\)


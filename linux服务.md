# SSH服务

SSH全称Secure Shell是一种加密的网络协议.使用该协议的数据将被加密,如果在传输中间数据泄漏,也可以确保没有人能读取出有用信息.要使用SSH,目标机器应该安装SSH服务端应用程序,因为SSH是基于客户-服务模式的.当你想安全的远程连接到主机,可中间的网络\(比如因特网\)并不安全,通常这种情况下就会使用SSH.

一般情况下系统最小安装,SSH也是安装了的,如果恰巧没有安装,可以使用

```
sudo apt-get install openssh-client # 客户端
sudo apt-get install openssh-server # 服务端
yum install openssh-server openssh-client
```

SSH服务默认是开启的,并且开机自动启动

```
service sshd status # 服务状态
ls /etc/systemd/system/multi-user.target.wants/ # systmed服务查看开机自启动
chkconfig –list # SysV服务查看开机自动启
```

> SSH和SElinux没有直接的冲突,防火墙默认唯一开启的服务

### SSH基本信息






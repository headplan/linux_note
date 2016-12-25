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

**网卡配置**

需要为安装了SSH服务的系统配置一个固定的IP

```
vim /etc/sysconfig/network-scripts/ifcfg-xxx
```

**软件包**

一般发行版的Linux的软件包都提供了openssh软件包,也可以向上网中提到的使用yum或apt-get等安装.

**进程名**

SSH服务器启动后,会自动启动名为sshd的进程.查看:

```
ps -eaf | grep sshd
```

**端口号**

SSH服务运行后,默认监听TCP协议上的22端口号.查看:

```
netstat -antpul | grep sshd
```

**防火墙开放的端口号**

```
# 添加开放端口22
iptables -I INPUT -p tcp --dport 22 -j ACCEPT
```

### SSH运行机制

**SSH的组成**

SSH是由客户端和服务端的软件组成.有两个不兼容的版本1.x和2.x,安全和功能性上2.x被广泛使用.

* SSH服务端:是一个守护进程\(daemon\),它在后台运行并响应来自SSH客户端的连接请求.SSH服务端一般是sshd进程,提供了对远程连接的处理,一般包括公共密钥认证,密钥交换,对称密钥加密和非安全连接.
* SSH客户端:包含ssh程序以及类似scp\(远程复制\),slogin\(远程登录\),sftp\(安全文件传输\)等其他的应用程序.

**SSH的安全验证**

的


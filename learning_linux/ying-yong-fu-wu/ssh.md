# SSH

> 基本配置参考php\_note中部署章节笔记

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

* 基于密码的安全验证,用户需要通过账号和密码登录到远程主机,并且所有传输的数据都是加密的.但是可能会有其他服务器冒充正真的服务器,无法避免被"中间人"攻击.
* 基于密钥的安全验证,需要依靠密钥,也就是必须为自己创建一对密钥,并把公有密钥放在需要访问的服务器上.当客户端软件向服务器发出使用的密钥进行安全验证请求后,服务器收到请求,会先在该服务器的用户根目录下寻找公有密钥,然后把它和发送过来的公有密钥进行比较.如果两个密钥一致,服务器就用公有密钥加密"质询"并把它发送给客户端软件,从而避免被"中间人"攻击.

**SSH为服务端也提供安全验证**

* 第一种方案中,主机将自己的公用密钥分发给相关的客户端,客户机在访问主机时需要使用该主机的公开密钥加密数据,而主机则使用自己的私有密钥解密数据,实现主机密钥认证,确定客户端的可靠身份.
* 第二种方案中,存在一个密钥认证中心,所有提供服务的主机都将自己公开密钥交给认证中心,任何作为客户端的主机则只要保存一份认证中心的公开密钥就可以了.客户端必须先访问认证中心,然后才能访问服务器主机.

### SSH文件组成

* /etc/pam.d
  * sshd - 配置文件:PAM认证文件
  * ssh-keycat - 配置文件:PAM认证文件
* /etc/rc.d/init.d
  * sshd - 脚本文件:控制SSH服务的运行
* /etc/ssh/
  * sshd\_config - 配置文件:SSH服务的主配置文件
  * ssh\_config - 配置文件:SSH客户端配置文件
  * moduli - 配置文件:配置密钥组
  * ssh\_host\_rsa\_key - 配置文件:RSA私钥
  * ssh\_host\_rsa\_key.pub - 配置文件:RSA公钥
  * ssh\_host\_ecdsa\_key - 配置文件:ECDSA私钥
  * ssh\_host\_ecdsa\_key.pub - 配置文件:ECDSA公钥
  * ssh\_host\_ed25519\_key - 配置文件:ED25519私钥
  * ssh\_host\_ed25519\_key.pub - 配置文件:ED25519公钥
* /etc/sysconfig
  * sshd - 配置文件:SSH命令配置参数
* /usr/libexec/openssh
  * sftp-server - 可执行文件:SFTP服务子系统
  * ssh-keysign - 可执行文件:基于主机的认证ssh的辅助程序
  * ctr-cavstest
  * ssh-pkcs11-helper
* /usr/bin
  * ssh
  * ssh-add
  * ssh-agent
  * ssh-copy-id
  * ssh-keygen
  * ssh-keyscan
* /usr/sbin
  * sshd
  * sshd-keygen

### SSH配置文件

/etc/ssh/sshd\_config

```
############# 关于SSH Server的整体设置 ##############

# 设置SSH服务监听的端口,默认为22.建议设置为陌生的5位数端口
Port 22
# any表示监听IPv4和IPv6.如果设置为inet表示只监听IPv4,inet6表示仅监听IPv6
AddressFamily any
# 设置允许连接到SSH服务的主机.默认0.0.0.0监听所有主机
ListenAddress 0.0.0.0
# 设置使用SSH协议,如果使用两个协议之间用逗号分隔(2,1),默认协议SSH2,SSH1存在漏洞与缺陷
Protocol 2

############# Private Key相关的配置 ##############

# 设置私钥加密文件,使用rsa,ecdsa,ed25519加密算法生成的文件;
# HostKey是主机私钥文件的存放位置;
# SSH-1默认是/etc/ssh/ssh_host_key.SSH-2默认是/etc/ssh/ssh_host_rsa_key和/etc/ssh/ssh_host_dsa_key.
# 一台主机可以拥有多个不同的私钥."rsa1"仅用于SSH-1,"dsa"和"rsa"仅用于SSH-2.
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key
# 设置多少秒之后系统自动重新生成服务器的密钥
KeyRegenerationInterval 1h
# 定义服务器密钥长度
ServerKeyBits 1024
#

https://blog.csdn.net/xieyi2015/article/details/70990922
https://blog.csdn.net/field_yang/article/details/51568861
http://www.ruanyifeng.com/blog/2011/12/ssh_port_forwarding.html
http://blog.licess.com/sshd_config/
https://blog.csdn.net/zhu_xun/article/details/18304441
https://www.cnblogs.com/sysk/p/4825275.html
```




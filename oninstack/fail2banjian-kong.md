# fail2ban监控

fail2ban是由Python语言开发监控软件，通过监控系统日志的登录信息来调用iptables屏蔽相应登录IP，以阻止某个IP（fail2ban读对应日志文件，Debian/Ubuntu:/var/log/auth.log、CentOS/Redhat:/var/log/secure）不停尝试密码。fail2ban在防御对SSH服务器的暴力密码破解上非常有用。

#### 安装配置Fail2ban

使用OneinStack , 内置fail2ban , 一键安装并设置好即可 : 

```
./addons.sh  # 选择9安装fail2ban
```

#### Fail2ban配置文件说明

```
cat /etc/fail2ban/jail.local
[DEFAULT]
ignoreip = 127.0.0.1/8 # 指定哪些地址可以忽略 fail2ban 防御
bantime  = 86400       # 客户端主机被禁止的时长(秒)
findtime = 600         # 查找失败次数的时长(秒)
maxretry = 5           # 客户端主机被禁止前允许失败的次数
[ssh-iptables]
enabled = true
filter  = sshd
action  = iptables[name=SSH, port=22, protocol=tcp]
logpath = /var/log/secure
```

fail2ban会自动禁止在最近10分钟内有超过5次访问尝试失败的任意IP地址 . 这个IP地址将会在24小时内一直被禁止访问SSH服务 . 安装设置启用后 , Fail2ban会在iptables添加相关规则 . 查看 : 

```
iptables -nvL
```

#### fail2ban测试

ssh 你的服务器IP , 输错密码5次以上 , 查看日志/var/log/fail2ban.log

#### fail2ban状态

```
/usr/local/python/bin/fail2ban-client status ssh-iptables
```

显示出被禁止IP地址列表

#### fail2ban解锁IP

为了解锁特定的IP地址命令

```
/usr/local/python/bin/fail2ban-client set ssh-iptables unbanip 192.168.123.123
```




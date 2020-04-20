# SSH相关问题

#### **ssh连接主机时出现如下报错**

> ssh\_exchange\_identification: read: Connection reset by peer

```
[root@headplan ~]# ssh root@192.168.1.101
ssh_exchange_identification: read: Connection reset by peer
```

```
# -v表示查看连接详细信息
[root@headplan ~]# ssh -v root@192.168.1.101
```

在服务端更改配置文件

```
vim /etc/hosts.allow
systemctl restart sshd
```






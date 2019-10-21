# Kali开启SSH服务

配置SSH参数 , 修改sshd\_config文件

```
vi /etc/ssh/sshd_config
```

将\#PasswordAuthentication no的注释去掉 , 并且将NO修改为YES //kali中默认是yes

将PermitRootLogin without-password修改为PermitRootLogin yes

保存

**启动SSH服务**

```
/etc/init.d/ssh start
或
service ssh start
```

查看SSH服务状态是否正常运行

```
/etc/init.d/ssh status
或
service ssh status
```

使用SSH客户端登录Kali

> 如何还是不行 , 可能要先生成两个密钥：
>
> \#ssh-keygen -t dsa -f /etc/ssh/ssh\_host\_dsa\_key
>
> \#ssh-keygen -t dsa -f /etc/ssh/ssh\_host\_rsa\_key

执行命令后都会让输入密码，直接敲回车设置为空即可

设置系统自动启动SSH服务

```
systemctl enable ssh.service
```




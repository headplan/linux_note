# CentOS7简单初始化

登录服务器

```
local$ ssh root@SERVER_IP_ADDRESS
```

创建新用户

```
# adduser demo
# passwd demo
输入密码
```

添加用户到wheel组 , 使其有sudu权限

```
# gpasswd -a demo wheel
```

添加公钥验证身份

```
local$ 
```

参考资料

https://www.digitalocean.com/community/tutorials/how-to-connect-to-your-droplet-with-ssh

https://www.digitalocean.com/community/tutorials/initial-server-setup-with-centos-7


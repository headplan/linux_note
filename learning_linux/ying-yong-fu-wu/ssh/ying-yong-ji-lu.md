# 应用记录

#### SSH错误

REMOTE HOST IDENTIFICATION HAS CHANGED 问题解决

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
da:f7:3e:ba:f7:00:e6:44:76:f2:58:6e:48:**.
Please contact your system administrator.
Add correct host key in /用户home目录/.ssh/known_hosts to get rid of this message.
Offending RSA key in /用户home目录/.ssh/known_hosts:1
RSA host key for ip地址 has changed and you have requested strict checking.
Host key verification failed.
```

**先查看**

```
ssh-keygen -l -f ~/.ssh/known_hosts
```

由于服务器重新安装系统了,所以会出现以上错误.

解决办法

```
ssh-keygen -R 服务器端的ip地址
```

之后重连即可.




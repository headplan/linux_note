# scp

> 应用场景 : 当各种离线 , 下载方式让人抓狂时使用 . 搬瓦工-&gt;阿里云 .

**传输文件**

```
scp /tmp/test.tar root@192.168.1.110:/home/myhome
```

**下载文件**

```
scp root@192.168.1.110:/home/myhome /tmp/test.tar
```

**递归目录**

```
scp -r root@192.168.1.190:/home/mydir /tmp
```

**断点续传**

```
rsync -P --rsh='ssh -p 520521' /data/sexy.sql root@192.168.6.25:/root/mydata/
```

**保持会话**

```
# 新建
screen -S myjobsname
# 恢复
screen -r myjobsname
```




# Linux下查看进程打开的文件句柄数

查看系统默认的最大文件句柄数 , 系统默认是1024

```
# ulimit -n
1024
```

查看当前进程打开了多少句柄数

```
# lsof -n | awk '{print $2}' | sort | uniq -c | sort -nr | more

131 24204
57 24244
57 24231
```

其中第一列是打开的句柄数 , 第二列是进程ID .

可以根据ID号来查看进程名 .

```
# ps -ef | grep 24204
nginx　　24204 24162 99 16:15 ?　　　　00:24:25 /usr/local/nginx/sbin/nginx -s
```

Linux有硬性限制和软性限制 . 可以通过ulimit来设定这两个参数 : 

```
# ulimit -HSn 4096
```

* H指定了硬性大小 ;
* S指定了软性大小 ; 
* n表示设定单个进程最大的打开文件句柄数量 .

设定句柄数量后 , 系统重启后又会恢复默认值 . 

如果想永久保存下来 , 可以修改.bash\_profile文件 , 可以修改 /etc/profile 把上面命令加到最后 . 或者直接修改配置文件 : 

```
/etc/security/limits.conf
```

配置文件 . 


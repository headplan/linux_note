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




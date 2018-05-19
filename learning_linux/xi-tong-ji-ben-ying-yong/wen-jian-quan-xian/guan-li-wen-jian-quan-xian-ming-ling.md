# 管理文件权限命令

#### **chmod**

#### chmod : 修改文件权限位命令

chmod - change file mode bits

表达格式 :

```
chmod [OPTION]... MODE[,MODE]... FILE...
chmod [OPTION]... OCTAL-MODE FILE...
chmod [OPTION]... --reference=RFILE FILE...
```

常用选项 : -R 递归 , 将设置的权限应用到下面的所有文件 .

**赋权表示法** : u=属主  g=属组  o=其他  a=所有

直接操作一类用户的所有权限位 rwx

写法：u=rwx

```
chmod u=rwx,g=rwx cat1
```

**授权表示法 : **直接操作一类用户的一个权限为r,w,x

写法 : u+\(r\|w\|x\) u-\(r\|w\|x\) g+\(r\|w\|x\) g-\(r\|w\|x\) o+\(r\|w\|x\) o-\(r\|w\|x\) a+\(r\|w\|x\) a-\(r\|w\|x\)

```
chmod u+x,g+w cat2
```

还有就是我们常用的数字写法 :

```
chmod 755 cat3
```

还有前面提的修改setuid等权限

```
chmod u+s prog1
chmod 4xxx prog1

chmod g+s dir1
chmod 2xxx dir1

chmod t dir1
chmod 1xxx dir1
```

#### **chown**

chown - change file owner and group

表达格式：

```
chown [OPTION]... [OWNER][:[GROUP]] FILE...
chown [OPTION]... --reference=RFILE FILE...
```

常用选项 : -R 递归修改

```
chown headplan:root cat1
```




# 文件权限

```
# 查看文件权限
ls -l 文件名
```

![](/assets/wenjianquanxian.png)

三种用户角色 :

* user : 文件的所有者
* group : 所属的用户组
* others : 其他人

每个文件或目录有三种基本权限类型 :

* r : 读权限    
* w : 写权限    
* x : 执行权限

**文件中**rwx的具体含义：

```
  r : 可以使用类似cat等命令查看文件内容

  w : 可以编辑或删除此文件

  x : 可以在命令提示符下当做命令提交给内核运行
```

**目录中**rwx的具体含义：

```
  r : 可以对此目录执行ls以列出内部的所有文件

  w : 可以在此目录创建文件

  x : 可以使用cd切换进此目录，也可以使用ls -l查看内部文件的详细信息
```

![](/assets/qianxianleixing.png)

数字的对应关系 :

* 000`---`对应十进制0
* 001`--x`对应十进制1
* 010`-w-`对应十进制2
* 011`-wx` 对应十进制3
* 100`r--`对应十进制4
* 101`r-x`对应十进制5
* 110`rw-`对应十进制6
* 111`rwx`对应十进制7

![](/assets/quanxianleixing2.png)

权限对应数字关系 :

```
-rw-------    (600) 只有所有者才有读和写的权限  
-rw-r--r--    (644) 只有所有者才有读和写的权限，组群和其他人只有读的权限  
-rwx------    (700) 只有所有者才有读，写，执行的权限  
-rwxr-xr-x    (755) 只有所有者才有读，写，执行的权限，组群和其他人只有读和执行的权限  
-rwx--x--x    (711) 只有所有者才有读，写，执行的权限，组群和其他人只有执行的权限  
-rw-rw-rw-    (666) 每个人都有读写的权限  
-rwxrwxrwx    (777) 每个人都有读写和执行的权限
```

### linux中一些特殊的权限\(setuid/setgid/sticky\)

#### setuid

其中之一就是setuid位 , 八进制表示为4000 , 当把它应用到一个可执行文件时 , 有效用户ID将从实际用户ID（实际运行该程序的用户）设置成该程序所有者的ID，大多数情况下，该权限设置通常应用于一些由超级用户所拥有的程序，例如sudo。当普通用户运行一个具有“setuid root”（已设置setuid位，由root用户所有）属性的程序时，该程序将以超级用户的权限执行。

**可以理解为 : 让普通用户可以以root用户的角色运行只有root帐号才能运行的程序或命令 . **

#### setgid

第二个是setgid位 , 八进制表示为2000，类似于setuid，它会把有效用户组ID从该用户的实际组ID更改为该文件所有者的组ID。如果对一个目录设置setgid位，那么在该目录下创建的文件将由该目录所在组所有，而不属于文件创建者所在组。**当一个公共组下的成员需要访问共享目录下的所有文件时，设置setgid位将会很有用，并不需要关注文件所有者所在的用户组。设置后 , 任何用户在此目录下创建的文件都具有和该目录所属的组相同的组 . **

#### sticky

第三个是sticky位，八进制表示位1000，它是从UNIX中继承下来的，在LINUX中将会忽略文件的sticky位。但是对一个目录设置sticky位，那么将能**阻止用户删除或者重命名文件，除非用户是这个目录的所有者、文件所有者或者超级用户。它通常用来控制对共享目录（例如/tmp）的访问。设置该位后, 就算用户对目录具有写权限, 也不能删除该文件**

#### 特殊权限的设置

**授予setuid权限**

```
chmod u+s prog1
chmod 4xxx prog1
```

具有setuid属性的程序为`-rwsr-xr-x`。

**授予setgid权限**

```
chmod g+s dir1
chmod 2xxx dir1
```

具有setgid属性的目录为`drwxrwsr-x`。

**授予sticky权限**

```
chmod t dir1
chmod 1xxx dir1
```

具有sticky属性的目录为`drwxrwxrwt`。

---

#### 带着问题去看 , 为什么普通用户可以执行passwd , 修改/etc/passwd ? 

```
-rw-r--r-- 1 root root 1787 Oct 27  2018 /etc/passwd
-r-------- 1 root root 1187 Oct 27  2018 /etc/shadow
```

/etc/passwd文件每个用户都有读权限但是只有root有写权限 , /etc/shadow文件只有超级用户root有读写权限 , 也就是说普通用户对这两个文件都没有写权限无法写入新密码 , 为什么普通用户可以更改密码呢 ? 

其实 , 用户能更改密码真正的秘密不在于文件的权限 , 而在于更改密码的命令passwd : 

```
-rwsr-xr-x 1 root root 22960 Jul 17 2018 /usr/bin/passwd
```

可以看到s标记 , 也就是setuid权限 . 

在来几个例子 , 普通用户headplan使用touch命令创建一个文件 : 

```
touch myfile
ls -l myfile
-rw-rw-r-- 1 headplan headplan 0 05-21 01:20 myfile
```

使用root给touch命令添加SetUID权限 : 

```
chmod u+s /bin/touch   
# chmod 4755 /bin/touch

ls -l /bin/touch
-rwsr-xr-x 1 root root 42284 Jul 13  2018 /bin/touch
```

现在 , 再用普通用户headplan创建文件 : 

```
touch myfile1
ls -l myfile1
-rw-rw-r-- 1 root headplan 0 05-21 01:48 myfile1
```

当一个可执行文件\(命令touch\)设置SetUID权限后 , 当普通用户headplan执行touch创建新文件时 , 实际上是以touch命令所有者root的身份在执行此操作 , 既然是以root身份执行 , 当然新建文件的所有者为root , 这就是SetUID的作用 . 




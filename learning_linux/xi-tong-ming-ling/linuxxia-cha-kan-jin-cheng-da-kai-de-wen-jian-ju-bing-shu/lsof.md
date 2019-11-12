# lsof

**lsof命令**用于查看你进程开打的文件 , 打开文件的进程 , 进程打开的端口\(TCP、UDP\) . 找回/恢复删除的文件 . 是十分方便的系统监视工具 , 因为lsof命令需要访问核心内存和各种文件 , 所以需要root用户执行 .

在Linux环境下 , 任何事物都以文件的形式存在 , 通过文件不仅仅可以访问常规数据 , 还可以访问网络连接和硬件 . 所以如传输控制协议 \(TCP\) 和用户数据报协议 \(UDP\) 套接字等 , 系统在后台都为该应用程序分配了一个文件描述符 , 无论这个文件的本质如何 , 该文件描述符为应用程序与基础操作系统之间的交互提供了通用接口 . 因为应用程序打开文件的描述符列表提供了大量关于这个应用程序本身的信息 , 因此通过lsof工具能够查看这个列表对系统监测以及排错将是很有帮助的 .

#### 语法

```
lsof(选项)
```

#### 选项

```
-a:列出打开文件存在的进程
-c<进程名>:列出指定进程所打开的文件
-g:列出GID号进程详情
-d<文件号>:列出占用该文件号的进程
+d<目录>:列出目录下被打开的文件
+D<目录>:递归列出目录下被打开的文件
-n<目录>:列出使用NFS的文件
-i<条件>:列出符合条件的进程(4/6/协议/:端口/@ip)
-p<进程号>:列出指定进程号所打开的文件
-u:列出UID号进程详情
-h:显示帮助信息
-v:显示版本信息
```

#### lsof 输出各列信息的意义如下

```
COMMAND     PID    USER   FD      TYPE     DEVICE      SIZE       NODE NAME 
 init        1     root   cwd     DIR       3,2        4096          2 / 
 init        1     root   rtd     DIR       3,2        4096          2 / 
 init        1     root   txt     REG       3,2       32684    1200637 /sbin/init
```

**COMMAND** : 进程的名称

**PID** : 进程标识符

**USER** : 进程所有者

**FD** : 文件描述符 , 应用程序通过文件描述符识别该文件 , 如 cwd、txt 等 .

**TYPE** : 文件类型，如 DIR、REG 等

**DEVICE** : 指定磁盘的名称

**SIZE** : 文件的大小

**NODE** : 索引节点\(文件在磁盘上的标识\)

**NAME** : 打开文件的确切名称

#### 文件描述符列表

1. cwd : 表示current work dirctory , 即 : 应用程序的当前工作目录 , 这是该应用程序启动的目录 , 除非它本身对这个目录进行更改
2. txt : 该类型的文件是程序代码 , 如应用程序二进制文件本身或共享库 , 如上列表中显示的 /sbin/init 程序
3. lnn : library references \(AIX\)
4. er : FD information error \(see NAME column\)
5. jld : jail directory \(FreeBSD\)
6. ltx : shared library text \(code and data\)
7. mxx : hex memory-mapped type number xx
8. m86 : DOS Merge mapped file
9. mem : memory-mapped file
10. mmap : memory-mapped device
11. pd : parent directory
12. rtd : root directory
13. tr : kernel trace file\(OpenBSD\)
14. v86  VP/ix mapped file
15. 0 : 表示标准输出
16. 1 : 表示标准输入
17. 2 : 表示标准错误

#### 一般在标准输出、标准错误、标准输入后还跟着文件状态模式

1. u : 表示该文件被打开并处于读取/写入模式
2. r : 表示该文件被打开并处于只读模式
3. w : 表示该文件被打开并处于
4. 空格 : 表示该文件的状态模式为unknow , 且没有锁定
5. `-`表示该文件的状态模式为unknow , 且被锁定

#### 同时在文件状态模式后面 , 还跟着相关的锁

1. N : for a Solaris NFS lock of unknown type
2. r : for read lock on part of the file
3. R：for a read lock on the entire file
4. w : for a write lock on part of the file \(文件的部分写锁\)
5. W : for a write lock on the entire file \(整个文件的写锁\)
6. u : for a read and write lock of any length
7. U : for a lock of unknown type
8. x : for an SCO OpenServer Xenix lock on part of the file
9. X : for an SCO OpenServer Xenix lock on the entire file
10. space : if there is no lock

#### 文件类型

1. DIR : 表示目录
2. CHR : 表示字符类型
3. BLK : 块设备类型
4. UNIX : UNIX 域套接字
5. FIFO : 先进先出\(FIFO\)队列
6. IPv4 : 网际协议 \(IP\) 套接字
7. DEVICE : 指定磁盘的名称
8. SIZE : 文件的大小
9. NODE : 索引节点\(文件在磁盘上的标识\)
10. NAME : 打开文件的确切名称

---

### 实际应用

#### **关键选项**

```
默认:没有选项,lsof列出活跃进程的所有打开文件
组合:可以将选项组合到一起,如-abc,但要当心哪些选项需要参数
-a:结果进行"与"运算(而不是"或")
-l:在输出显示用户ID而不是用户名
-h:获得帮助
-t:仅获取进程ID
-U:获取UNIX套接口地址
-F:格式化输出结果,用于其它命令.可以通过多种方式格式化,如-F pcfn(用于进程id、命令名、文件描述符、文件名，并以空终止)
```

#### 获取网络信息

```
lsof -i[46] [protocol][@hostname|hostaddr][:service|port]
```

**使用`-i`显示所有连接**

```
# lsof -i
```

**使用-i 6仅获取IPv6流量**

```
# lsof -i 6
```

**仅显示TCP连接\(同理可获得UDP连接\)**

```
# lsof -iTCP
```

**使用-i:port来显示与指定端口相关的网络信息**

```
# lsof -i :80
```

**使用@host来显示指定到指定主机的连接**

```
# lsof -i@127.0.0.1
```

**使用@host:port显示基于主机与端口的连接**

```
# lsof -i@127.0.0.1:80
```

**找出正等候连接的端口**

```
# lsof -i -sTCP:LISTEN
```

也可以grep "LISTEN"来完成该任务

```
# lsof -i | grep -i LISTEN
```

**找出已建立的连接**

```
# lsof -i -sTCP:ESTABLISHED
```

也可以通过grep搜索"ESTABLISHED"来完成该任务

```
# lsof -i | grep -i ESTABLISHED
```

#### 获取用户信息

**使用-u显示指定用户打开了什么**

```
# lsof -u www
```

**使用-u ^user来显示除指定用户以外的其它所有用户所做的事**

```
# lsof -u ^www
```

**杀死指定用户所做的一切事**

可以消灭指定用户运行的所有东西 . 

```
# kill -9 'lsof -t -u xiaoming'
```

#### 命令和进程



#### 文件和目录




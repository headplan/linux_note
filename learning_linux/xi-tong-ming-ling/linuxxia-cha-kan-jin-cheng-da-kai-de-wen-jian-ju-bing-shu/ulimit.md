# ulimit

**ulimit命令**用来限制系统用户对shell资源的访问 .

假设有这样一种情况 , 当一台 Linux 主机上同时登陆了 10 个人 , 在系统资源无限制的情况下 , 这 10 个用户同时打开了 500 个文档 , 而假设每个文档的大小有 10M , 这时系统的内存资源就会受到巨大的挑战 .

而实际应用的环境要比这种假设复杂的多 . 例如 , 在一个嵌入式开发环境中 , 各方面的资源都是非常紧缺的 , 对于开启文件描述符的数量 , 分配堆栈的大小 , CPU 时间 , 虚拟内存大小 , 等等 , 都有非常严格的要求 . 资源的合理限制和分配 , 不仅仅是保证系统可用性的必要条件 , 也与系统上软件运行的性能有着密不可分的联系 . 这时 , ulimit可以起到很大的作用 , 它是一种简单并且有效的实现资源限制的方式 .

ulimit 用于限制 shell 启动进程所占用的资源 , 支持以下各种类型的限制 : 所创建的内核文件的大小、进程数据块的大小、Shell 进程创建文件的大小、内存锁住的大小、常驻内存集的大小、打开文件描述符的数量、分配堆栈的最大大小、CPU 时间、单个用户的最大线程数、Shell 进程所能使用的最大虚拟内存 . 同时 , 它支持硬资源和软资源的限制 .

作为临时限制 , ulimit 可以作用于通过使用其命令登录的 shell 会话 , 在会话终止时便结束限制 , 并不影响于其他 shell 会话 . 而对于长期的固定限制 , ulimit 命令语句又可以被添加到由登录 shell 读取的文件中 , 作用于特定的 shell 用户 .

#### 语法

```
ulimit(选项)
```

#### 选项

```
-a：显示目前资源限制的设定；
-c <core文件上限>：设定core文件的最大值，单位为区块；
-d <数据节区大小>：程序数据节区的最大值，单位为KB；
-f <文件大小>：shell所能建立的最大文件，单位为区块；
-H：设定资源的硬性限制，也就是管理员所设下的限制；
-m <内存大小>：指定可使用内存的上限，单位为KB；
-n <文件数目>：指定同一时间最多可开启的文件数；
-p <缓冲区大小>：指定管道缓冲区的大小，单位512字节；
-s <堆叠大小>：指定堆叠的上限，单位为KB；
-S：设定资源的弹性限制；
-t <CPU时间>：指定CPU使用时间的上限，单位为秒；
-u <程序数目>：用户最多可开启的程序数目；
-v <虚拟内存大小>：指定可使用的虚拟内存上限，单位为KB。
```

#### 实例

```
[root@localhost ~]# ulimit -a
core file size          (blocks, -c) 0           # core文件的最大值为100 blocks。
data seg size           (kbytes, -d) unlimited   # 进程的数据段可以任意大。
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited   # 文件可以任意大。
pending signals                 (-i) 98304       # 最多有98304个待处理的信号。
max locked memory       (kbytes, -l) 32          # 一个任务锁住的物理内存的最大值为32KB。
max memory size         (kbytes, -m) unlimited   # 一个任务的常驻物理内存的最大值。
open files                      (-n) 1024        # 一个任务最多可以同时打开1024的文件。
pipe size            (512 bytes, -p) 8           # 管道的最大空间为4096字节。
POSIX message queues     (bytes, -q) 819200      # POSIX的消息队列的最大值为819200字节。
real-time priority              (-r) 0
stack size              (kbytes, -s) 10240       # 进程的栈的最大值为10240字节。
cpu time               (seconds, -t) unlimited   # 进程使用的CPU时间。
max user processes              (-u) 98304       # 当前用户同时打开的进程（包括线程）的最大个数为98304。
virtual memory          (kbytes, -v) unlimited   # 没有限制进程的最大地址空间。
file locks                      (-x) unlimited   # 所能锁住的文件的最大个数没有限制。
```

在上述参数中 , 关注的比较多的是 :

**open files** - 一个进程可打开的最大文件数

**max user processes** - 系统允许创建的最大进程数量

可以使用 ulimit -u 4096 修改max user processes的值 , 但是只能在当前终端的这个session里面生效 , 重新登录后仍然是使用系统默认值 . 如果想永久保存下来 , 可以修改.bash\_profile文件 , 可以修改 /etc/profile 把上面命令加到最后 .

#### 用户进程的有效范围

ulimit 作为对资源使用限制的一种工作 , 是有其作用范围的 . ulimit 限制的是当前 shell 进程以及其派生的子进程 . 举例来说 , 如果用户同时运行了两个 shell 终端进程 , 只在其中一个环境中执行了 ulimit – s 100 , 则该 shell 进程里创建文件的大小收到相应的限制 , 而同时另一个shell终端包括其上运行的子程序都不会受其影响 .

**针对用户永久生效**

直接修改配置文件 :

```
/etc/security/limits.conf
```

该文件不仅能限制指定用户的资源使用 , 还能限制指定组的资源使用 .

格式如下 :

```
<domain> <type> <item> <value>
```

**domain : **设置需要被限制的用户名 , 组名前面加@和用户名区别 . 也可以用通配符\*来做所有用户的限制 . 例如 , `username|@groupname`

**type : **有soft , hard和 - , **soft**指的是当前系统生效的设置值 . **hard**表明系统中所能设定的最大值 . **soft**的最大值不能超过hard的值 . 用- 就表明同时设置了soft和hard的值 .

**item : **也就是resource .

* core - 限制内核文件的大小
* date - 最大数据大小
* fsize - 最大文件大小
* memlock - 最大锁定内存地址空间
* nofile - 打开文件的最大数目
* rss - 最大持久设置大小
* stack - 最大栈大小
* cpu - 以分钟为单位的最多 CPU 时间
* noproc - 进程的最大数目\(系统的最大进程数\)
* as - 地址空间限制
* maxlogins - 此用户允许登录的最大数目

**value** : 就是limit数值

**要使 limits.conf 文件配置生效 , 必须要确保 pam\_limits.so 文件被加入到启动文件中 . **

查看 /etc/pam.d/login 文件 :

```
session required /lib/security/pam_limits.so
```

例如 : 解除Linux系统的最大进程数和最大文件打开数限制

```
* soft noproc 65535
* hard noproc 65535
* soft nofile 65535
* hard nofile 65535
```

说明 : soft表示软限制 , hard表示硬限制 , nproc进程数 , nofile文件数 .

**需要注意的是 , **`/etc/security/limits.d`**下也有noproc最大进参数的限制 : **

```
/etc/security/limits.d/20-nproc.conf
```

**即**`/etc/security/limits.d/`**下的文件覆盖了**`/etc/security/limits.conf`**设置的值 . **

> 官方的解释 : [https://access.redhat.com/solutions/406663](https://access.redhat.com/solutions/406663**)

现在已经可以对进程和用户分别做资源限制了 , 看似已经足够了 , 其实不然 . 很多应用需要对整个系统的资源使用做一个总的限制 , 这时候需要修改`/proc`下的配置文件 . `/proc`目录下包含了很多系统当前状态的参数 , 例如`/proc/sys/kernel/pid_max`, `/proc/sys/net/ipv4/ip_local_port_range`等等 , 从文件的名字大致可以猜出所限制的资源种类 .

修改了前面的配置文件 , 重现登录shell , 用`ulimit -Hn`和`ulimit -Sn`确认修改已生效 .

> 淘宝雕梁说 :
>
> > 在[ ](http://www.linuxde.net/)Linux Kernel 2.6.25之前通过ulimit -n\(setrlimit\(RLIMIT\_NOFILE\)\)设置每个进程的最大打开文件句柄数不能超过NR\_OPEN \(1024\*1024\) , 也就是100多万\(除非重新编译内核\) , 而在Linux Kernel 2.6.25之后 , 内核导出了一个sys接口可以修改这个最大值\(`/proc/sys/fs/nr_open`\) . 具体的changelog[ ](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commit;h=9cfe015aa424b3c003baba3841a60dd9b5ad319b): [https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=9cfe015aa424b3c003baba3841a60dd9b5ad319b](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=9cfe015aa424b3c003baba3841a60dd9b5ad319b)

通过读取**`/proc/sys/fs/file-nr`**可以看到当前使用的文件描述符总数 . 另外 , 对于文件描述符的配置 , 需要注意以下几点 : 

* 所有进程打开的文件描述符数不能超过**`/proc/sys/fs/file-max`**
* 单个进程打开的文件描述符数不能超过user limit中nofile的soft limit
* nofile的soft limit不能超过其hard limit
* nofile的hard limit不能超过**`/proc/sys/fs/nr_open  `**




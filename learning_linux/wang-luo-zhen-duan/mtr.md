# MTR

MTR是一种简单的跨平台命令行网络诊断工具 , 它将常用的traceroute和ping , nslookup程序的功能组合到一个工具中 . 与traceroute类似 , mtr输出关于数据包从运行mtr的主机到用户指定的目标主机的路由信息​​ .

运行**mtr , **它将探测本地系统和指定的远程主机之间的网络连接 . 它首先建立主机之间的每个网络跳跃点\(网桥 , 路由器和网关等\)的地址 , 然后**ping**每个跳跃点\(发送一个序列**ICMP ECHO**请求\)以确定到每台机器的链路的质量 .

在此操作过程中 , 默认情况下 , **mtr**会输出有关每台机器的有用统计信息 - 实时更新 .

#### 安装

```
$ yum install mtr             # centos
$ sudo apt-get install mtr    # debian/ubuntu
$ brew install mtr            # macos
```

#### 相关参数

```bash
$ mtr -h  # 提供帮助命令
$ mtr -v  # 显示mtr的版本信息
$ mtr -r  # 已报告模式显示
$ mtr -s  # 用来指定ping数据包的大小
$ mtr --no-dns # 不对IP地址做域名解析
$ mtr -a  # 来设置发送数据包的IP地址 这个对一个主机由多个IP地址是有用的
$ mtr -i  # 使用这个参数来设置ICMP返回之间的要求默认是1秒
$ mtr -4  # IPv4
$ mtr -6  # IPv6
```

#### 显示描述

* 第一列Host : IP地址和域名 , 按n键可以切换IP和域名
* 第二列Loss% : 丢包率
* 第三列Snt : 设置每秒发送数据包的数量 , 默认值是10 可以通过参数-c来指定
* 第四列Last : 最近一次的PING值
* 第五列Avg : 是平均值 这个应该是发送ping包的平均时延
* 第六列Best : 是最好或者说时延最短的
* 第七列Wrst : 是最差或者说时延最常的
* 第八列StDev : 标准偏差

#### 使用示例

1.使用**mtr**的最简单的例子是提供远程机器的域名或IP地址作为参数 . 显示实时更新的**traceroute**报告 , 直到退出程序 .

```
$ mtr google.com
OR
$ mtr 216.58.223.78
```

2.可以使用`-n`标识强制mtr显示数字IP地址而不是主机名\(**通常为FQDN-完全限定的域名**\)

```
mtr -n google.com
```

3.mtr同时显示主机名称和数字IP号码 , 请使用`-b`标识

```
mtr -b google.com
```

4.将ping的数量限制为特定值并在ping之后退出mtr , 请使用`-c`标识 . 从Snt列中观察 , 一旦达到指定的ping次数 , 实时更新停止并且程序退出 . 

```
mtr -c 5 google.com
```

5.使用`-r`标识将其设置为报告模式 , 这是生成有关网络质量统计信息的有用选项 . 可以使用此选项和`-c`选项来指定ping的数量 . 由于统计信息被打印到标准输出 , 可以将它们重定向到一个文件以供日后分析 . 

```
mtr -r -c 5 google.com > mtr-report.log
```

`-w`标识启用广泛的报告模式以获得更清晰的输出

```
mtr -rw -c 5 google.com > mtr-report.log
```




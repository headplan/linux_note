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




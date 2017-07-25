# Kcptun加速方案

> 新版的ShadowsocksX-NG中已经添加了对Kcptun的支持 , 直接配置地址即可

## Kcptun介绍

Kcptun 是一个非常简单和快速的，基于 KCP 协议的 UDP 隧道，它可以将 TCP 流转换为 KCP+UDP 流。而 KCP 是一个快速可靠协议，能以比 TCP 浪费10%-20%的带宽的代价，换取平均延迟降低 30%-40%，且最大延迟降低三倍的传输效果。

Kcptun 是 KCP 协议的一个简单应用，可以用于任意 TCP 网络程序的传输承载，以提高网络流畅度，降低掉线情况。由于 Kcptun 使用 Go 语言编写，内存占用低（经测试，在64M内存服务器上稳定运行），而且适用于所有平台，甚至 Arm 平台。

Kcptun 工作示意图：![](/assets/kcptun.png)KCP 协议：[https://github.com/skywind3000/kcp](https://github.com/skywind3000/kcp)

Kcptun 项目地址：[https://github.com/xtaci/kcptun](https://github.com/xtaci/kcptun)

下载CPU对应版本 : https://github.com/xtaci/kcptun/releases

正在使用的搬瓦工系统为CentOS , 所以下载对应的[**kcptun-linux-amd64-20170525.tar.gz**](https://github.com/xtaci/kcptun/releases/download/v20170525/kcptun-linux-amd64-20170525.tar.gz) . 

下载的是预编译版 , 所以直接运行 , 配合参数即可 , 这里记录一下脚本以及参数 : 

解压之后有两个文件 : client\_linux\_amd64 和 server\_linux\_amd64 , 一个用于服务器 , 一个用于客户端 . 

**创建start.sh**

```
#!/bin/bash
cd /root/kcptun/
./server_linux_amd64 -c /root/kcptun/server-config.json > kcptun.log 2>&1 &
echo "Kcptun started."
```

这里的server\_linux\_amd64就是Kcptun服务器 , server-config.json是要加载的配置文件 , 会自动生成日志文件kcptun.log

**创建server-config.json**

```
{
    "listen": ":29900",
    "target": "127.0.0.1:8388",
    "key": "test",
    "crypt": "salsa20",
    "mode": "fast2",
    "mtu": 1350,
    "sndwnd": 1024,
    "rcvwnd": 1024,
    "datashard": 70,
    "parityshard": 30,
    "dscp": 46,
    "nocomp": false,
    "acknodelay": false,
    "nodelay": 0,
    "interval": 40,
    "resend": 0,
    "nc": 0,
    "sockbuf": 4194304,
    "keepalive": 10
}
```

* listen - Kcptun 的服务端监听端口 , 用于接收外部请求和发送数据 , 默认 29900
* target - 要加速的地址 , 这里设置的是本机Shadowsocks的端口
* key - Kcptun的验证密钥 , 服务端和本地必须一致才能通过验证 , 自定义
* crypt - KCPTun服务端与客户端通信时使用的加密方式
* mode - KCPTun服务端与客户端数据传输模式
  * 响应速度 - fast3 &gt; fast2 &gt; \[fast\] &gt; normal &gt; default
  * 有效载荷比 - default &gt; normal &gt; \[fast\] &gt; fast2 &gt; fast3
* mtu - 设置 udp 数据包的最大传输单位 \(默认: 1350\)
* sndwnd - 设置发送窗口大小 \(数据包个数\) \(默认值: 1024\)
* rcvwnd - 设置接收窗口大小 \(数据包个数\) \(默认值: 1024\)
* 更多查看 - ./server\_linux\_amd64 -h

**创建stop.sh**

    #!/bin/bash
    echo "Stopping Kcptun..."
    PID=`ps -ef | grep server_linux_amd64 | grep -v grep | awk '{print $2}'`
    if [ "" !=  "$PID" ]; then
      echo "killing $PID"
      kill -9 $PID
    fi
    echo "Kcptun stoped."

**创建 restart.sh**

```
#!/bin/bash
cd /root/kcptun/
sh stop.sh
echo "Restarting Kcptun..."
sh start.sh
```

sh /root/kcptun/start.sh 启动后 , 就会生成kcptun.log日志文件 . 

**添加开机启动**

**Centos**

```
chmod +x /etc/rc.d/rc.local;echo "sh /root/kcptun/start.sh" >> /etc/rc.d/rc.local
```

**Ubuntu/Debian**

```
chmod +x /etc/rc.local;echo "sh /root/kcptun/start.sh" >> /etc/rc.local
```




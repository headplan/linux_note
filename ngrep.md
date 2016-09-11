# ngrep命令

ngrep命令是grep命令的网络版,他力求更多的grep特征,用于搜寻指定的数据包.正由于安装ngrep需用到libpcap库,所以支持大量的操作系统和网络协议.能识别TCP、UDP和ICMP包,理解bpf的过滤机制.

### 安装

**ngrep**

下载地址:http:\/\/ngrep.sourceforge.net\/

**libpcap**

下载地址:http:\/\/www.tcpdump.org\/

先用yum install libpcap完全安装libpcap,注意有时候用libpcap安装包安装的不完整会影响ngrep的使用.

如果yum无法安装,也可以make安装

```
wget http://www.tcpdump.org/release/libpcap-1.3.0.tar.gz
tar -zxf libpcap-1.3.0.tar.gz
cd libpcap-1.3.0
./configure
make && make install
```

ngrep的安装就是`configure/make/make install`三部曲.

如果遇到please wipe out all unused pcap installations,可以添加一下选项:

> .\/configure --with-pcap-includes=\/usr\/local\/include\/pcap

输入ngrep来验证下安装是否成功.

### 语法

```
ngrep <-LhNXViwqpevxlDtTRM> <-IO pcap_dump> <-n num> <-d dev> <-A num>
<-s snaplen> <-S limitlen> <-w normal|byline|single|none> <-c cols>
<-P char> <-F file>
```

### 选项

| 选项 | 含义 |
| --- | --- |
| -e | 显示空数据包 |



### 实例


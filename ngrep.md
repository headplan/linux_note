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

> -e - 显示空数据包
> -i - 忽略大小写
> -v - 反转匹配
> 
> -R - don't do privilege revocation logic
> 
> -x - 以16进制格式显示 
> 
> -X - 以16进制格式匹配
> 
> -w - 整字匹配 -p ：不使用混杂模式 -l ：make stdout line buffered -D ：replay pcap\_dumps with their recorded time intervals -t ：在每个匹配的包之前显示时间戳 -T ：显示上一个匹配的数据包之间的时间间隔 -M ：仅进行单行匹配 -I ：从文件中读取数据进行匹配 -O ：将匹配的数据保存到文件 -n ：仅捕获指定数目的数据包进行查看 -A ：匹配到数据包后dump随后的指定数目的数据包 -s ：set the bpf caplen -S ：set the limitlen on matched packets -W ：设置显示格式byline将解析包中的换行符 -c ：强制显示列的宽度 -P ：set the non-printable display char to what is specified -F ：使用文件中定义的bpf\(Berkeley Packet Filter\) -N ：显示由IANA定义的子协议号 -d ：使用哪个网卡，可以用-L选项查询 -L ：查询网卡接口

### 实例


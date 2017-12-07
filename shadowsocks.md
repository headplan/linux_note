# Shadowsocks

##### 参考资料

[https://github.com/shadowsocks/ShadowsocksX-NG](https://github.com/shadowsocks/ShadowsocksX-NG) - 客户端下载

[https://teddysun.com/486.html](https://teddysun.com/486.html) - 服务器安装

安装

```
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

安装完成后提示

```
Congratulations, your_shadowsocks_version install completed!
Your Server IP        :your_server_ip
Your Server Port      :your_server_port
Your Password         :your_password
Your Encryption Method:aes-256-cfb

Welcome to visit:https://teddysun.com/486.html
Enjoy it!
```

卸载

若已安装多个版本,则卸载时也需多次运行\(每次卸载一种\)

使用root用户登录,运行以下命令:

```
./shadowsocks-all.sh uninstall
```

启动脚本

```
启动脚本后面的参数含义，从左至右依次为：启动，停止，重启，查看状态。

Shadowsocks-Python 版：
/etc/init.d/shadowsocks-python start | stop | restart | status

ShadowsocksR 版：
/etc/init.d/shadowsocks-r start | stop | restart | status

Shadowsocks-Go 版：
/etc/init.d/shadowsocks-go start | stop | restart | status

Shadowsocks-libev 版：
/etc/init.d/shadowsocks-libev start | stop | restart | status
```

各个版本配置

```
Shadowsocks-Python 版：
/etc/shadowsocks-python/config.json

ShadowsocksR 版：
/etc/shadowsocks-r/config.json

Shadowsocks-Go 版：
/etc/shadowsocks-go/config.json

Shadowsocks-libev 版：
/etc/shadowsocks-libev/config.json
```

---

### Shadowsockske客户端

#### ubuntu

ubuntu16.04以上版本直接安装 :

```
sudo apt install shadowsocks
```

**启动**

```
sslocal --help
```

这里用加载配置文件的方式 :

```
sslocal -c 配置文件
```

**配置文件**

```js
{
    "server":"11.22.33.44", # 服务端IP
    "server_port":12345,    # 服务端端口
    "local_port":1080,      # 本地端口,默认1080
    "password":"123456",    # 服务端设置的密码
    "timeout":"600",        # 超时设置
    "method":"aes-256-cfb"  # 加密方式
}
```

**GUI客户端**

使用图形界面 , Linux有QT版 : 

```
sudo apt install shadowsocks-qt
```

配置和上面的配置文件说明类似 , 不过和Mac中的略有不同 , 没有自带全局代理的功能 , 如果只是浏览器 , 可以安装一些插件代理 , 但是比较麻烦 , 这里还是使用全局代理的方式 : 

**安装GenPAC**

基于gfwlist的代理自动配置\(Proxy Auto-config\)文件生成工具 , 支持自定义规则 . 

```
sudo pip install genpac
pip install --upgrade genpac
```

调用在线gfwlist列表生成本地autoproxy.pac文件 : 

```
mkdir .sspac && cd .sspac
touch my-rules.txt
```

创建存储pac的文件夹 , 以及自定义规则文件 . 运行命令生成pac文件 : 

```
genpac --pac-proxy "SOCKS5 127.0.0.1:1080" --gfwlist-proxy="SOCKS5 127.0.0.1:1080" \
--output="~/.sspac/proxy.pac" \
--gfwlist-url="https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt" \
--user-rule-from="~/.sspac/my-rules.txt"
```

**设置全局代理**

配置Network Proxy

URL配置 : file:///home/{user}/.sspac/proxy.pac


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

}
```




# WebSocket + TLS

#### 准备操作

Godaddy域名 : [https://sg.godaddy.com/zh](https://sg.godaddy.com/zh)

其他域名 : [https://www.namesilo.com](https://www.namesilo.com/)

Just My Socks机场 : [https://justmysocks1.net/members/cart.php](https://justmysocks1.net/members/cart.php)

Cloudflare免费CDN : [https://www.**cloudflare**.com/](http://www.baidu.com/link?url=-kXyAJYvgMWiGooBatfD0Q1kNCzSRgwxuDpK2OX1fRwjq5G0SwtelYOhgsuaRoV2)

* 添加域名
* 选择free
* 添加A记录\(域名和IP地址\)
* 设置域名解析服务器
* 开启SSL/TLS\(默认开启 , 选择Full\)
* DNS暂时关闭\(Proxy status状态设置灰色\)

#### **下载证书**

确保Edge Certificates菜单中Universal Status状态需为Active .

在Origin Server菜单中点击Origin Certificates中的创建证书按钮Create Certificate .

默认配置即可 , 保存证书以及私钥 , 私钥保存好\(只出现一次\) .

#### 搭建Nginx服务

这里直接用Oneinstack安装Nginx , 直接创建新的站点 , HTTPS也一件部署好了 . 然后手动配置一个ws的location

> 这里整数可以用前面的 , 也可以直接用Oneinstack的脚本生成 .

```bash
location /ws {
    proxy_redirect off;
    proxy_pass http://127.0.0.1:12345;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $http_host;
}
```

重启服务 .

#### 安装配置v2ray

使用233的一键脚本 , 选择4 : WebSocket+TLS传输协议

V2Ray 端口 = 56597

输入之前配置解析好的域名 , 记得在Cloudflare的DNS设置成DNS only

然后选择已经配置了TLS

是否开启广告拦截\(会影响性能\) , N

是否配置 Shadowsocks , N

然后回车 , 开始安装 . 




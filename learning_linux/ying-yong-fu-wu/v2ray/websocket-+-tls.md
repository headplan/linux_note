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






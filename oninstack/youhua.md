# 环境优化

### **关于防火墙**

> 特别注意:云服务器所在的安全组端口是否开放

默认开通端口

* SSH:22
* Nginx:80,443
* FTP:21,20000:30000

```
# 允许8080端口
iptables -I INPUT 4 -p tcp -m state --state NEW -m tcp --dport 8080  -j ACCEPT
# 保存iptables规则
service iptables save
# 查看iptables规则
iptables -nvL
# 列出INPUT的所有的规则
iptables -nvL INPUT --line-numbers
# 删除指定的第4行规则
iptables -D INPUT 4
service iptables save
```

### 关于PHP缓存

默认情况下,为了减少PHP编译时间,提高性能,生产环境强烈开启Opcache.PHP5.5,5.6,7.0等环境默认加载了Opcache模块,但是这样会出现PHP代码更新后,需要2~3分钟后才能生效,在网站调试阶段可以关闭或者更新代码后刷新缓存.

* 关闭 - /usr/local/php/etc/php.ini  和 /usr/local/php/etc/php.d 目录中相关文件,重启php-fpm.
* 刷新 - [http://公网/ocp.php](http://公网/ocp.php)

### 关于PHP模块安装

**以安装IMAP扩展为例**

```
yum -y install krb5-devel libc-client libc-client-devel
ln -sv /usr/lib64/libc-client.so /usr/lib/libc-client.so
# 进入原始目录,找到PHP源代码包解压缩
cd /root/oneinstack/src/
tar -zxvf php-5.6.29.tar.gz
cd /root/oneinstack/src/php-5.6.29/ext/imap
/usr/local/php56/bin/phpize
./configure --with-php-config=/usr/local/php56/bin/php-config --with-imap=/usr/lib64 --with-imap-ssl --with-kerberos
make && make install
cd /usr/local/php56/etc/php.d
# 编辑配置文件
vi imap.ini
extension = /usr/local/php/lib/php/extensions/no-debug-non-zts-20121212/imap.so
# 重启
service nginx restart
```

**支持fileinfo扩展安装**

```
# 进入原始目录,找到PHP源代码包解压缩
cd /root/oneinstack/src/
tar -zxvf php-5.6.29.tar.gz
cd /root/oneinstack/src/php-5.6.29/ext/fileinfo
/usr/local/php56/bin/phpize
./configure --with-php-config=/usr/local/php56/bin/php-config
make && make install
cd /usr/local/php56/lib/php/extensions
ls #看到no-debug-non-zts-20131226类似文件夹
cd no-debug-zts-20131226
ls #查看有没有 fileinfo.so,如果有，证明编译成功
#加载fileinfo
echo 'extension = /usr/local/php/lib/php/extensions/no-debug-non-zts-20170718/fileinfo.so' > /usr/local/php/etc/php.d/ext-fileinfo.ini
```

### 关于PHP多版本共存

安装了OneinStack之后,需要先停止PHP之后再继续进行安装.

```
service php-fpm stop # 停止PHP
mv /etc/init.d/php-fpm{,_bk} # 修改PHP启动脚本文件名,之后安装会覆盖
```

PHP默认安装在/usr/local/php目录中,再次安装会提示PHP已经安装,因此需要修改配置文件修改安装目录.

```
# 修改/root/oneinstack/options.conf
php_install_dir=/usr/local/php56
```

再次执行./install.sh,选择对应版本,其余选择n,等待安装完成,重启.

**修改PHP配置文件**

```
service php-fpm stop #停止php5.6启动脚本
mv /etc/init.d/php-fpm /etc/init.d/php56-fpm  #重命名php56启动脚本
mv /etc/init.d/php-fpm_bk /etc/init.d/php-fpm  #恢复php启动脚本
```

**设置多个PHP版本开机自启动**

```
# CentOS:
chkconfig --add php-fpm
chkconfig --add php56-fpm
chkconfig php-fpm on
chkconfig php56-fpm on
# Ubuntu/Debian:
update-rc.d php-fpm defaults
update-rc.d php56-fpm defaults
```

**防止多个PHP版本监听sock冲突,修改php56的listen配置**

```
# /usr/local/php56/etc/php-fpm.conf
listen = /dev/shm/php56-cgi.sock
service php-fpm start   #启动php
service php56-fpm start #启动php5.6
ps -ef | grep php # 查看进程
```

**修改nginx虚拟主机配置文件**

使用脚本./vhost添加虚拟主机绑定域名,生成nginx.conf文件后需要修改

```
fastcgi_pass unix:/dev/shm/php-cgi.sock;
# 修改为
fastcgi_pass unix:/dev/shm/php56-cgi.sock;
service nginx reload # 重启nginx
```

### 关于Redis、Memcached

* Redis 默认端口:6379
* Memcached 默认端口:11211
* 默认监听地址:127.0.0.1

**更改监听端口**

Redis:

```
# 编辑配置文件
vim /usr/local/redis/etc/redis.conf
# 重启生效
service redis-server restart
```

Memcached:

```
# 编辑脚本启动文件
vi /etc/init.d/memcached
# 重启生效
service memcached restart
```




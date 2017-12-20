# SYNC

> [http://www.vriteam.com/sync](http://www.vriteam.com/sync)

安装了SYNC需要的两个扩展

```
# 安装svn的php扩展
wget http://pecl.php.net/get/svn-1.0.2.tgz
tar zxf svn-1.0.2.tgz
cd svn-1.0.2
phpize
./configure 
make install

# 添加配置文件
echo 'extension = /usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/svn.so' > /usr/local/php/etc/php.d/ext-svn.ini
# 重启服务
service nginx restart
service php-fpm restart

# 这里需要一个依赖,需要先安装
yum install libssh2-devel
# 安装ssh2的php扩展
wget http://pecl.php.net/get/ssh2-0.12.tgz
tar zxf ssh2-0.12.tgz
cd ssh2-0.12
phpize
./configure
make install

# 添加配置文件
echo 'extension = /usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/ssh2.so' > /usr/local/php/etc/php.d/ext-ssh2.ini
# 重启服务
service nginx restart
service php-fpm restart
```

**安装SYNC**

直接copy代码即可

修改代码中错误提示,关闭E\_DEPRECATED的提示

**添加服务器**

```
# 使用脚本直接添加
./vhost.sh
```




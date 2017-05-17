# OneinStack安装

### 安装步骤

**注意**:如果有单独数据盘,建议您先挂载数据盘,建议将网站内容、数据库放在数据盘中.可以使用下面的脚本:

```
wget http://mirrors.linuxeye.com/scripts/auto_fdisk.sh
chmod +x ./auto_fdisk.sh
./auto_fdisk.sh
```

**先安装几个软件**

```
yum -y install wget screen curl python        #for CentOS/Redhat
# apt-get -y install wget screen curl python  #for Debian/Ubuntu
```

**下载安装包**

```
wget http://aliyun-oss.linuxeye.com/oneinstack-full.tar.gz #阿里云用户下载 
wget http://mirrors.linuxeye.com/oneinstack-full.tar.gz    #包含源码，国内外均可下载 
wget http://mirrors.linuxeye.com/oneinstack.tar.gz         #不包含源码，建议仅国外主机下载
```

**解压安装**

    tar xzf oneinstack-full.tar.gz 
    cd oneinstack                  #如果需要修改目录(安装、数据存储、Nginx日志)，请修改options.conf文件 
    screen -S oneinstack           #如果网路出现中断，可以执行命令`screen -r oneinstack`重新连接安装窗口 
    ./install.sh                   #注：请勿sh install.sh或者bash install.sh这样执行

**接下来是脚本一键安装时的配置**

```
Please input SSH port(Default: 22):        # 更改SSH端口号,建议默认22,过程中出现Defaultk可直接回车
Do you want to install Web server? [y/n]:y # 是否安装Web服务器,就是Nginx,Apache,Tomcat
Please select Nginx server:
        1. Install Nginx
        2. Install Tengine
        3. Install OpenResty
        4. Do not install
Please input a number:(Default 1 press Enter)1
Please select Apache server:
        1. Install Apache-2.4
        2. Install Apache-2.2
        3. Do not install
Please input a number:(Default 3 press Enter) 3
Please select tomcat server:
        1. Install Tomcat-8
        2. Install Tomcat-7
        3. Install Tomcat-6
        4. Do not install
Please input a number:(Default 4 press Enter) 4
#这里有4种模式可自由组合
1.lnmp - 安装Nginx,不安装Apache,Tomcat.系统运行php-fpm进程
2.lamp - 不安装Nginx,Tomcat,只安装Apache,.无php-fpm进程,PHP以模块形式加载在Apache中
3.lnmpa - 安装Nginx,Apache,不安装Tomcat.该模式下,静态资源由Nginx处理,PHP由Apache处理,无php-fpm进程,PHP以模块形式加载在Apache中.
4.lnmt - 安装Nginx和Tomcat,不安装Apache.该模式下,静态资源由Nginx处理,JAVA由Tomcat处理,可安装PHP,支持多语言环境,同时运行PHP,JAVA.
PHP用户推荐1,JAVA用户推荐4
也就是134组合.

Do you want to install Database? [y/n]:y # 是否安装数据库
Please select a version of the Database:
         1. Install MySQL-5.7
         2. Install MySQL-5.6
         3. Install MySQL-5.5
         4. Install MariaDB-10.1
         5. Install MariaDB-10.0
         6. Install MariaDB-5.5
         7. Install Percona-5.7
         8. Install Percona-5.6
         9. Install Percona-5.5
        10. Install AliSQL-5.6
Please input a number:(Default 2 press Enter)2 # 选择数据库版本
Please input the root password of database:    # 设置数据库root密码
Please choose installation of the database:    # 数据库安装方式.1.二进制安装,2.源码编译,建议1
        1. Install database from binary package.
        2. Install database from source package.
Please input a number:(Default 1 press Enter) 1
Do you want to install PHP? [y/n]:y # 是否安装PHP
Please select a version of the PHP:
        1. Install php-5.3
        2. Install php-5.4
        3. Install php-5.5
        4. Install php-5.6
        5. Install php-7.0
        6. Install php-7.1
Please input a number:(Default 4 press Enter) 6 #这里选择了最新版的PHP7.1
Do you want to install opcode cache of the PHP? [y/n]:y #是否安装PHP代码缓存组件(官方建议y)
Please select a opcode cache of the PHP:        #建议安装Zend Opcache,官方建议.如果选择了1,则不会安装ZendGuardLoader
        1. Install Zend OPcache
        3. Install APCU
Please input a number:(Default 1 press Enter)1
Do you want to install ionCube? [y/n]:y #PHP源码加密组件,安装看看
Do you want to install ImageMagick or GraphicsMagick? [y/n]:y #PHP图片处理模块
Please select ImageMagick or GraphicsMagick:
        1. Install ImageMagick
        2. Install GraphicsMagick
Please input a number:(Default 1 press Enter)1 #选择1
Do you want to install Pure-FTPd? [y/n]:y      #是否安装PureFTPd
Do you want to install phpMyAdmin? [y/n]: y    #是否安装phpMyAdmin
Do you want to install redis? [y/n]: y         #是否安装Redis
Do you want to install memcached? [y/n]: y     #是否安装Memcached
Do you want to install HHVM? [y/n]:n           #是否安装HHVM
之后就开始安装了
```

安装完毕后,会提示重启,还有有一个基本的列表,同时可以访问难受也查看基本情况,这里内容在下面的笔记中记录.


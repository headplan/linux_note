# 安装

安装分为有网络安装和无网络安装 . 由于无网络安装环节需要在有网络的主机上进行依赖包下载 , 所以相对繁琐麻烦 , 如果本机没有网络 , 可以考虑使用squid代理来进行安装 , 下面介绍的是有网络安装 .

安装命令可以使用easy\_install supervisor或者 pip install supervisor 或者去pypi官网上下载最新版本进行解压安装 . 也可以使用yum或者apt , 但不保证是最新版本 .

**使用pip install安装**

```
pip install supervisor
```

根据系统Python的权限 , 可能需要成为root用户才能使用pip成功安装Supervisor .

**下载安装**

[https://pypi.org/project/supervisor/](https://pypi.org/project/supervisor/)

如果系统没有安装pip , 则需要下载Supervisor发行版并手动安装 .

可以从PyPi下载当前和以前的Supervisor版本 . 解压缩软件存档后 , 运行 :

```
python setup.py install
```

根据系统Python的权限 , 可能需要成为root用户才能成功调用安装命令 .

#### 创建配置文件

Supervisor相当强大 , 提供了很丰富的功能 , 不过我们可能只需要用到其中一小部分 . 安装完成之后 , 可以编写配置文件 , 来满足自己的需求 . 为了方便 , 把配置分成两部分 : supervisord\(supervisor是一个C/S模型的程序 , 这是server端 , 对应的有client端supervisorctl\)和应用程序\(即我们要管理的程序\) . 

首先来看 supervisord 的配置文件 . 安装完 supervisor 之后 , 可以运行`echo_supervisord_conf`命令输出默认的配置项 , 也可以重定向到一个配置文件里 : 

```
echo_supervisord_conf > /etc/supervisord.conf
```




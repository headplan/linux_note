# 安装

安装分为有网络安装和无网络安装 . 由于无网络安装环节需要在有网络的主机上进行依赖包下载 , 所以相对繁琐麻烦 , 如果本机没有网络 , 可以考虑使用squid代理来进行安装 , 下面介绍的是有网络安装 .

安装命令可以使用easy\_install supervisor或者 pip install supervisor 或者去pypi官网上下载最新版本进行解压安装 . 也可以使用yum或者apt , 但不保证是最新版本 .

**使用pip install安装**

```
pip install supervisor
```

根据系统Python的权限 , 可能需要成为root用户才能使用pip成功安装Supervisor . 

**下载安装**

如果系统没有安装pip , 则需要下载Supervisor发行版并手动安装 . 

可以从[PyPi](https://translate.googleusercontent.com/translate_c?depth=1&hl=zh-CN&rurl=translate.google.com&sl=en&sp=nmt4&tl=zh-CN&u=https://pypi.org/pypi/supervisor/&xid=25657,15700021,15700186,15700191,15700253,15700256,15700259&usg=ALkJrhg3uCOvHaVQSRPemOIq2UjHWN43iA)下载当前和以前的Supervisor版本 . 解压缩软件存档后 , 运行 : 

```
python setup.py install
```




# 常见问题

**静态文件**

使用Vagrant的**config.vm.synced\_folder "/Users/bob/Documents/code/", "/var/www/“**之后,在本地修改了一些文件,发现在浏览器刷新不会变,修改配置文件即可

\# Apache 配置添加: EnableSendfile off

\# Nginx 配置添加:sendfile off;

**共享目录权限问题**

修改配置文件即可,搜索到两个解决方案,一个是配置目录权限,一个是配置用户和用户组的权限,推荐后者.

config.vm.synced\_folder "wwwroot", "/home/wwwroot",create: true, owner:"www", group: "www"

1. 假设你用的是nginx，那么要确认你的配置文件里用户和组都是www，如下user www www;
2. 假设你用的是php-fpm，那么要确认你的php-fpm配置文件中用户和组都是www，如下
   listen.owner = www
   listen.group = www

config.vm.synced\_folder ".", "/var/www", :mount\_options =&gt; \["dmode=777", "fmode=666"\]

修改"."为自己的目录,然后vagrant up开启虚拟机,指定目录即可.

**无法启动的问题**

**机器配置偏低的配置**

如果机器本身cpu的1,但vagrant默认的配置是2,这样就无法启动虚拟机了,修改配置文件

config.vm.provider "virtualbox" do \|vb\|

 vb.customize \["modifyvm", :id, "--cpus", "1"\]

end

**启动时无响应**

这个是现在一般的虚拟机都会遇到的问题,主要是因为电脑没有开始vt虚拟技术.

开机进入BIOS,开启Security中的两项:

* Intel \(R\) Virtualization Technology \[Enable\]
* Intel \(R\) VT-d Feature \[Enable\]

错误码:E\_FAIL \(0x80004005\)

**Vagrant启动时Timeout**

报错:\[default: Error: Connection timeout. Retrying... \]

多数因为360等杀毒软件的晶核防护禁用了64位,关闭就可以了.

**VirtualBox没有32位选项也是这个原因：**  
 Intel-VT晶核防护引擎占用了CPU的虚拟化技术,将其关闭后重启系统,再打开,就可以建立64位虚拟机系统了.

**不能挂载共享文件夹**

原因为VitrualBox没有安装增强功能,VBoxGuestAdditions.

打开虚拟机直接在虚拟机中安装.

先点击设备,选择最后一项安装增强功能,然后在命令行输入:

```
sudo mount /dev/cdrom /media/cdrom
cd /media/cdrom/
sudo ./VBoxLinuxAddtions.run
```

参考

[https://segmentfault.com/a/1190000002436885](https://segmentfault.com/a/1190000002436885)

[https://segmentfault.com/q/1010000004621907/a-1020000004622731](https://segmentfault.com/q/1010000004621907/a-1020000004622731)

[http://blog.csdn.net/hel12he/article/details/51353539](http://blog.csdn.net/hel12he/article/details/51353539)




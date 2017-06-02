# Vagrant安装与使用

**相关资料:**

* [https://segmentfault.com/a/1190000000264347](https://segmentfault.com/a/1190000000264347)
* [http://rmingwang.com/vagrant-commands-and-config.html](http://rmingwang.com/vagrant-commands-and-config.html)

**安装VirtualBox:**

虚拟机还是得依靠VirtualBox来搭建,虽然Vagrant也支持VMware,但是收费.

**安装Vagrant并添加镜像:**

下载地址:[https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)根据提示一步步安装

安装好以后运行:

\# 添加Vagrant官方的box镜像,会从官网下载名为hashicorp/precise64的box

vagrant box add hashicorp/precise64

如果需要其他系统的镜像,可以在这下载:

[https://atlas.hashicorp.com/boxes/search](https://atlas.hashicorp.com/boxes/search)

> **提示:如果因为网络问题添加不了镜像,可以用工具先将这些box下载下来,然后按照”打包分发”部分进行添加.**
>
> [**https://github.com/chef/bento**](https://github.com/chef/bento)

**初始化开发环境:**

创建一个开发目录,例如 ~/dev,或使用已有目录,用镜像初始化当前目录的环境

cd ~/dev \# 切换目录

vagrant init hashicorp/precise64 \# 用hashicorp/precise64进行box初始化

vagrant up \# 启动环境

在终端可以看到启动过程,启动之后就可以用SSH登陆虚拟机了,之后在虚拟机里配置环境就可以了

vagrant ssh \# SSH 登陆

cd /vagrant 切换到开发目录,也就是宿主机上的’~/dev’目录,是对应关系.

**其他设置:**

Vagrant初始化成功后,会在目录中生成一个Vagrantfile的配置文件,可以修改这个配置文件进行一些个性化定制.

Vagrant默认是使用端口映射方式将虚拟机的端口映射本地从而实现类似http://localhost:80这种访问方式,这种方式比较麻烦,新开和修改端口的时候都得编辑.相比较而言,host-only模式显得方便多了.打开Vagrantfile,将下面这行的注释去掉（移除\#）并保存:

```
config.vm.network :private_network, ip: "192.168.33.10"
```

重启虚拟机,就可以用192.168.33.10访问这台机器了,可以把IP改成其他地址,只要不产生冲突即可.

**打包分发:**

配置好开发环境后,退出并关闭虚拟机.在终端里对开发环境进行打包:

```
 vagrant package
```

打包完成后会在当前目录生成一个package.box的文件,将这个文件传给其他用户,其他用户只要添加这个box并用其初始化自己的开发目录就能得到一个一模一样的开发环境了.

假设我们拿到的box存放路径是~/box/package.box,在终端里输入:

```
 vagrant box add haha ~/box/package.box # 添加package.box镜像并命名为hahaha
```

 cd ~/dev \#切换到项目目录

```
 vagrant init haha # 用haha镜像初始化
```

**集成预安装**

如果每次都修改了一点点内容,再打包分发给其他用户其实很麻烦.为此Vagrant还提供了更为便捷的预安装定制.打开Vagrantfile文件末尾处有下面被注释的代码:

```
config.vm.provision "shell", inline: <<-SHELL
 apt-get update
 apt-get install -y apache2
SHELL
```

这段代码就是让你在初次运行vagrant up后,虚拟机创建过程众自动运行的初始化命令.取消注释,把要预先安装的php/mysql/redis和配置之类的通通都写进去.初始化时这些程序都会根据你写好的方法安装并配置.

如果不是初次运行,同时又修改了这里的命令,想让系统再次运行这里的命令,可以使用

```
vagrant reload --provision
```

进行重载,所以把Vagrantfile共享给其他人,运行相同的命令即可.

还可以把要运行的命令单独写在一个文件里存放在相同的目录下,比如bootstrap.sh

```
#!/usr/bin/env bash

apt-get update
apt-get install -y apache2
if ! [ -L /var/www ]; then
	rm -rf /var/www
	ln -fs /vagrant /var/www
fi
然后在Vagrantfile里面添加这个配置
Vagrant.configure(“2”) do |config|
	config.vm.box = “hashicorp/precise64”
	…
	config.vm.provision “shell”, path: “bootstrap.sh” # 添加这行
end
```

这样效果就和直接写在Vagrantfile是一样的.

**注意事项**

使用Apache/Nginx时会出现诸如图片修改后但页面刷新仍然是旧文件的情况,是由于静态文件缓存造成的.需要对虚拟机里Apache/Nginx配置文件进行修改:

```
# Apache 配置添加:
EnableSendfile off
# Nginx 配置添加:
sendfile off;
```

**常用命令**

* $ vagrant init  \# 初始化
* $ vagrant up  \# 启动虚拟机
* $ vagrant halt  \# 关闭虚拟机
* $ vagrant reload  \# 重启虚拟机
* $ vagrant ssh  \# SSH 至虚拟机
* $ vagrant status  \# 查看虚拟机运行状态
* $ vagrant destroy  \# 销毁当前虚拟机

**Vagrant命令**

用法:vagrant \[options\] &lt;command&gt; \[&lt;args&gt;\]

参数:

* \* -v,—version - 查看版本并退出
* \* -h,—help - 查看帮助

命令:

* \* box - 管理box,安装和删除等等
* \* connect - 连接到远程共享的Vagrant环境
* \* destroy - 暂停并删除Vagrant虚拟机的所有痕迹
* \* global-status - 输出当前用户Vagrant环境的状态
* \* halt - 暂停Vagrant虚拟机
* \* help - 显示子命令的帮助
* \* init - 通过创建Vagrantfile来初始化一个新的Vagrant环境
* \* login - 登陆HashiCorp的Atlas
* \* package - 打包一个Vagrant运行环境到box
* \* plugin - 管理插件,安装,卸载,删除等
* \* port - 显示关于guest的端口映射信息
* \* powershell - 通过powershell远程连接到机器
* \* provision - provisions the vagrant machine
  \* push - deploys code in this environment to a configured destination
  \* rdp - connects to machine via RDP
  \* reload - restarts vagrant machine, loads new Vagrantfile configuration
  \* resume - resume a suspended vagrant machine
  \* share - share your Vagrant environment with anyone in the world
  \* snapshot - manages snapshots: saving, restoring, etc.
  \* ssh - connects to machine via SSH
  \* ssh-config - outputs OpenSSH valid configuration to connect to the machine
  \* status - outputs status of the vagrant machine
  \* suspend - suspends the machine
  \* up - starts and provisions the vagrant environment
  \* version - prints current and latest Vagrant version




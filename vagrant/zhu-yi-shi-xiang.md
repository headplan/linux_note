# Vagrant注意事项

**使用工具连接Vagrant中的数据库**

有的工具可以使用本地的秘钥直接通过设置ssh连接数据库,但Navicat就不可以.

一般会提示秘钥无法连接

使用命令查看vagrant的连接信息

vagrant ssh-config

可以找到vagrant的秘钥地址

/Users/headplan/.vagrant.d/boxes/centos\_v0.2/0/virtualbox/vagrant\_private\_key

秘钥使用这个地址,数据库连接地址使用localhost即可.

**静态文件缓存问题**

使用Apache/Nginx时会出现诸如图片修改后但页面刷新仍然是旧文件的情况,是由于静态文件缓存造成的.需要对虚拟机里的Apache/Nginx配置文件进行修改:

```
# Apache 配置添加:
EnableSendfile off
# Nginx 配置添加:
sendfile off;
```

**Vagrant内的站点访问速度慢**

NFS权限问题

```
config.vm.synced_folder '.', '/vagrant', :nfs =>{
    :linux__nfs_options => ["no_root_squash"],
    :map_uid => 0,
    :map_gid => 0
}
```

域名解析慢的问题

```
config.vm.provider :virtualbox do |vb|
    #vb.gui = true
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
end
```

**挂载失败的问题**

报错

```
Failed to mount folders in Linux guest. This is usually because the "vboxsf" file system is not available. 
Please verify that the guest additions are properly installed in the guest and can work properly. The command attempted was:
```

解决

```
//sudo apt-get install virtualbox-guest-dkms
sudo apt-get install virtualbox-guest-utils
```

报错

```
default: stdin: is not a tty
```

解决

```
vi /root/.profile
```

把mesg n替换成tty -s && mesg n

**Redis文件权限问题**

**报错**

redis Can't open the log file

redis无法加载.rdb

redis无法载入.rdb

**解决**

把 redis:redis 用户组设置更改为 vagrant:vagrant.

[http://serverfault.com/questions/541258/permissions-error-trying-to-dump-redis-to-a-vagrant-shared-folder](http://serverfault.com/questions/541258/permissions-error-trying-to-dump-redis-to-a-vagrant-shared-folder)

  


参考内容:

[http://rmingwang.com/vagrant-commands-and-config.html](http://rmingwang.com/vagrant-commands-and-config.html)


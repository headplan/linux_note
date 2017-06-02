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




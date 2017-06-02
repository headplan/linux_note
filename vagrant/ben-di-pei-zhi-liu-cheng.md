# 本地配置流程

```
# 添加box
vagrant box add centos ./box/vagrant-centos-7.2.box
# 初始化
vagrant init centos
# 编辑Vagrantfile配置文件
config.ssh.username = "vagrant"
config.ssh.password = "vagrant"
config.vm.network "private_network", ip: "192.168.33.11"
# config.vm.synced_folder "./wwwroot", "/home/wwwroot", create: true, owner:"www", group: "www"
# 启动box
vagrant up
# 基本信息
# 连接
vagrant ssh
vagrant:vagrant
root:vagrant
# 添加新用户
sudo adduser headplan
sudo passwd headplan
headplan:headplan
# 设置普通用户有roo权限
su # 切换到root
echo 'headplan ALL=(ALL) ALL' >> /etc/sudoers
tail -1 /etc/sudoers # 检查一下
```

```
vagrant halt # 关机
vagrant package # 打包
```

之后的部署参考阿里云服务器配置

参考资料 :

[http://seisman.info/linux-environment-for-seismology-research.html](http://seisman.info/linux-environment-for-seismology-research.html)


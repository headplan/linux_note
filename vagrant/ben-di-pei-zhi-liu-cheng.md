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
```

参考资料 :

[http://seisman.info/linux-environment-for-seismology-research.html](http://seisman.info/linux-environment-for-seismology-research.html)


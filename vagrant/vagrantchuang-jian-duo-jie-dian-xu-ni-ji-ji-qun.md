# Vagrant创建多节点虚拟机集群

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.ssh.username = "vagrant"
    config.ssh.password = "vagrant"
    (1..3).each do |i|
        config.vm.define "node#{i}" do |node|
        # 设置使用的盒子
        node.vm.box = "centos-init"
        # 设置虚拟机的主机名
        node.vm.hostname = "node#{i}"
        # 设置虚拟机的IP
        node.vm.network "private_network", ip:"192.168.33.#{i}"
        # 设置共享目录
        node.vm.synced_folder "./", "/home/headplan"
        # VirtaulBox相关配置
        node.vm.provider "virtualbox" do |v|
            # 设置虚拟机的名称
            v.name = "node#{i}"
            # 设置虚拟机的内存大小
            v.memory = "1024"
            # 设置虚拟机的CPU个数
            v.cpus = 1
        end
        # 使用Shell安装脚本
        # config.vm.provision "shell", inline: <<-SHELL
        #   apt-get update
        #   apt-get install -y apache2
        # SHELL
        end
    end
 end
```

Shell脚本部分还可以添加初始化时安装Docker

```
# 使用shell脚本进行软件安装和配置
node.vm.provision "shell", inline: <<-SHELL

    # 安装docker 1.11.0
    wget -qO- https://get.docker.com/ | sed 's/docker-engine/docker-engine=1.11.0-0~trusty/' | sh
    usermod -aG docker vagrant

SHELL
```

参考内容:

[http://kiwenlau.com/2016/07/03/vagrant-vm-cluster/](http://kiwenlau.com/2016/07/03/vagrant-vm-cluster/)


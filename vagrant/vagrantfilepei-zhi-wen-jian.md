# Vagrantfile配置文件

初始化后的目录会生成一个Vagrantfile,里面包含了大量的配置信息,主要包含三方面的配置:

* 虚拟机配置
* SSH配置
* Vagrant配置

常用配置:

* box设置 : config.vm.box = "centos7"
* hostname设置 : config.vm.hostname = "workstation"
* 虚拟机网络设置 : 
  * \#config.vm.network "private\_network", ip: "192.168.33.10"
    config.vm.network "public\_network"
* 同步目录 : config.vm.synced\_folder "../data", "/vagrant\_data"
* 端口转发 : config.vm.network "forwarded\_port", guest: 80, host: 8080
* 内存和CPU核心 : 
  * config.vm.provider "virtualbox" do \|vb\|
    \#Display the VirtualBox GUI when booting the machine
    vb.gui = true
    \#Customize the amount of memory on the VM:
    vb.memory = "1024"
    vb.cpus = 2
    vb.name = "my\_vm"
    end




# Vagrant简介

**相关资料:**

* \# 官方网站
  * [https://www.vagrantup.com/](https://www.vagrantup.com/)
* \# 搜索其他系统
  * [https://atlas.hashicorp.com/boxes/search](https://atlas.hashicorp.com/boxes/search)
* \# Box下载
  * [https://github.com/chef/bento](https://github.com/chef/bento)
* \# 一份配置
  * [https://github.com/fenbox/Vagrantfile](https://github.com/fenbox/Vagrantfile)
* \# 国内讨论组
  * [https://segmentfault.com/t/vagrant](https://segmentfault.com/t/vagrant)
* \# 一个打包好的Web基础环境镜像
  * [https://github.com/scotch-io/scotch-box](https://github.com/scotch-io/scotch-box)
* \# 图形化界面管理Vagrnt
  * [https://github.com/lanayotech/vagrant-manager](https://github.com/lanayotech/vagrant-manager)

Vagrant 是一个基于 Ruby 的工具,用于创建和部署虚拟化开发环境.它使用Oracle的开源VirtualBox虚拟化系统,使用Chef创建自动化虚拟环境.

**功能特性:**

* 支持快速新建虚拟机
* 支持快速设置端口转发
* 支持自定义镜像打包（原始镜像方式、增量补丁方式）
* 基本上日常能用到的基础配置都能快速设置
* 支持开机启动自动运行命令
* 可以自己写扩展

**做些什么:**

* 统一开发环境,一次配置打包,统一分发给团队成员,统一团队开发环境,解决诸如"编码问题”,"缺少模块”,"配置文件不同"带来的问题.
* 避免重复搭建开发环境.新员工加入,不用浪费时间搭建开发环境,快速加入开发,减少时间成本的浪费.
* 多个相互隔离开发环境.可以在不用box里跑不同的语言,或者编译安装同一语言不同版本,搭建多个相互隔离的开发环境,卸载清除时也很快捷轻松.

**安装方法:**

```
sudo gem install vagrant
vagrant box add base http://files.vagrantup.com/base.box
mkdir vagrant
vagrant init
vagrant up
```




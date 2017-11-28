# 脚本管理

**PHP脚本:/data/wwwroot/default**

* _phpinfo.php-&gt;修改为catinfo.php_

* _ocp.php-&gt;修改为catocp.php_

* _tz.php-&gt;修改为cattz.php_

* _phpMyAdmin/-&gt;修改为catMysql/_

**Shell脚本**

* ./reset\_db\_root\_password.sh - 修改数据库密码

* ./vhost.sh - 添加虚拟主机. \#如输入错误,请按Ctrl+删除键

* ./vhost.sh del - 删除虚拟主机

* ./upgrade.sh - 切换/升级软件小版本

* ./uninstall.sh - 单独卸载软件

  * 大版本升级可以先删除软件,再重新安装,只选择要安装的软件y,其余选择n.

    * ./uninstall.sh

    * ./install.sh

* ./pureftpd\_vhost.sh - 管理FTP账号

* ./auto\_fdisk.sh - 挂载云数据盘

* ./backup.sh - 备份




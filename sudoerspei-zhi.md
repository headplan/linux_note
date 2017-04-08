# Sudoers配置

```
# SUDO_LOGS
Defaults      logfile=/tmp/sudo_logs.log

# HEADPLAN_GROUP
HEADPLAN_GROUP       ALL=(ALL)       NOPASSWD:CMD_SYSTEM,CMD_SERVICE
User_Alias      HEADPLAN_GROUP = headplan,reallyli,richard

#Cmnd_Alias
Cmnd_Alias      CMD_SYSTEM = ALL,!/sbin/init,!/sbin/halt,!/sbin/reboot,!/sbin/shutdown,!/bin/su,!/bin/su - root,!/bin/su -,!/usr/sbin/visudo,!/bin/bash
Cmnd_Alias      CMD_SERVICE = !/etc/init.d/network,!/etc/init.d/sshd,!/etc/init.d/iptables,!/sbin/service,!/sbin/chkconfig
```




# CPU性能

```
uptime # 平均负载
grep 'model name' /proc/cpuinfo | wc -l # CPU数

# Linux系统压力测试工具
stress:异常进程模拟平均负载升高的场景
# yum安装
yum install -y epel-release
yum install -y stress

# CPU性能监控
sysstat
git clone git://github.com/sysstat/sysstat
cd sysstat
./configure --enable-install-cron
make
make install
```




# 归纳总结

```
uptime # 平均负载:1分钟,5分钟,15分钟
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

#### CPU密集型进程

```
# 模拟CPU使用率100%的场景
stress --cpu 1 --timeout 600

# 查看平均负载
watch -d uptime

# 查看CPU使用率的变化
# -P ALL 表示监控所有 CPU,后面数字 5 表示间隔 5 秒后输出一组数据
mpstat -P ALL 5
```

#### I/O密集型进程

#### 大量进程场景




# 服务管理launchctl

launchctl是一个统一的服务管理框架 , 可以启动、停止和管理守护进程、应用程序、进程和脚本等 . launchctl是通过配置文件来指定执行周期和任务的 . 

> 当然mac也可以像linux系统一样 , 使用crontab命令来添加定时任务 .

### 编写plist文件

launchctl 将根据plist文件的信息来启动任务 . plist脚本一般存放在以下目录 : 

`/Library/LaunchDaemons` - 只要系统启动了 , 哪怕用户不登陆系统也会被执行 . 

`/Library/LaunchAgents` - 当用户登陆系统后才会被执行 . 

更多的plist存放目录 : 

```
~/Library/LaunchAgents 由用户自己定义的任务项
/Library/LaunchAgents 由管理员为用户定义的任务项
/Library/LaunchDaemons 由管理员定义的守护进程任务项
/System/Library/LaunchAgents 由MacOSX为用户定义的任务项
/System/Library/LaunchDaemons 由MacOSX定义的守护进程任务项
```

进入`~/Library/LaunchAgents` , 创建一个plist文件`com.demo.plist`

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <!-- Label唯一的标识 -->
  <key>Label</key>
  <string>com.demo.plist</string>
  <!-- 指定要运行的脚本 -->
  <key>ProgramArguments</key>
  <array>
    <string>/Users/demo/run.sh</string>
  </array>
  <!-- 指定要运行的时间 -->
  <key>StartCalendarInterval</key>
  <dict>
        <key>Minute</key>
        <integer>00</integer>
        <key>Hour</key>
        <integer>22</integer>
  </dict>
<!-- 标准输出文件 -->
<key>StandardOutPath</key>
<string>/Users/demo/run.log</string>
<!-- 标准错误输出文件，错误日志 -->
<key>StandardErrorPath</key>
<string>/Users/demo/run.err</string>
</dict>
</plist>
```

### 加载命令

```
launchctl load -w com.demo.plist
```

这样任务就加载成功了 . 更多的命令 : 

```
# 加载任务,-w选项会将plist文件中无效的key覆盖掉,建议加上
$ launchctl load -w com.demo.plist

# 删除任务
$ launchctl unload -w com.demo.plist

# 查看任务列表, 使用 grep '任务部分名字' 过滤
$ launchctl list | grep 'com.demo'

# 开始任务
$ launchctl start com.demo.plist

# 结束任务
$ launchctl stop com.demo.plist
```

> 如果任务被修改了 , 那么必须先unload , 然后重新load . start可以测试任务 , 这个是立即执行 , 不管时间到了没有 . 执行start和unload前 , 任务必须先load过 , 否则报错 . stop可以停止任务 .




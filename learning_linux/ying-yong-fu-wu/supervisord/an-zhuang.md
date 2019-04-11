# 安装

安装分为有网络安装和无网络安装 . 由于无网络安装环节需要在有网络的主机上进行依赖包下载 , 所以相对繁琐麻烦 , 如果本机没有网络 , 可以考虑使用squid代理来进行安装 , 下面介绍的是有网络安装 .

安装命令可以使用easy\_install supervisor或者 pip install supervisor 或者去pypi官网上下载最新版本进行解压安装 . 也可以使用yum或者apt , 但不保证是最新版本 .

**使用pip install安装**

```
pip install supervisor
```

根据系统Python的权限 , 可能需要成为root用户才能使用pip成功安装Supervisor .

**下载安装**

[https://pypi.org/project/supervisor/](https://pypi.org/project/supervisor/)

如果系统没有安装pip , 则需要下载Supervisor发行版并手动安装 .

可以从PyPi下载当前和以前的Supervisor版本 . 解压缩软件存档后 , 运行 :

```
python setup.py install
```

根据系统Python的权限 , 可能需要成为root用户才能成功调用安装命令 .

#### 创建配置文件

Supervisor相当强大 , 提供了很丰富的功能 , 不过我们可能只需要用到其中一小部分 . 安装完成之后 , 可以编写配置文件 , 来满足自己的需求 . 为了方便 , 把配置分成两部分 : supervisord\(supervisor是一个C/S模型的程序 , 这是server端 , 对应的有client端supervisorctl\)和应用程序\(即我们要管理的程序\) .

首先来看 supervisord 的配置文件 . 安装完 supervisor 之后 , 可以运行`echo_supervisord_conf`命令输出默认的配置项 , 也可以重定向到一个配置文件里 :

```
echo_supervisord_conf > /etc/supervisord.conf
```

**配置文件详解**

```
; Sample supervisor config file.
;
; For more information on the config file, please see:
; http://supervisord.org/configuration.html
;
; Notes:
;  - Shell expansion ("~" or "$HOME") is not supported.  Environment
;    variables can be expanded using this syntax: "%(ENV_HOME)s".
;  - Quotes around values are not supported, except in the case of
;    the environment= options as shown below.
;  - Comments must have a leading space: "a=b ;comment" not "a=b;comment".
;  - Command will be truncated if it looks like a config file comment, e.g.
;    "command=bash -c 'foo ; bar'" will truncate to "command=bash -c 'foo ".

[unix_http_server]
file=/tmp/supervisor.sock   ; UNIX socket文件,supervisorctl会使用
;chmod=0700                 ; socket文件的mode,默认是 0700
;chown=nobody:nogroup       ; socket文件的owner,格式 uid:gid
;username=user              ; http_server用户,默认无 (open server)
;password=123               ; http_server密码,默认无 (open server)

;[inet_http_server]         ; HTTP服务器,提供web管理界面
;port=127.0.0.1:9001        ; Web管理后台运行的IP和端口,如果开放到公网,需要注意安全性
;username=user              ; 登录管理后台的用户名 (open server)
;password=123               ; 登录管理后台的密码 (open server)

[supervisord]
logfile=/tmp/supervisord.log ; 日志文件,默认是$CWD/supervisord.log
logfile_maxbytes=50MB        ; 日志文件大小,超出会rotate,默认 50MB
logfile_backups=10           ; 日志文件保留备份数量默认10
loglevel=info                ; 日志级别,默认info,其它:debug,warn,trace
pidfile=/tmp/supervisord.pid ; pid文件
nodaemon=false               ; 是否在前台启动,默认是false,即以daemon的方式启动
minfds=1024                  ; 可以打开的文件描述符的最小值,默认1024
minprocs=200                 ; 可以打开的进程数的最小值,默认200
;umask=022                   ; 进程文件创建的默认权限,默认022
;user=supervisord            ; 默认是当前启动的用户
;identifier=supervisor       ; 标识符supervisord,默认是'supervisor'
;directory=/tmp              ; 默认启动时间不会切换
;nocleanup=true              ; 在启动时不清理临时文件,默认值为false
;childlogdir=/tmp            ; 'AUTO'子进程日志目录,默认$TEMP
;environment=KEY="value"     ; 增加一个环境变量键值对,key="value"
;strip_ansi=false            ; 在log日志里去掉ansi转义编码,默认是false

; 下面的部分选项必须保留在RPC的配置文件中
; supervisorctl/web接口 使用以下配置来管理
; The rpcinterface:supervisor section must remain in the config file for
; RPC (supervisorctl/web interface) to work.  Additional interfaces may be
; added by defining them in separate [rpcinterface:x] sections.

[rpcinterface:supervisor]
supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface

; The supervisorctl section configures how supervisorctl will connect to
; supervisord.  configure it match the settings in either the unix_http_server
; or inet_http_server section.

[supervisorctl]
serverurl=unix:///tmp/supervisor.sock ; 通过UNIX socket连接supervisord,路径与unix_http_server部分的file一致
;serverurl=http://127.0.0.1:9001 ; 通过HTTP的方式连接supervisord
;username=chris              ; should be same as in [*_http_server] if set
;password=123                ; should be same as in [*_http_server] if set
;prompt=mysupervisor         ; cmd line prompt (default "supervisor")
;history_file=~/.sc_history  ; use readline history if available

; 以下是被管理的示例程序显示所有可能用到的配置
; 创建一个或多个程序:要遵循以下的键值对规则
; supervisor.

;[program:theprogramname]
;command=/bin/cat              ; 程序的启动命令(使用绝对路径)
;process_name=%(program_name)s ; process_name表示(默认是 %(program_name)s)
;numprocs=1                    ; 启动时的进程数(默认 1)
;directory=/tmp                ; 执行时切换到的目录 (def no cwd)
;umask=022                     ; 进程文件创建的默认权限 (default None)
;priority=999                  ; 相对启动优先级 (default 999)
;autostart=true                ; 是否跟随supervisord程序启动该监控程序 (default: true)
;startsecs=1                   ; # 在设定时间内,程序必须保持运行 (def. 1)
;startretries=3                ; 当启动失败时尝试的最大次数 (default 3)
;autorestart=unexpected        ; 如果退出后,什么状态退出的去重启,默认非意外的 (def: unexpected)
;exitcodes=0                   ; 'expected' 符合退出代码之后去重启 (default 0)
;stopsignal=QUIT               ; 用于杀死进程的信号 (default TERM)
;stopwaitsecs=10               ; 最大等待秒数SIGKILL (default 10)
;stopasgroup=false             ; 发送停止信号到Unix进程组 (default false)
;killasgroup=false             ; SIGKILL UNIX进程组 (def false)
;user=chrism                   ; setuid to this UNIX account to run the program
;redirect_stderr=true          ; 是否开启程序标准错误输出的重定向 (default false)
;stdout_logfile=/a/path        ; 标准输出路径; default AUTO
;stdout_logfile_maxbytes=1MB   ; 文件最大大小 # 日志文件进行切割 (default 50MB)
;stdout_logfile_backups=10     ; # 日志文件备份数目 (0 means none, default 10)
;stdout_capture_maxbytes=1MB   ; '捕获模式'中的字节数 (default 0)
;stdout_events_enabled=false   ; 在标准输出写入文件时发出事件 (default false)
;stdout_syslog=false           ; send stdout to syslog with process name (default false)
;stderr_logfile=/a/path        ; 标准错误输出,NONE for none;default AUTO
;stderr_logfile_maxbytes=1MB   ; 文件最大大小 # logfile bytes b4 rotation (default 50MB)
;stderr_logfile_backups=10     ; # of stderr logfile backups (0 means none, default 10)
;stderr_capture_maxbytes=1MB   ; number of bytes in 'capturemode' (default 0)
;stderr_events_enabled=false   ; emit events on stderr writes (default false)
;stderr_syslog=false           ; send stderr to syslog with process name (default false)
;environment=A="1",B="2"       ; 添加进程环境变量 (def no adds)
;serverurl=AUTO                ; 覆盖serverurl计算 (childutils)

; 下面是event事件部分所有可能设置的值,大部分同上面一样。
; The sample eventlistener section below shows all possible eventlistener
; subsection values.  Create one or more 'real' eventlistener: sections to be
; able to handle event notifications sent by supervisord.

;[eventlistener:theeventlistenername]
;command=/bin/eventlistener    ; the program (relative uses PATH, can take args)
;process_name=%(program_name)s ; process_name expr (default %(program_name)s)
;numprocs=1                    ; number of processes copies to start (def 1)
;events=EVENT                  ; event notif. types to subscribe to (req'd)
;buffer_size=10                ; event buffer queue size (default 10)
;directory=/tmp                ; directory to cwd to before exec (def no cwd)
;umask=022                     ; umask for process (default None)
;priority=-1                   ; the relative start priority (default -1)
;autostart=true                ; start at supervisord start (default: true)
;startsecs=1                   ; # of secs prog must stay up to be running (def. 1)
;startretries=3                ; max # of serial start failures when starting (default 3)
;autorestart=unexpected        ; autorestart if exited after running (def: unexpected)
;exitcodes=0                   ; 'expected' exit codes used with autorestart (default 0)
;stopsignal=QUIT               ; signal used to kill process (default TERM)
;stopwaitsecs=10               ; max num secs to wait b4 SIGKILL (default 10)
;stopasgroup=false             ; send stop signal to the UNIX process group (default false)
;killasgroup=false             ; SIGKILL the UNIX process group (def false)
;user=chrism                   ; setuid to this UNIX account to run the program
;redirect_stderr=false         ; redirect_stderr=true is not allowed for eventlisteners
;stdout_logfile=/a/path        ; stdout log path, NONE for none; default AUTO
;stdout_logfile_maxbytes=1MB   ; max # logfile bytes b4 rotation (default 50MB)
;stdout_logfile_backups=10     ; # of stdout logfile backups (0 means none, default 10)
;stdout_events_enabled=false   ; emit events on stdout writes (default false)
;stdout_syslog=false           ; send stdout to syslog with process name (default false)
;stderr_logfile=/a/path        ; stderr log path, NONE for none; default AUTO
;stderr_logfile_maxbytes=1MB   ; max # logfile bytes b4 rotation (default 50MB)
;stderr_logfile_backups=10     ; # of stderr logfile backups (0 means none, default 10)
;stderr_events_enabled=false   ; emit events on stderr writes (default false)
;stderr_syslog=false           ; send stderr to syslog with process name (default false)
;environment=A="1",B="2"       ; process environment additions
;serverurl=AUTO                ; override serverurl computation (childutils)

; The sample group section below shows all possible group values.  Create one
; or more 'real' group: sections to create "heterogeneous" process groups.

;[group:thegroupname]
;programs=progname1,progname2  ; 这里的progname1,progname2就是定义的监控管理程序的名字,如[program:x]这里就是x
;priority=999                  ; the relative start priority (default 999)

; 下面的 [include] 选项只能包含一个files 设置,功能是定义supervisor管理程序的配置文件,可以单独的移除去,和主配置文件分开,方便.
; The [include] section can just contain the "files" setting.  This
; setting can list multiple files (separated by whitespace or
; newlines).  It can also contain wildcards.  The filenames are
; interpreted as relative to this file.  Included files *cannot*
; include files themselves.

;[include] 定义管理监控程序的配置文件的路径
;files = relative/directory/*.ini
```

创建supervisor存放监控程序的目录 , 并修改supervisod.conf文件 :

```
mkdir -pv /etc/supervisor/config.d
```

修改supervisord主程序文件 :

```
sed -i '$ a [include]' /etc/supervisord.conf
sed -i '$ a files = /etc/supervisor/config.d/*.ini' /etc/supervisord.conf
```

在init.d中创建开始停止脚本 :

官网提供的init脚本

```
https://github.com/Supervisor/initscripts
```

CentOS 7 以后 , 使用Systemd来管理自启动服务 , 下载对应的脚本 :

```
wget -O /usr/lib/systemd/system/supervisord.service https://raw.githubusercontent.com/Supervisor/initscripts/master/centos-systemd-etcs
```

#### 启动Supervisor服务

重新加载Systemd配置 , 使得Supervisord配置生效 : 

```
systemctl daemon-reload
```

然后设置自启动 , 并启动Supervisor服务 : 

```
systemctl enable supervisord.service
systemctl start supervisord.service
```




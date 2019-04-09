# 用户\(user\)和用户组\(group\)的配置

### 用户\(user\)

**配置文件**

```
/etc/passwd # 用户(user)的配置文件; 
/etc/shadow # 用户(user)影子口令文件;
```

**管理工具**

useradd

```
# 添加用户:保存在/etc/passwd文件中
useradd(选项)(参数)
adduser
    # 在Slackware中,adduser指令是个script程序,利用交谈的方式取得输入的用户帐号资料,然后再交由真正建立帐号的useradd命令建立新用户;
    # 在Red Hat Linux中,adduser命令则是useradd命令的符号连接,两者实际上是同一个指令.

    选项
    -b, --base-dir BASE_DIR:新账户的主目录的基目录 - useradd -b /home/test
    -c, --comment COMMENT:新账户的GECOS字段,一般为备注文字,保存在passwd的备注栏位中
    -d, --home-dir HOME_DIR:新账户的主目录,登入时的起始目录
    -D, --defaults:显示或更改默认的useradd配置
    -e, --expiredate EXPIRE_DATE:新账户的过期日期,账号的有效期限
    -f, --inactive INACTIVE:新账户的密码不活动期,指定在密码过期后多少天即关闭该帐号
    -g, --gid GROUP:新账户主组的名称或ID,指定用户所属群组
    -G, --groups GROUPS:新账户的附加组列表,指定用户所属的附加群组
    -h, --help:显示此帮助信息并推出
    -k, --skel SKEL_DIR:使用此目录作为骨架目录
    -K, --key KEY=VALUE:不使用/etc/login.defs中的默认值
    -l, --no-log-init:不要将此用户添加到最近登录和登录失败数据库
    -m, --create-home:创建用户的主目录,自动建立用户的登入目录
    -M, --no-create-home:不创建用户的主目录,不要自动建立用户的登入目录
    -N, --no-user-group:不创建同名的组
    -n:取消建立以用户名称为名的群组
    -o, --non-unique:允许使用重复的UID创建用户
    -p, --password PASSWORD:加密后的新账户密码
    -r, --system:创建一个系统账户
    -R, --root CHROOT_DIR:chroot 到的目录
    -s, --shell SHELL:新账户的登录shell,指定用户登入后所使用的shell
    -u, --uid UID:新账户的用户ID,指定用户ID
    -U, --user-group:创建与用户同名的组
    -Z, --selinux-user SEUSER:为 SELinux 用户映射使用指定 SEUSER

    参数
    用户名:要创建的用户名
```

passwd

```
# 为用户设置密码 
passwd
# 修改用户命令,可以通过usermod修改登录名,用户的家目录等等
usermod
# 同步用户从/etc/passwd到/etc/shadow
userdel
pwcov
# 校验用户配置文件/etc/passwd 和/etc/shadow 文件内容是否合法或完整
pwck 
pwunconv 注：是pwcov 的立逆向操作，是从/etc/shadow和 /etc/passwd 创建/etc/passwd ，然后会删除 /etc/shadow 文件； 
finger 注：查看用户信息工具 
id 注：查看用户的UID、GID及所归属的用户组 
chfn 注：更改用户信息工具 
su 注：用户切换工具 
sudo 注：sudo 是通过另一个用户来执行命令（execute a command as another user），su 是用来切换用户，然后通过切换到的用户来完成相应的任务，但sudo 能后面直接执行命令，比如sudo 不需要root 密码就可以执行root 赋与的执行只有root才能执行相应的命令；但得通过visudo 来编辑/etc/sudoers来实现； 
visudo 注：visodo 是编辑 /etc/sudoers 的命令；也可以不用这个命令，直接用vi 来编辑 /etc/sudoers 的效果是一样的； 
sudoedit 注：和sudo 功能差不多；
```

### 用户组\(group\)

```
/etc/group # 用户组(group)配置文件;
/etc/gshadow # 用户组(group)的影子文件;
```

**管理工具**

```
groupadd 注：添加用户组； 
groupdel 注：删除用户组； 
groupmod 注：修改用户组信息 
groups 注：显示用户所属的用户组 
grpck 
grpconv 注：通过/etc/group和/etc/gshadow 的文件内容来同步或创建/etc/gshadow ，如果/etc/gshadow 不存在则创建；
```




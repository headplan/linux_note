# 用户\(user\)和用户组\(group\)存储文件

```
# 配置文件
/etc/passwd # 用户(user)的配置文件;
/etc/shadow # 用户(user)影子口令文件;
/etc/group # 用户组(group)配置文件;
/etc/gshadow # 用户组(group)的影子文件;
/etc/skel # 用户的骨架目录,每次新建用户时都会将这个目录下的文件复制到用户家目录下来布置环境;
/etc/login.defs # 用户创建规则配置文件;
/etc/default/useradd # 通过useradd添加用户时的默认规则
```

**/etc/passwd**

* 用户名
* 用户密码\(默认为x,加密后的字符串放在/etc/shadow中\)
* 用户ID\(uid\)
* 用户初始组ID\(gid\)
* 用户描述信息\(可用chfn修改,可用finger查询\)
* 用户家目录
* 用户使用哪种shell\(在**/etc/shells**下是规定了可以使用的Shell\)

```
headplan:x:1001:1001:My Username:/home/headplan:/bin/bash
```

**/etc/shadow**

* 用户名
* 用户加密的密码
* 上次修改密码的时间\(上次修改距离1970/1/1的天数.17000/365+1970\)
* 密码最短修改时间间隔
* 密码最长修改时间间隔
* 密码警告时间\(密码距离到达第四个字段多长时间时需要会发出警告\)
* 非活跃期\(当密码过期后还有多少天可以使用\)
* 密码到期日\(过了这个时间用户就无法使用了\)

```
headplan:$6$F43...:17000:0:99999:7:::
```

**/etc/group**

* 用户名\(也就是这个用户的初始组\)
* 加密的组密码
* 组ID\(gid\)
* 组的用户\(以这个组为附加值的用户\)

```
headplan:x:1001:vagrant
```

初始组与附加组的概念:

> 用一个通俗的解释,你刚出生时只属于一个组,就是你的家,而且这个组一般是不会变的,这个家就是你的初始组,生你的时候家必须存在,所以用-g指定的那个组,也就必须存在;随着你的长大,你又加入了很多组,比如小学,初中,高中,大学等等,但是这些组不会覆盖你的初始组,你还是属于你的家,这就是附加组.

**/etc/gshadow**

* 用户名\(也就是这个用户的初始组\)
* 加密的组密码\(!表示还没有设置\)
* 组的用户\(以这个组为附加值的用户\)

```
headplan:!::vagrant
```

**/etc/skel**

> 用户的骨架目录,每次新建用户时都会将这个目录下的文件复制到用户家目录下来布置环境.

/etc/skel目录一般是存放用户启动文件的目录,这个目录是由root权限控制.当我们添加用户时,这个目录下的文件自动复制到新添加的用户的家目录下./etc/skel目录下的文件都是隐藏文件,也就是类似.file格式的.我们可通过修改、添加、删除/etc/skel目录下的文件,来为用户提供一个统一、标准的、默认的用户环境.

> 注意:目录下的文件,一般是用useradd或adduser命令添加用户\(user\)时,系统自动复制到新添加用户\(user\)的家目录下.如果通过修改/etc/passwd来添加用户时,可以自己创建用户的家目录,然后把/etc/skel下的文件复制到用户的家目录下,然后要用chown来改变新用户家目录的属主.

**/etc/login.defs**

> 文件是创建用户时的一些规划,比如创建用户时,是否需要家目录,UID和GID的范围,用户的期限等等.文件可以通过root来定义.
>
> 注意:该文件里的配置对root用户无效.如果/etc/shadow文件里有相同的选项,则以/etc/shadow里的设置为准,也就是说/etc/shadow的配置优先级高于/etc/login.defs
>
> 更多关于密码加固的策略在/etc/pam.d/system-auth中配置,这里可以另开一个文档记录

```
# *REQUIRED*
#   Directory where mailboxes reside, _or_ name of file, relative to the
#   home directory.  If you _do_ define both, MAIL_DIR takes precedence.
#   QMAIL_DIR is for Qmail
#
#QMAIL_DIR    Maildir
# 创建用户时在目录/var/spool/mail中创建一个用户mail文件
MAIL_DIR    /var/spool/mail
# 邮件驻留在家目录的.mail文件中,如果MAIL_DIR同时定义优先级高于此项
#MAIL_FILE    .mail

# Password aging controls:
#
#    PASS_MAX_DAYS    Maximum number of days a password may be used.
#    PASS_MIN_DAYS    Minimum number of days allowed between password changes.
#    PASS_MIN_LEN    Minimum acceptable password length.
#    PASS_WARN_AGE    Number of days warning given before a password expires.
#
PASS_MAX_DAYS    99999 # 密码最大有效期(过期天数)
PASS_MIN_DAYS    0     # 两次修改密码需要的最小间隔天数
PASS_MIN_LEN    5      # 密码最小长度,对于root无效
PASS_WARN_AGE    7     # 密码过期前多少天开始提示警告

#
# Min/max values for automatic uid selection in useradd
#
UID_MIN                  1000 # 最小UID为1000,也就是说添加用户时UID是从1000开始的
UID_MAX                 60000 # 最大UID为60000
# System accounts
SYS_UID_MIN               201 # 系统账号最小UID
SYS_UID_MAX               999 # 系统账号最大UID

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN                  1000 # 最小GID
GID_MAX                 60000 # 最大GID
# System accounts
SYS_GID_MIN               201 # 系统账号最小GID
SYS_GID_MAX               999 # 系统账号最大GID

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD    /usr/sbin/userdel_local # 删除用户时执行的脚本,这个脚本你是自定义,应该删除属于这个用户的定时任务等.

#
# If useradd should create home directories for users by default
# On RH systems, we do. This option is overridden with the -m flag on
# useradd command line.
#
CREATE_HOME    yes # 是否创建用户home目录

# The permission mask is initialized to this value. If not specified,
# the permission mask will be initialized to 022.
# 家目录权限初始值drwx------,如果不写默认初始值为022
UMASK           077

# This enables userdel to remove user groups if no members exist.
# 当一个组只有一个用户存在的时候,删除用户同时删除组
USERGROUPS_ENAB yes

# Use SHA512 to encrypt password.
ENCRYPT_METHOD SHA512 # 指定的密码的加密方式
```

**/etc/default/useradd**

```
# useradd defaults file
GROUP=100             # 用户组ID,可以查看到users组的ID就是100
HOME=/home            # 把用户的家目录建在/home中
INACTIVE=-1           # 是否启用帐号过期停权,-1表示不启用
EXPIRE=               # 帐号终止日期,不设置表示不启用
SHELL=/bin/bash       # 用户所用Shell的类型
SKEL=/etc/skel        # 初始化用户的家目录所需文件存放的位置
CREATE_MAIL_SPOOL=yes # 是否在目录/var/spool/mail中创建用户mail文件
```




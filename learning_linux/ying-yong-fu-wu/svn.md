# SVN

### SVN服务器搭建

> 记录详细的搭建流程
>
> [http://www.ha97.com/4467.html](http://www.ha97.com/4467.html)
>
> [http://yielon.blog.51cto.com/6579928/1159925/](http://yielon.blog.51cto.com/6579928/1159925/)

**SVN简介和工作原理**

```
subversion（简称svn）是近几年崛起的版本管理软件，是cvs的接班人，目前绝大多数开源软件都使用svn作为代码版本管理软件。
Subversion支持linux和windows，但较多安装在linux下。

svn服务器有两种运行方式:独立服务器和借助于apache - svn://或http://
svn客户端tortoisesvn

svn的基本工作原理:
在一台服务器上建立一个源代码库,库里可以存放许多不同项目的源程序.
有源代码库管理员统一管理这些源程序.
每个用户在使用源代码库之前，首先要把源代码库里德项目文件下载到本地,
然后开发人员可以在本地修改，左后用svn命令进行提交，由源代码库统一管理修改.

版本控制解决了：
*代码管理混乱
*解决代码冲突困难
*在代码整合期间引发bug
*无法对代码的拥有者进行权限控制
*项目不同版本的发布困难
```

**Subversion目录说明**

```
*dav目录:是提供apache与mod_dav_svn使用的目录，让他们存储内部数据
*db目录:就是所有版本控制的数据存放文件
*hooks目录:放置hook脚本文件的目录
*locks目录:用来放置subversion见艰苦锁定数据的目录，用来追踪存取文件库的客户端
*format文件:是一个文本文件，里面只放了一个整数。表示当前文件库配置的版本号
*conf目录:是这个仓库的配置文件（仓库的用户访问账号、权限等）
```

**安装软件包**

```
yum install -y subversion mysql-server httpd mod_dav_svn mod_perl sendmail wget gcc-c++ make unzip perl* ntsysv vim-enhanced

# 报错
# You could try using --skip-broken to work around the problem
# You could try running: rpm -Va --nofiles --nodigest
yum clean all
rpm --rebuilddb
yum update
# 这里跳过安装
--skip-broken

subversion # SVN服务器
subversion-devel # SVN服务器开发包
mysql-server # 用于codestriker
httpd mod_dav_svn mod_perl # 用于支持WEB方式管理SVN服务器
sendmail # 用于配置用户提交代码后发邮件提醒
wget gcc-c++ make unzip perl* # 必备软件包
ntsysv vim-enhanced # 可选

# 查看svn安装位置
rpm -ql subversion
```

**配置SVN服务器**

```
1.新建一个目录用于存储SVN所有文件
# mkdir -p /home/svn

2.新建一个版本仓库
# svnadmin create /home/svn/project

3.初始化版本仓库中的目录
# mkdir project project/server project/client project/test (建立临时目录)
# svn import project/ file:///home/svn/project -m “初始化SVN目录”
# rm -rf project (删除临时建立的目录)

4.添加用户
在/home/svn/project/conf/passwd文件添加一个形如“username=password”的条目

[users]
# harry = harryssecret
# sally = sallyssecret
pm = pm_pw
server_group = server_pw
client_group = client_pw
test_group = test_pw

5.修改用户访问策略
/home/svn/project/conf/authz记录用户的访问策略,以下是参考:

[groups]
project_p = pm
project_s = server1,server2,server3
project_c = client1,client2,client3
project_t = test1,test1,test1

[project:/]
@project_p = rw
* =

[project:/server]
@project_p = rw
@project_s = rw
* =

[project:/client]
@project_p = rw
@project_c = rw
* =

[project:/doc]
@project_p = rw
@project_s = r
@project_c = r
@project_t = r
* =

说明:
以上信息表示,只有project_p用户组有根目录的读写权
r表示对该目录有读权限
w表示对该目录有写权限
rw表示对该目录有读写权限
最后一行的* = 表示除了上面设置了权限的用户组之外
其他任何人都被禁止访问本目录.这个很重要,一定要加上.

6.修改svnserve.conf文件,让用户和策略配置升效.
svnserve.conf内容如下:

[general]
anon-access = none
auth-access = write
password-db = /home/svn/project/conf/passwd
authz-db = /home/svn/project/conf/authz

7.启动服务器
# svnserve -d -r /home/svn
注意:如果修改了svn配置,需要重启svn服务

# ps -aux | grep svnserve
# kill -9 ID号
# svnserve -d -r /home/svn

8.测试服务器
# 在此之前需要配置一下防火墙,打开端口3690的访问权限
# 允许3690端口
iptables -I INPUT 4 -p tcp -m state --state NEW -m tcp --dport 3690 -j ACCEPT
# 保存iptables规则
service iptables save
# 查看iptables规则
iptables -nvL

# svn co svn://192.168.60.10/project
Authentication realm: <svn://192.168.60.10:3690> 92731041-2dae-4c23-97fd-9e1ed7f0d18d
Password for 'root':
Authentication realm: <svn://192.168.60.10:3690> 92731041-2dae-4c23-97fd-9e1ed7f0d18d
Username: server_group
Password for 'server_group':
svn: Authorization failed ( server_group没用根目录的访问权 )

# svn co svn://192.168.60.10/project
Authentication realm: <svn://192.168.60.10:3690> 92731041-2dae-4c23-97fd-9e1ed7f0d18d
Password for ‘root’:
Authentication realm: <svn://192.168.60.10:3690> 92731041-2dae-4c23-97fd-9e1ed7f0d18d
Username: pm
Password for ‘pm’:
A    project/test
A    project/server
A    project/client
Checked out revision 1.  ( 测试提取成功 )

# cd project/server
# vim main.c
# svn add main.c
# svn commit main.c -m “测试一下我的C程序,看什么看,不行啊??”
Adding         main.c
Transmitting file data .
Committed revision 2.  ( 测试提交成功 )
```

**配置SVN服务器的HTTP支持**

    1.转换SVN服务器的密码
    由于SVN服务器的密码是明文的,HTTP服务器不与支持,所以需要转换成HTTP支持的格式.
    写了一个Perl脚本完成这个工作.
    脚本内容如下:
    # cd /home/svn/project/conf/
    # vim PtoWP.pl

    #!/usr/bin/perl

    use warnings;
    use strict;

    # open the svn passwd file
    open (FILE, "passwd") or die ("Cannot open the passwd file!!!\n");

    # clear the apache passwd file
    open (OUT_FILE, ">webpasswd") or die ("Cannot open the webpasswd file!!!\n");
    close (OUT_FILE);

    #begin
    foreach (<FILE>) {
        if($_ =~ m/^[^#].*=/) {
            $_ =~ s/=//;
            `htpasswd -b webpasswd $_`;
        }
    }

    # chmod +x PtoWP.pl
    # ./PtoWP.pl
    Adding password for user pm
    Adding password for user server_group
    Adding password for user client_group
    Adding password for user test_group
    现在目录下会多一个webpasswd文件。

    2.修改httpd.conf,添加关于SVN服务器的内容
    编辑/etc/httpd/conf/httpd.conf,在最后添加如下信息:
    <Location /project>
    DAV svn
    SVNPath /home/svn/project/
    AuthType Basic
    AuthName "svn for project"
    AuthUserFile /home/svn/project/conf/webpasswd
    AuthzSVNAccessFile /home/svn/project/conf/authz
    Satisfy all
    Require valid-user
    </Location>

    3.修改svn目录的属主为apache帐号
    chown -R apache.apache /home/svn/project/

    4.重启Web服务器：
    # /etc/init.d/httpd restart
    # 这里80端口可能会被占用,可以修改一个,记得加入防火墙端口白名单
    Stopping httpd: [FAILED]
    Starting httpd: [ OK ]

    5.用浏览器访问
    http://192.168.60.10/project/server/




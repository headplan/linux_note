# 常用建立用户分配权限

```
1.添加账户
useradd std02
passwd std02
也可以这样添加
useradd -n std02 -p std02

2.新建一个子目录
/home/public
让它被所有的用户共享,而且拥有所有权限,但不能被非属主删除
mkdir /home/public
chmod a+trwx /home/public
3.让一个子目录/home/std02私有化只允许std02所独享
mkdir  /home/student02
chown std02 /home/student02 # 私有化
chmod a-rwx /home/student02 # 独享
chmod  u+rwx /home/student02
上面的命令等于
chmod 700 /home/student02

3.让一用户成为一个用户组群中的成员
groupadd student
useradd -g student -n std03

规划用户与组群
案例:有程序开发员5人,项目管理员2人,分别取名为:
prg01~prg05
mgr01,mgr2
并分别从属于组program与manage
现按下列要求规划:
(1)每个开发员拥有自己的帐户,用户名:prg??,密码:prog??;
(2)每个开发员从属于program组,并共享两个子目录:program与source,而且拥有所有权限;
(3)每个管理员拥有自己的帐户,用户名mgr??,密码:mngr??;
(4)每个管理员从属于manage组,并共享两个子目录:project与document,而且拥有所有权限;
(5)创建一个公共子目录/home/public,让它被所有的用户共享,而且拥有所有权限,但不能被非属主删除.

# 创建两个组群
# groupadd program
# groupadd manage
# 添加五个开发员
# useradd -g program -n prg 01 -p prog01
# useradd -g program -n prg 02 -p prog02
# useradd -g program -n prg 03 -p prog03
# useradd -g program -n prg 04 -p prog04
# useradd -g program -n prg 05 -p prog05
# 添加两个管理员
# useradd -g manage -n mgr01 mngr01
# useradd -g manage -n mgr02 mngr02
# 创建四个子目录
# mkdir /home/program
# mkdir /home/source
# mkdir /home/project
# mkdir /home/document

#chmod 770      /home/program
#chgrp program  /home/program
#chmod 770      /home/source
#chgrp program  /home/source
#chmod 770      /home/project
#chgrp manage   /home/project
#chmod 770      /home/document
#chgrp manage   /home/document

# 开辟一个公共子目录
# mkdir /home/public
# chmod a+rwxt /home/public

# chmod 777 /home/public
# chmod a+t /home/public

6.修改用户分组：

# usermod -G 组名 用户名
# usermod -a -G 组名 用户名 就可以追加额外组了
```




# Linux用户与用户组

一份运维笔记:[http://blog.csdn.net/no\_red/article/details/52725536](http://blog.csdn.net/no_red/article/details/52725536)

gogs搭建:[https://blog.mynook.info/post/host-your-own-git-server-using-gogs](https://blog.mynook.info/post/host-your-own-git-server-using-gogs)

两篇用户相关文章:

[http://www.cnblogs.com/licheng/p/6104080.html](http://www.cnblogs.com/licheng/p/6104080.html)

[http://www.jb51.net/LINUXjishu/43206.html](http://www.jb51.net/LINUXjishu/43206.html)

Linux是一个多用户,多任务的操作系统.

**1.Linxu的单用户多任务**

单用户多任务,比如我们用root用户登录系统,为了完成工作,我们需要同时执行多个任务,比如编辑文档,听音乐,同时打开MSN沟通等等.

**2.Linux的多用户,多任务**

有时可能是很多用户同时用同一个系统,但并不所有的用户都一定都要做同一件事,所以这就有多用户多任务之说.不同用户所具有的权限也不同,要完成不同的任务得需要不同的用户,也可以说不同的用户,可能完成的工作也不一样.

**3.用户的角色分区**

用户在系统中是分角色的,在Linux系统中,由于角色不同,权限和所完成的任务也不同;值得注意的是用户的角色是通过UID识别的,特别是UID;在系统管理中,系统管理员一定要坚守UID 唯一的特性.

* root用户 - 系统唯一,是真实的,可以登录系统,可以操作系统任何文件和命令,拥有最高权限.

* 虚拟用户 - 这类用户也被称之为伪用户或假用户,与真实用户区分开来.不具有登录系统的能力,但却是系统运行不可缺少的用户,比如bin、daemon、adm、ftp、mail等;这类用户都系统自身拥有的,而非后来添加的,当然我们也可以添加虚拟用户.

* 普通真实用户 - 这类用户能登录系统,但只能操作自己家目录的内容,权限有限.并且都是系统管理员自行添加的.

**4.多用户操作系统的安全**

多用户系统从事实来说对系统管理更为方便.从安全角度来说,多用户管理的系统更为安全,比如a用户下的某个文件不想让其它用户看到,只是设置一下文件的权限,只有a一个用户可读可写可编辑就行了,这样一来只有a一个用户可以对其私有文件进行操作,Linux在多用户下表现最佳,Linux能很好的保护每个用户的安全.


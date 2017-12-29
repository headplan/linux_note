# 关于C语言

#### C简介

C 语言是一种通用的高级语言 , 最初是由丹尼斯·里奇在贝尔实验室为开发 UNIX 操作系统而设计的 . C 语言最开始是于 1972 年在 DEC PDP-11 计算机上被首次实现 . 在 1978 年 , 布莱恩·柯林汉\(Brian Kernighan\)和丹尼斯·里奇\(Dennis Ritchie\)制作了 C 的第一个公开可用的描述 , 现在被称为 K&R 标准 . UNIX 操作系统 , C编译器和几乎所有的 UNIX 应用程序都是用 C 语言编写的 . 由于各种原因 , C 语言现在已经成为一种广泛使用的专业语言 .

* C 语言是为了编写 UNIX 操作系统而被发明的 . 
* C 语言是以 B 语言为基础的 , B 语言大概是在 1970 年被引进的 . 
* C 语言标准是于 1988 年由美国国家标准协会\(ANSI , 全称 American National Standard Institute\)制定的 . 
* 截至 1973 年 , UNIX 操作系统完全使用 C 语言编写 . 
* 目前 , C 语言是最广泛使用的系统程序设计语言 . 
* 大多数先进的软件都是使用 C 语言实现的 . 
* 当今最流行的Linux操作系统和RDBMS\(Relational Database Management System : 关系数据库管理系统\)MySQL都是使用C语言编写的 . 

#### C使用

C 语言最初是用于系统开发工作 , 特别是组成操作系统的程序 . 由于 C 语言所产生的代码运行速度与汇编语言编写的代码运行速度几乎一样 , 所以采用 C 语言作为系统开发语言 . 下面列举几个使用 C 的实例 :

* 操作系统
* 语言编译器
* 汇编器
* 文本编辑器
* 打印机
* 网络驱动器
* 现代程序
* 数据库
* 语言解释器
* 实体工具

#### C标准

C语言的发展历史大致上分为三个阶段 : Old Style C , C89和C99 . Ken Thompson和Dennis Ritchie发明C语言时有很多语法和现在并不一样 , 但为了向后兼容性\(Backward Compatibility\) , 这些语法仍然在C89和C99中保留下来了 , 这里不使用Old Style C , 但在必要的地方会加以说明 . C89是最早 的C语言规范 , 于1989年提出 , 1990年先由ANSI\(美国国家标准委员会,American National Standards Institute\)推出ANSI版本 , 后来被接纳为ISO国际标准\(ISO/IEC 9899:1990\) , 因而有时也称为C90 , 最经典的C语言教材\[K&R\]就是基于这个版本的 , C89是目前最广泛采用的C语言标准 , 大多数编译器都完全支持C89 . C99标准\(ISO/IEC 9899:1999\)是在1999年推出的 , 加 入了许多新的特性 , 但目前仍没有得到广泛支持 , 在C99推出之后相当长的一段时间里 , 连gcc也没有完全实现C99的所有特性 . C99标准详见\[C99\] . 

C标准的目的是为了精确定义C语言 , 而不是为了教别人怎么编程 , C标准在表达上追求准确和无歧义 , 却十分不容易看懂 , \[Standard C\]和\[Standard C Library\]是对C89及其修订版本的阐释\(可惜作者没有随C99更新\) , 比C标准更容易看懂 , 另外 , 参考\[C99 Rationale\]也有助于加深对C标准的理解 . 

**C11**

C11\(也被称为C1X\)指ISO标准ISO/IEC 9899:2011 , 是当前最新的C语言标准 . 

**新特性 : **

* 对齐处理（Alignment）的标准化（包括\_Alignas标志符，alignof运算符，aligned\_alloc函数以及&lt;stdalign.h&gt;头文件）。
* \_Noreturn 函数标记，类似于 gcc 的 \_\_attribute\_\_\(\(noreturn\)\)。
* \_Generic 关键字。
* 多线程（Multithreading）支持，包括：
  * \_Thread\_local存储类型标识符，&lt;threads.h&gt;头文件，里面包含了线程的创建和管理函数。
  * \_Atomic类型修饰符和&lt;stdatomic.h&gt;头文件。
* 增强的Unicode的支持。基于C Unicode技术报告ISO/IEC TR 19769:2004，增强了对Unicode的支持。包括为UTF-16/UTF-32编码增加了char16\_t和char32\_t数据类型，提供了包含unicode字符串转换函数的头文件&lt;uchar.h&gt;。
* 删除了 gets\(\) 函数，使用一个新的更安全的函数gets\_s\(\)替代。
* 增加了边界检查函数接口，定义了新的安全的函数，例如 fopen\_s\(\)，strcat\_s\(\) 等等。
* 增加了更多浮点处理宏\(宏\)。
* 匿名结构体/联合体支持。这个在gcc早已存在，C11将其引入标准。
* 静态断言（Static assertions），\_Static\_assert\(\)，在解释 \#if 和 \#error 之后被处理。
* 新的 fopen\(\) 模式，\("…x"\)。类似 POSIX 中的 O\_CREAT\|O\_EXCL，在文件锁中比较常用。
* 新增 quick\_exit\(\) 函数作为第三种终止程序的方式。当 exit\(\)失败时可以做最少的清理工作。




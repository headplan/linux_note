# ctags

> ctags（Generate tag files for source code）是vim下方便代码阅读的工具。尽管ctags也可以支持其它编辑器，但是它正式支持的只有VIM。并且VIM中已经默认安装了Ctags，它可以帮助程序员很容易地浏览源代码。

ctags 最先是用来生成C代码的tags文件，后来扩展成可以生成各类语言的tags, 有些语言也有专有的tags生成工具（比如java的jtags, python的 ptags\).

在源码目录下执行 : 

```
ctags –R .
```

“-R”表示递归创建，也就包括源代码根目录（当前目录）下的所有子目录。“\*”表示所有文件。这条命令会在当前目录下产生一个“tags”文件，当用户在当前目录中运行vi时，会自动载入此tags文件。Tags文件中包括这些对象的列表：用\#define定义的宏枚举型变量的值函数的定义、原型和声明名字空间（namespace）类型定义（typedefs）变量（包括定义和声明）类（class）、结构（struct）、枚举类型（enum）和联合（union）类、结构和联合中成员变量或函数VIM用这个“tags”文件来定位上面这些做了标记的对象。

**ctags配置**

使用sudo vim /etc/vim/vimrc 编辑vim的配置文档，在其中加入如下命令：

* set tags=/home/headplan/phpsrc/tags;"后面的路径是使用ctags -R 后生成的tags文件所在目录，如果需要配置多个tags，只需如下再添加即可
* set tags=/home/headplan/phpsrc/ext/tags;
* set autochdir

**ctags命令**

1. `ctags -R *` : 生成tags文件
2. `vim –t tag` : tag为要查找的变量或函数名等
3. `:ts` : 在vi命令行模式下列出一个tag列表供用户选择
4. `:tp` : 上一个标记
5. `:tn` : 下一个标记
6. `Ctrl+]` : 跳到光标所在函数或者结构体的定义处
7. `Ctrl+T` : 返回查找或跳转

> 最方便的方法是把光标移到变量名或函数名上 , 然后按下`Ctrl+]` , 这样就能直接跳到这个变量或函数定义的源文件中 , 并把光标定位到这一行 . 用`Ctrl+T`可以退回原来的地方 . 即使用户使用了N次`Ctrl+]`查找了N个变量 , 按N次`Ctrl+T`也能回到最初打开的文件 , 它会按原路返回 .

> 运行vim的时候 , 必须在tags文件所在的目录下运行 . 否则 , 运行vim的时候还要用`:set tags=`命令设定tags文件的路径 , 这样vim才能找到tags文件 . 在完成编码时 , 可以手工删掉tags文件 .




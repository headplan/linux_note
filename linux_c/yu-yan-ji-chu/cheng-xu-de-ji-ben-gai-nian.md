# 程序的基本概念

#### 程序和编程语言

程序由一系列指令\(Instruction\)组成 , 指令是指示计算机做某种运算的命令 , 通常包括以下几类 :

* **输入\(Input\)** - 从键盘 , 文件或者其它设备获取数据 . 
* **输出\(Output\)** - 把数据显示到屏幕 , 或者存入一个文件 , 或者发送到其它设备 . 
* **基本运算** - 执行最基本的数学运算\(加减乘除\)和数据存取 , 其实输入和输出也属于数据存取 . 
* **测试和分支\(Branch\)** - 测试某个条件 , 然后根据不同的测试结果执行不同的后续指令 . 
* **循环\(Loop\)** - 重复执行一系列操作 . 

在不同的编程语言\(Programming Language\)中 , 以上几种指令具有不同的形式 . 通常"指令"这个词专指**机器语言\(Machine Language\)**或者**汇编语言\(Assembly Language\)**等**低级语言**\(Low-level Language\)中的指令 , 而在C语言、C++、Java、Python等**高级语言**\(High-level Language\)中通常称为**语句\(Statement\)**或**表达式\(Expression\)** .

计算机只能对数字做运算 , 虽然高级语言中有大量的**符号** , 但这些符号都是**人为定义**的 , 最终**转换**成计算机可以直接处理的机器语言仍然是**数字 . **有了**汇编语言** , 把机器语言中的一组一组数字用**助记符**\(Mnemonic\)来表示 , 直接用这些助记符写出汇编程序 , 然后让**汇编器** \(Assembler\)去查表把助记**符替换成数字 **, 也就把汇编语言翻译成了**机器语言 . **汇编语言和机器语言的指令是一一对应的 , **汇编器**就是做一个简单的替换工作 .

C语言的语句和低级语言的指令之间不是简单的一一对应关系 , 一条`a=b+1`语句要翻译成三条汇编或机器指令 , 这个过程称为**编译**\(Compile\) , 由**编译器**\(Compiler\)来完成  . 用C语言编写的程序**必须经过编译**转成机器指令才能被计算机执行 . C语言是**可移植的**\(Portable\)或者称为**平台无关的**\(Platform Independent\) , 可以指计算机**体系结构**\(Architecture\) , 也可以指**操作系统**\(Operating System\) , 也可以指两者的组合 . 不同的计算机体系结构有不同的**指令集**\(Instruction Set\) , 可以识别的机器指令格式是不同的 , 各种计算机上都有C编译器 , 可以把C程序编译成该计算机自己的\(Native\)机器指令 , 可以在不同的计算机上编译执行 . 各种高级语言都具有C语言的这些优点,所以绝大部分程序是用高级语言编写的 , 只有和硬件关系密切的少数程序\(例如驱动程序\)才会用到低级语言 .

**编译执行过程**

![](/assets/bianyizhixingguocheng.png)

**解释执行过程**

有些高级语言以**解释**\(Interpret\)的方式执行 , 解释执行的过程和C语言的编译执行过程很不一 样 , 例如写一个Python源代码 , 保存成program.py\(通常Python程序的文件名后缀是.py\) , 然后并不需要生成目标代码 , 而是直接运行解释器\(Interpreter\)执行该源代码,解释器是一行 一行地翻译源代码 , 边翻译边执行的 :

![](/assets/jieshizhixingguocheng.png)

以上介绍的

机器语言称为第一代语言\(1GL,1st Generation Programming Language\)

汇编语言称为第二代语言\(2GL,2nd Generation Programming Language\)

C、C++、Java、Python等可以称为第三代语言\(3GL,3rd Generation Programming Language\)

后面还有4GL和5GL的概念 , 语言主要不是通过输入、输出、基本运算、测试分支和循环这些基本指令来编程的 , 语言更多是在描述要做什么\(Declarative\)而不是描述具体一步一步怎么做 \(Imperative\) , 具体一步一步怎么做完全交由编译器或解释器决定 , 例如SQL语言 \(SQL,Structured Query Language , 结构化查询语言\)就是这样的例子 .

**总结**

程序由语句或指令组成,在高级语言写的程序中通常叫语句,在低级语言写的程序中通常叫指令,计算机只能执行低级语言中的指令,高级语言要执行就必须先翻译成低级语言,翻译的方法有两种--编译和解释,虽然有这样的不便,但高级语言有一个好处是平台无关性.什么是平台?一种平台,就是一种体系结构,就是一种指令集,就是一种机器语言,这些都可看作是一一对应的,上文没有明确讲它们之间是一一对应的但读者应该能推理出这个结论,而高级语言和它们不是一一对应的,因此高级语言是平台无关的,概念之间像这样的数量对应关系尤其重要 .

---

#### 自然语言和形式语言

* **自然语言**\(Natural Language\)就是人类讲的语言 , 比如汉语、英语和法语 , 自然进化 . 
* **形式语言**\(Formal Language\)是为了特定应用而人为设计的语言 , 例如数学家用的数字和运算符号 , 化学家用的分子式等 . 

**编程语言**也是一种形式语言,是专门设计用来表达计算过程的形式语言 .

形式语言有严格的**语法\(Syntax\)规则** , 语法规则是由关于**符号\(Token\)**和**结构\(Structure\)**的规则所组成的 .

* **Token**的概念相当于自然语言中的单词和标点、数学式中的数和 运算符、化学分子式中的元素名和数字 . 
* 语法规则的第二个范畴是**结构**,也就是Token的排列方式 . 关于Token的规则称为**词法\(Lexical\)规则 **, 而关于语句结构的规则称为**语法\(Grammar\)规则** . 

形式语言和自然语言有很多共同之处 , 包括Token、结构和语义 , 但是也有很多不一样的地方 :

* 歧义性\(Ambiguity\) - 自然语言充满歧义 , 人们通过上下文的线索和其它一些信息来解决这个问题 . 形式语言的设计要求是清晰的、毫无歧义的 , 这意味着每一个语句必须有确切的含义而不管上下文如何 . 
* 冗余性\(Redundancy\) - 为了消除歧义减少误解 , 自然语言引入了相当多的冗余 . 结果是自然语言经常变得啰里啰嗦 , 而形式语言则更加紧凑,极少有冗余 . 
* 与字面意思的一致性 - 自然语言充斥着成语和隐喻\(Metaphor\) , 我在某种场合下说"The other shoe fell" , 可能并不是说谁的鞋掉了 . 而形式语言中字面\(Literal\)意思基本上就是真实意思 , 也有些特殊情况 , 例如C语言的转义序列\(Escape Sequence\) , 但也都会明确规定哪些字面意思不是真实意思 , 它们所表示的真实意思又是什么 . 

总之 , 阅读程序更好的方式是 , 识别Token,分解结构 , 从上到下从左到右地读往往不是一个好办法 .

---

#### 程序的调试

程序中的错误被叫做臭虫\(Bug\) , 而找到这些Bug并加以纠正的过程就叫做调试\(Debug\) .

程序中的Bug分类 :

**编译时错误**

编译器只能翻译语法正确的程序 , 否则将导致编译失败 , 无法产生目标代码 . 对于自然语言来说 , 一点语法错误不是很严重的问题 , 因为我们仍然可以读懂句子 . 可惜编译器就没那么宽容了 , 只要有哪怕一个很小的语法错误 , 编译器就会输出一条错误提示信息然后罢工 , 你就得不到你想要的目标代码 . 虽然大部分情况下编译器给出的错误提示信息就是你出错的代码行 , 但也有个别时候编译器给出的错误提示信息帮助不大 , 甚至会误导你 .

**运行时错误**

编译器检查不出这类错误 , 仍然可以生成目标代码 , 但在运行时会出错而导致程序崩溃 .

**逻辑错误和语义错误**

第三类错误是逻辑错误和语义错误 . 如果程序里有逻辑错误 , 编译和运行都会很顺利 , 看上去也不产生任何错误信息 , 但是程序没有干它该干的事情 , 而是干了些别的什么 . 当然不管怎么样 , 计算机只会按你写的程序去做 , 问题出在你写的程序不是你真正想要的 , 这意味着程序的意思\(即语义\)是错的 . 找到逻辑错误在哪需要十分清醒的头脑 , 因为要通过观察程序的输出而回过头来判断它到底在做什么.

也可以把编程和调试当成一回事 , 编程就是逐步调试直到获得期望结果为止的过程 . 



# 基本语法

#### Tokens

C程序由各种令牌组成 , 令牌可以是关键字 , 标识符 , 常量 , 字符串值或者是一个符号 .

例如 , 下面的 C 语句包括五个令牌 :

```
printf("Hello, World! \n");
```

五个Token分别为 :

```
printf
(
"Hello, World! \n"
)
;
```

**分号;**

在 C 程序中 , 分号是语句结束符 . 也就是说 , 每个语句必须以分号结束 . 它表明一个逻辑实体的结束 .

```
printf("Hello, World! \n");
return 0;
```

**注释**

注释就像是 C 程序中的帮助文本 , 它们会被编译器忽略 . 它们以`/*`开始 , 以字符`*/`终止 , 如下所示：

```
/* 我的第一个 C 程序 */
```

有的C代码中有类似`// comment`的注释 , 两个/斜线\(Slash\)表示从这里直到该行末尾的 所有字符都属于注释 , 这种注释不能跨行 , 也不能穿插在一行代码中间 . 这是从C++借鉴的语法 , 在C99中被标准化 .

**标识符**

C 标识符是用来标识变量、函数或任何其他用户自定义项目的名称 . 一个标识符以字母 A-Z 或 a-z 或下划线 \_ 开始 , 后跟零个或多个字母、下划线和数字\(0-9\) .

C 标识符内不允许出现标点字符 , 比如@、$ 和 % . C 是**区分大小写**的编程语言 . 因此 , 在 C 中 , Manpower和manpower是两个不同的标识符 . 下面列出几个有效的标识符 :

```
mohd       zara    abc   move_name  a_123
myname50   _temp   j     a23b9      retVal
```

**关键字**

下表列出了 C 中的保留字 . 这些保留字不能作为常量名、变量名或其他标识符名称 .

| auto | else | long | switch |
| :--- | :--- | :--- | :--- |
| break | enum | register | typedef |
| case | extern | return | union |
| char | float | short | unsigned |
| const | for | signed | void |
| continue | goto | sizeof | volatile |
| default | if | static | while |
| do | int | struct | \_Packed |
| double |  |  |  |

**C99新增关键字**

\_Bool    \_Complex    \_Imaginary    inline    restrict

**C11新增关键字**

\_Alignas    \_Alignof    \_Atomic    \_Generic    \_Noreturn

\_Static\_assert    \_Thread\_local

**C标准规定的转义字符**

| \' | 单引号'\(Single Quote,或Apostrophe\) |
| :--- | :--- |
| \" | 双引号" |
| \? | 问号?\(Question Mark\) |
| \\ | 反斜线\\(Backslash\) |
| \a | 响铃\(Alert,或Bell\) |
| \b | 退格\(Backspace\) |
| \f | 分页符\(Form Feed\) |
| \n | 换行\(Line Feed\) |
| \r | 回车\(Carriage Return\) |
| \t | 水平制表符\(Horizontal Tab\) |
| \v | 垂直制表符\(Vertical Tab\) |

双引号是字符串字面值的**界定符**\(Delimiter\) , 夹在双引号中间的一串字符才是它的内容 . 如果在字符串字面值中要表示单引号'和问号?,既可以使用转义序列\'和\?,也可以直接使用 . 

转义序列有两个作用 : 

* 把普通字符转义成特殊字符 , 例如换行\n
* 把特殊字符转义成普通字符 , 例如 ' 和 " 



**C 中的空格**

只包含空格的行 , 被称为空白行 , 可能带有注释 , C 编译器会完全忽略它 . 在 C 中 , 空格用于描述空白符、制表符、换行符和注释 . 空格分隔语句的各个部分 , 让编译器能识别语句中的某个元素\(比如 int\)在哪里结束 , 下一个元素在哪里开始 . 因此 , 在下面的语句中 :

```
int age;
```

在这里 , int 和 age 之间必须至少有一个空格字符\(通常是一个空白符\) , 这样编译器才能够区分它们 . 另一方面 , 在下面的语句中 :

```
fruit = apples + oranges;   // 获取水果的总数
```

fruit 和 = 或者 = 和 apples 之间的空格字符不是必需的 , 但是为了增强可读性 , 可以根据需要适当增加一些空格 .


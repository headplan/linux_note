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

注释就像是 C 程序中的帮助文本 , 它们会被编译器忽略 . 它们以` /* `开始 , 以字符` */ `终止 , 如下所示：

```
/* 我的第一个 C 程序 */
```

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




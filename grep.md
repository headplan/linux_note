# grep命令

grep - global search regular expression\(RE\) and print out the line

全面搜索正则表达式匹配的并把行打印出来.

文本搜索工具

### 常见用法

在文件中搜索一个单词,没有返回代表没搜索到

> grep "match\_pattern" file\_name \# 搜索文件中文本,输出当前行
> 
> grep "match\_pattern" file\_1 file\_2 \# 多文件搜索
> 
> grep -v "match\_pattern" file\_name \# -v表示输出除此之外其他内容,除了那一行,没搜到会全部输出
> 
> grep "match\_pattern" file\_name --color=auto \# --color=auto标记匹配颜色
> 
> grep -E "\[1-9\]+" file\_name \# -E使用正则表达式
> 
> echo this is a test line. \| grep -o -E "\[a-z\]+\." \# -o只输出文件中匹配到的部分


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
> echo this is a test line. \| grep -o -E "\[a-z\]+." \# -o只输出文件中匹配到的部分
> 
> echo this is a test line. \| egrep -o "\[a-z\]+." \# 同上
> 
> grep -c "match\_pattern" file\_name \# -c统计匹配行数,int数,记忆:count
> 
> grep "match\_pattern" -n file\_name \# -n返回匹配行内容+该行的行号,记忆:number
> 
> cat file\_name \| grep "match\_pattern" -n \# 同上
> 
> grep "match\_pattern" -n file\_1 file\_2 \# 多文件,同上
> 
> grep -b -o "match\_pattern" file\_name \# -b -o字节偏移没有显示==========
> 
> grep -l "match\_pattern" file\_1 file\_2 \# 返回匹配的多文件中的文件名

上面的都是指定文件名file\_name的.

### grep递归搜索文件

> grep "match\_pattern" .\/ -r -n \# -r -n多级目录中对文本进行递归搜索
> 
> echo "hello world" \| grep -i "HELLO" \# -i忽略大小写匹配
> 
> echo this is a text line \| grep -e "is" -e "line" \# -e搜索多个匹配内容
> 
> echo aaa bbb ccc ddd \| grep -f match -o \# 匹配多项,还可以创建一个文件,使用-f匹配
> 
> grep "main\(\)" . -r --include \*.{php,html} \# 递归搜索文件夹下匹配main\(\)的.php和.html文件
> 
> grep "main\(\)" . -r --exclude "README" \# 在搜索结果中排除README文件
> 
> grep "main\(\)" . -r --exclude-from filelist \# 同上,但是根据filelist文件里的列表排除
> 
> grep -q "match\_pattern" file\_name \# 静默输出,成功返回0,不成功返回其他.
> 
> seq 10 \| grep "5" -A 3 \# 匹配内容5,并显示后3行
> 
> seq 10 \| grep "5" -B 3 \# 匹配内容5,并显示前3行
> 
> seq 10 \| grep "5" -C 3 \# 匹配内容5,并显示前后3行




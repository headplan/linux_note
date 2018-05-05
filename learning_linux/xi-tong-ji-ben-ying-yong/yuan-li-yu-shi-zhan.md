# 原理与实战

举例

统计两个文件一共有多少个IP ?

```
cat ./file1 ./file2 | sort | uniq | wc -l
```

如何查看压缩包test.zip内 , 有没有包含test.so文件 ?

```
unzip -l test.zip | grep test.so | tail -c 9
```




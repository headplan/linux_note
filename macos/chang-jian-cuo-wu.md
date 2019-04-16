# 常见错误

#### Readline更新

```
dyld: Library not loaded: /usr/local/opt/readline/lib/libreadline.7.dylib 
Referenced from: /usr/local/bin/php 
Reason: image not found Abort trap: 6
```

```
$ brew link readline
$ brew link readline --force
# 如果还不能工作,运行
$ cd /usr/local/opt/readline/lib/
$ ln -s libreadline.dylib libreadline.7.dylib
```




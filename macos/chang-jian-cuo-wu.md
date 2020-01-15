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

> 原因 homebrew 将 libhistory 更新至8.0 . 而很多软件仍没有更新 . 或者是libreadline.7.dylib找不到 .

#### libjpeg更新

```
dyld: Library not loaded: /usr/local/opt/jpeg/lib/libjpeg.8.dylib
Referenced from: /usr/local/bin/php 
Reason: image not found Abort trap: 6
```

```
wget -c http://www.ijg.org/files/jpegsrc.v8d.tar.gz
```

其他步骤同上 . 


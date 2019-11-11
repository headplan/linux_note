# 文档显示图标和软件图标不一致

## 解决方案

[https://gist.github.com/fabiofl/5873100](https://link.jianshu.com?t=https%3A%2F%2Fgist.github.com%2Ffabiofl%2F5873100)

> **方式1：先用这个命令行 , 一般都能解决**  
> `sudo find /private/var/folders/ -name com.apple.dock.iconcache -exec rm {} \;`
>
> **方式2：如果不行 再用下面这个命令 并重启电脑**
>
> ```
> sudo find /private/var/folders/ -name com.apple.dock.iconcache -exec rm {} \;
> sudo find /private/var/folders/ -name com.apple.iconservices -exec rm -rf {} \;
> sudo mv /Library/Caches/com.apple.iconservices.store com.apple.ic
> ```
>
> ```
> 上面的命令就是在/private/var/folders/
> 搜索com.apple.dock.iconcache和com.apple.iconservices两个文件夹删掉
> 然后再删掉这个/Library/Caches/com.apple.iconservices.store(当然这里没有删除,而是重命名了)
> 然后就可以重建图标缓存
> ```






# /proc目录

_/proc/cmdline_ 加载 kernel 时所下达的相关参数，查阅此文件，可了解系统是如何启动。

_/proc/cpuinfo_ 本机的 CPU 的相关资讯，包含时脉、类型与运算功能等

_/proc/devices_这个文件记录了系统各个主要装置的主要装置代号，与 mknod 有关。

_/proc/filesystems_目前系统已经加载的文件系统。

_/proc/interrupts_目前系统上面的 IRQ 分配状态。

_/proc/ioports_ 目前系统上面各个装置所配置的 I/O 位址。

_/proc/kcore_ 这个就是内存的大小，但是不要读他。

_/proc/loadavg_ 还记得 top 以及 uptime 吧？没错，上头的三个平均数值就是记录在此。

_/proc/meminfo_ 使用 free 列出的内存资讯，在这里也能够查阅到。

_/proc/modules_ 目前我们的 Linux 已经加载的模块列表，也可以想成是驱动程序。

_/proc/mounts_系统已经挂载的数据，就是用 mount 这个命令呼叫出来的数据。

_/proc/swaps_ 到底系统挂加载的内存在哪里？使用掉的 partition 就记录在此啦。

_/proc/partitions_ 使用 fdisk -l 会出现目前所有的 partition 吧？在这个文件当中也有纪录。

_/proc/pci_ 在 PCI 汇流排上面，每个装置的详细情况，可用 lspci 来查阅。

_/proc/uptime_ 就是用 uptime 的时候，会出现的资讯。

_/proc/version_ 核心的版本，就是用 uname -a 显示的内容。

_/proc/bus/\*_ 一些汇流排的装置，还有 U盘 的装置也记录在此。


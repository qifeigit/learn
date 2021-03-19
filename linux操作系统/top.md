### cpu

- ##### user: 表示CPU执行用户进程的时间,通常期望用户空间CPU越高越好.

- ##### sys: 表示CPU在内核运行时间,系统CPU占用率高,表明系统某部分存在瓶颈.通常值越低越好.

- ##### wait: CPU在等待I/O操作完成所花费的时间.系统不应该花费大量时间来等待I/O操作,否则就说明I/O存在瓶颈.

- ##### hirq: 系统处理硬中断所花费的时间百分比

- ##### sirq: 系统处理软中断所花费的时间百分比

- ##### util: CPU总使用的时间百分比 `util = 1 - idle - iowait - steal`

- ##### nice: 系统调整进程优先级所花费的时间百分比

- ##### steal: 被强制等待（involuntary wait）虚拟CPU的时间,此时hypervisor在为另一个虚拟处理器服务

- ##### ncpu: CPU的总个数





### memory



- ##### free: 空闲的物理内存的大小

- ##### used: 已经使用的内存大小

- ##### buff: buff使用的内存大小,buffer is something that has yet to be "written" to disk.

- ##### cach: 操作系统会把经常访问的东西放在cache中加快执行速度,A cache is something that has been "read" from the disk and stored for later use

- ##### total: 系统总的内存大小

- ##### util: 内存使用率 `util = (total - free - buff - cache) / total * 100%`

  todoqifei 为什么不直接用used/total?

> ##### 采集方法 内存的计数器在/proc/meminfo,里面有一些关键项 含义就不解释了,主要介绍一下内存使用率的计算算法: `util = (total - free - buff - cache) / total * 100%`


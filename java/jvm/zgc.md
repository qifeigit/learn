## ZGC原理

### 全并发的ZGC

与CMS中的ParNew和G1类似，ZGC也采用标记-复制算法，不过ZGC对该算法做了重大改进：ZGC在标记、转移和重定位阶段几乎都是并发的，这是ZGC实现停顿时间小于10ms目标的最关键原因。



ZGC垃圾回收周期如下图所示：

![img](https://p0.meituan.net/travelcube/40838f01e4c29cfe5423171f08771ef8156393.png@1812w_940h_80q)

ZGC只有三个STW阶段：**初始标记**，**再标记**，**初始转移**。其中，初始标记和初始转移分别都只需要扫描所有GC Roots，其处理时间和GC Roots的数量成正比，一般情况耗时非常短；再标记阶段STW时间很短，最多1ms，超过1ms则再次进入并发标记阶段。即，ZGC几乎所有暂停都只依赖于GC Roots集合大小，停顿时间不会随着堆的大小或者活跃对象的大小而增加。与ZGC对比，G1的转移阶段完全STW的，且停顿时间随存活对象的大小增加而增加。





remapped mo m1 3个占用的空间是相等的吗？

如果是相等，那么可利用得堆空间岂不是只有1/3







[美团ZGC](https://tech.meituan.com/2020/08/06/new-zgc-practice-in-meituan.html)

https://developer.aliyun.com/article/726120
## 是什么

分布式的数据管理中心

满足 cp性

基于paxos 协议，实现了zab协议

https://zhuanlan.zhihu.com/p/44207241



### ZooKeeper 集群为啥最好奇数台？

ZooKeeper 集群在宕掉几个 ZooKeeper 服务器之后，如果剩下的 ZooKeeper 服务器个数大于宕掉的个数的话整个 ZooKeeper 才依然可用。假如我们的集群中有 n 台 ZooKeeper 服务器，那么也就是剩下的服务数必须大于 n/2。先说一下结论，2n 和 2n-1 的容忍度是一样的，都是 n-1，大家可以先自己仔细想一想，这应该是一个很简单的数学问题了。 比如假如我们有 3 台，那么最大允许宕掉 1 台 ZooKeeper 服务器，如果我们有 4 台的的时候也同样只允许宕掉 1 台。 假如我们有 5 台，那么最大允许宕掉 2 台 ZooKeeper 服务器，如果我们有 6 台的的时候也同样只允许宕掉 2 台。

综上，何必增加那一个不必要的 ZooKeeper 呢？





## zab

Zookeeper Atomic Broadcast

ZAB协议定义了选举（election）、发现（discovery）、同步（sync）、广播(Broadcast)四个阶段。

选举（election）是选出哪台为主机；
发现（discovery）、同步（sync）当主选出后，要做的恢复数据的阶段；

广播(Broadcast)当主机和从选出并同步好数据后，正常的主写同步从写数据的阶段。

## fast paxos










## 遇到的问题





refer

[实例详解ZooKeeper ZAB协议、分布式锁与领导选举](https://dbaplus.cn/news-141-1875-1.html)
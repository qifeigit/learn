## 是什么

分布式的数据管理中心

满足 cp性

基于paxos 协议，实现了zab协议

https://zhuanlan.zhihu.com/p/44207241

## zab

Zookeeper Atomic Broadcast

ZAB协议定义了选举（election）、发现（discovery）、同步（sync）、广播(Broadcast)四个阶段。

选举（election）是选出哪台为主机；
发现（discovery）、同步（sync）当主选出后，要做的恢复数据的阶段；

广播(Broadcast)当主机和从选出并同步好数据后，正常的主写同步从写数据的阶段。

## fast paxos










## 遇到的问题


## todo
slot怎么迁移
怎么实现自动化的扩容，缩容
缓存和数据库不一致


![Alt text](./img/cluster1.png)



配置
cluster-enabled yes

如果开启集群配置，但没有配置详细信息，那么会提示
hash slot not served

## 搭建步骤

redis-cil --cluster create host:port --cluster-replicas 1

最少3个master 节点



# slot的算法

crc16，或者自己指定

slot怎么迁移


## 扩容


## 缩容

先迁移slot




## 命令 
cluster nodes 查看节点信息

cluster add-node  增加节点

cluster reshared  重新分配slot










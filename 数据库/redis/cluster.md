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



### 重新分片

将slot切换节点




## 扩容







## 缩容

先迁移slot




## 命令 
cluster info 查看集群信息

cluster nodes 查看节点信息

cluster add-node  增加节点

cluster reshared  重新分配slot





### 客户端

当以单机运行时候,如果当前的slot不由该节点负责则返回MOVED错误

```redis
set t "222"
(error) MOVED 15891 172.20.0.6:6379
```





#### ask错误

如果节点A正在迁移slot 到节点B，那么节点A没能在自己的数据库中找到对应的key时候，节点A会向客户端返回一个ask错误



### 故障检测

节点定期的向集群中其他节点发送ping消息，来检测对方是否下线


#  sentinel

哨兵：在复制的基础上，哨兵实现了自动化的故障恢复。缺陷：写操作无法负载均衡；存储能力受到单机的限制。

This is the full list of Sentinel capabilities at a macroscopical level (i.e. the *big picture*): 

- **Monitoring**. Sentinel constantly checks if your master and replica instances are working as expected.
- **Notification**. Sentinel can notify the system administrator, or other computer programs, via an API, that something is wrong with one of the monitored Redis instances.
- **Automatic failover**. If a master is not working as expected, Sentinel can start a failover process where a replica is promoted to master, the other additional replicas are reconfigured to use the new master, and the applications using the Redis server are informed about the new address to use when connecting.
- **Configuration provider**. Sentinel acts as a source of authority for clients service discovery: clients connect to Sentinels in order to ask for the address of the current Redis master responsible for a given service. If a failover occurs, Sentinels will report the new address.







1. **Sentinel, Docker, or other forms of Network Address Translation or Port Mapping should be mixed with care**: Docker performs port remapping, breaking Sentinel auto discovery of other Sentinel processes and the list of replicas for a master. Check the section about Sentinel and Docker later in this document for more information.

  什么意思呢？



# [深入学习Redis（4）：哨兵](https://www.cnblogs.com/kismetv/p/9609938.html)



[Redis Sentinel Documentation](https://redis.io/topics/sentinel)







sentinel 会挑选一个从服务器变成主服务器，那么挑选规则是什么

好像这个问题并不是很重要





选举领头的sentinel

干嘛不直接选出leader呢，非得等到要发命令的时候再选呢

也许是因为leader的状态无法完全保持住，有可能会重新选举leader








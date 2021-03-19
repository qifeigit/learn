### CORE CAPABILITIES

- #### HIGH THROUGHPUT

  Deliver messages at network limited throughput using a cluster of machines with latencies as low as 2ms.

- #### SCALABLE

  Scale production clusters up to a thousand brokers, trillions of messages per day, petabytes of data, hundreds of thousands of partitions. Elastically expand and contract storage and processing.

  #### PERMANENT STORAGE

  Store streams of data safely in a distributed, durable, fault-tolerant cluster.

- #### HIGH AVAILABILITY

  Stretch clusters efficiently over availability zones or connect separate clusters across geographic regions.





## 组成

- Broker：消息中间件处理结点，一个Kafka节点就是一个broker，多个broker可以组成一个Kafka集群。
- Topic：一类消息，例如page view日志、click日志等都可以以topic的形式存在，Kafka集群能够同时负责多个topic的分发。
- Partition：topic物理上的分组，一个topic可以分为多个partition，每个partition是一个有序的队列。
- Segment：partition物理上由多个segment组成，下面有详细说明。
- offset：每个partition都由一系列有序的、不可变的消息组成，这些消息被连续的追加到partition中。partition中的每个消息都有一个连续的序列号叫做offset,用于partition唯一标识一条消息.每个partition中的消息都由offset=0开始记录消息。
- zookeeper集群，负责选举，元数据存储，之前也保存offset，后来kafka自己保存



## ISR机制：

1. leader会维护一个与其基本保持同步的Replica列表，该列表称为ISR(in-sync Replica)，每个Partition都会有一个ISR，而且是由leader动态维护

2. 如果一个follower比一个leader落后太多，或者超过一定时间未发起数据复制请求，则leader将其重ISR中移除

3. 当ISR中所有Replica都向Leader发送ACK时，leader才commit，这时候producer才能认为一个请求中的消息都commit了。



我们设置 replica.lag.max.messages 为4，只要 follower 只要不落后leader 大于3条消息，就然后是跟得上leader的节点，就不会被踢出去， 设置 replica.lag.time.max.ms 为 500ms， 意味着只要 follower 在每 500ms内发送fetch请求，就不会被认为已经dead ，不会从ISR集合中踢出去。









## partition

分区内是有序的



## 读确认

消费者确保消费后再提交消费操作



## 写确认

生产者确保写入后再提交消费操作





## 高性能

零拷贝

顺序写磁盘





at least once

将producer的ack级别设置为-1



at most once

将producer的ack级别设置为0



## 只写一次

at least once + 幂等性 = exactly once

id是根据producer的id和消息的唯一键去做区分

producer重启的话，会生成新的pid



todoqifei





## 能被多个消费者读么

可以





https://www.confluent.io/blog/exactly-once-semantics-are-possible-heres-how-apache-kafka-does-it/
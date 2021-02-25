## 日志
binlog 
mysql层面的，用于主从复制，数据恢复

redolog
Innodb引擎，记录的是数据修改之后的值，不管事务是否提交都会记录下来。

undolog


Innodb引擎，保存了事务发生之前的数据的一个版本，可以用于回滚



采用mvcc，默认为repeatable read，通过间隙锁防止幻读出现



索引为聚簇索引





## 分区

hash分区，范围分区

按天分区的话，创建定时任务去创建新的分区，并且删除新的分区

和用户有关的表可以按照userid进行分区





## 行锁的实现

InnoDB行锁是通过给索引上的索引项加锁来实现的。*`InnoDB这种行锁实现特点意味着：只有通过索引条件检索数据，InnoDB才使用行级锁，否则，InnoDB将使用表锁！`*

todoqifei

### 死锁

InnoDB 引擎采取的是 `wait-for graph` 等待图的方法来自动检测死锁，如果发现死锁会自动回滚一个事务。

wait-for graph要求数据库保存两种信息

锁的信息链表

事务等待链表

通过上面链表构造出一张图，图中若存在回路，就代表存在死锁，资源间发生相互等待。

## 语句

**set autocommit=0,**

当前session禁用自动提交事物，自此句执行以后，每个SQL语句或者语句块所在的事务都需要显示"commit"才能提交事务。







### 特点

插入缓冲(insert buffer)

二次写(double write)

自适应哈希索引(adaptive hash index)

预读(read ahead)
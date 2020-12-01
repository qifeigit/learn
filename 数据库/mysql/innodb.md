## 日志
binlog 
mysql层面的，用于主从复制，数据恢复

redolog
Innodb引擎，记录的是数据修改之后的值，不管事务是否提交都会记录下来。

undolog


Innodb引擎，保存了事务发生之前的数据的一个版本，可以用于回滚



采用mvcc，默认为repeatable read，通过间隙锁防止幻读出现



索引为聚簇索引


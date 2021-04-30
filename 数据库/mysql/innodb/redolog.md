| redolog        | binlog      |
| -------------- | ----------- |
| innodb独有的   | mysql层面的 |
| 更改的物理情况 | 逻辑层面    |







步骤12执行完毕之后，mysql宕机了

> 此时redo log prepare过程是写入redo log文件了，但是binlog写入失败了，此时mysql重启之后会读取redo log进行恢复处理，查询到trx_id=10的记录是prepare状态，会去binlog中查找trx_id=10的操作在binlog中是否存在，如果不存在，说明binlog写入失败了，此时可以将此操作回滚
>
> todoqifei
>
> 此处的操作回滚是指什么呢？
## 功能
实现了多个容器的编排



方便部署调试



## 语法



```
docker run -d --name kafka -p 9092:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 --link zookeeper1 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://http://192.168.49.1:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka
```



## 问题

怎么只启动一个容器，现在运行命令会启动多个



在yaml编辑过程中可能会出现格式问题

[yaml 编辑器](https://codebeautify.org/yaml-validator)
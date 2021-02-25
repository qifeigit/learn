## 功能
实现了多个容器的编排

**编排(orchestration)**
编排指根据被部署的对象之间的耦合关系，以及被部署对象对环境的依赖，制定部署流程中各个动作的执行顺序，部署过程所需要的依赖文件和被部署文件的存储位置和获取方式，以及如何验证部署成功





方便部署调试



## 语法



```
docker run -d --name kafka -p 9092:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 --link zookeeper1 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://http://192.168.49.1:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka
```





docker-compose 学习

[Docker Compose 学习](https://www.cnblogs.com/sparkdev/p/9826520.html)

## 问题

怎么只启动一个容器，现在运行命令会启动多个



在yaml编辑过程中可能会出现格式问题

[yaml 编辑器](https://codebeautify.org/yaml-validator)


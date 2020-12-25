在目录下创建一个新文件:docker-compose-kafka-single-broker.yml，配置内容如下：

```dockerfile
version: '3'
services:
  zookeeper:
    image: wurstmeister/zookeeper
    container_name: zookeeper
    ports:
      - "2181:2181"

  kafka1:
    image: wurstmeister/kafka
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: 192.168.1.202
      KAFKA_CREATE_TOPICS: TestComposeTopic:4:3
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_BROKER_ID: 1
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://192.168.1.202:9092
      KAFKA_LISTENERS: PLAINTEXT://0.0.0.0:9092
    container_name: kafka01
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock

  kafka2:
    image: wurstmeister/kafka
    ports:
      - "9093:9093"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: 192.168.1.202
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_BROKER_ID: 2
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://192.168.1.202:9093
      KAFKA_LISTENERS: PLAINTEXT://0.0.0.0:9093
    container_name: kafka02
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock

  kafka3:
    image: wurstmeister/kafka
    ports:
      - "9094:9094"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: 192.168.1.202
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_BROKER_ID: 3
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://192.168.1.202:9094
      KAFKA_LISTENERS: PLAINTEXT://0.0.0.0:9094
    container_name: kafka03
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock

```

docker-compose -f docker-compose-kafka-cluster.yml up
```shell
$ curl -sSL https://raw.githubusercontent.com/bitnami/bitnami-docker-redis-cluster/master/docker-compose.yml > docker-compose.yml
$ docker-compose up -d  #后台启动并运行所有容器
```





```dockerfile
version: '3'
services:
    redis:
      image: redis:5.0.0
      container_name: redis
      command: redis-server --requirepass 123456
      ports:
        - "6379:6379"
      volumes:
        - ./data:/data
```




```dockerfile
version: '3'
services:
      mongodb:
        image: mongo:4.2.6 # 镜像:版本
        network_mode: host
        container_name: mongo_db
        environment:
          - MONGO_INITDB_DATABASE=admin
          - MONGO_INITDB_ROOT_USERNAME=root
          - MONGO_INITDB_ROOT_PASSWORD=123456
        volumes:
          - ./mongo/mongo-volume:/data/db
        ports:
          - "27017-27019:27017-27019"
```



```
db.createUser({user:"tes1t",pwd:"123456",roles:[{role:'readAnyDatabase',db:'admin'}]})
```

```js
 db.createUser({
    user: 'test',
    pwd: '123456',
    roles: [{ role: 'readWrite', db:'recommender'}]
})
```
[菜鸟教程-单机版本](https://www.runoob.com/docker/docker-install-mysql.html)

```shell
#启动
docker run --name mysql -h 0.0.0.0 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql

#进入容器
docker exec -it mysql bash

#登录mysql
mysql -u root -p
ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';

#添加远程登录用户
CREATE USER 'liaozesong'@'%' IDENTIFIED WITH mysql_native_password BY 'Lzslov123!';
GRANT ALL PRIVILEGES ON *.* TO 'liaozesong'@'%';
```



遇到的实际问题：
jdbc无法连接mysql，原因是因为编辑了idea的文件，修改了密码。但运行时候依然走得旧的文件内容，导致出现了问题



主机访问容器无法访问,但好像有问题

```shell
sudo docker run --name=mysql -it -p 3306:3306 -v /opt/data/mysql/mysqld:/var/run/mysqld -v /opt/data/mysql/db:/var/lib/mysql -v /opt/data/mysql/conf:/etc/mysql/conf.d -v /opt/data/mysql/files:/var/lib/mysql-files -e MYSQL_ROOT_PASSWORD=123456 --privileged=true -d mysql
```



ref

https://blog.csdn.net/zzddada/article/details/94742832
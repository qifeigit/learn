# docker compose 搭建 gitlab



## docker-compose.yml

```yaml
version: '3.6'
services:
  web:
  //ce为社区版，ee为企业版
    image: 'gitlab/gitlab-ce:latest'
    //是否重启
    restart: always
    hostname: 'gitlab.example.com'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://gitlab.example.com:8929'
        gitlab_rails['gitlab_shell_ssh_port'] = 2224
    ports:
    //web页面端口
      - '8929:8929'
     //实际git的端口 
      - '2224:22'
    volumes:
      - 'E:\docker\gitlab\config:/etc/gitlab'
      - 'E:\docker\gitlab\logs:/var/log/gitlab'
      - 'E:\docker\gitlab\data:/var/opt/gitlab'
    shm_size: '256m'
```





## 运行命令

docker-compose up -d

## 修改初始密码即可

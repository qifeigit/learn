sentry入门

简介

sentry 是一个开源的实时错误追踪系统,可以帮助开发者实时监控并修复异常问题。它主要专注于持续集成、提高效率并且提升用户体验。由python编写，底层为django。

背景

当生产系统中产生了一个bug时，我们如何快速地得到报警？如何快速地找到问题的根源？当hotfix完修复程序后，又如何知道它是否解决了问题？

结构和原理

可以理解为C/S结构，client 需要嵌入到我们的项目代码中，server 需要我们自行搭建。client 可以将我们需要的异常和错误信息发送到server，server 将消息记录到数据库中并提供一个web界面方便查看。

server安装

环境准备 

- Docker 19.03.6+
- Compose 1.24.1+
- python3

参考https://github.com/getsentry/onpremise 进行sentry 安装

```
Would you like to create a user account now? [Y/n]: y
Email: tuqifei111@126.com
Password: 
Repeat for confirmation: 
User created: tuqifei111@126.com
```

在此过程中，需要注册用户名，密码

安装完成后启动

```
docker-compose up -d
```

浏览器输入 [localhost:9000](http://localhost:9000) 访问,输入账号，密码，进入初始化界面

*|*![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=63b82feeee9589c4a6a8fd0167f875de_8f118824ce50c961_boxk4Y3uGKuXc1xBDWh3wdVomDh_SogvrvhT90okAvn2SZsA5xm47M3EPkkc)

点击 projects ->  create projects 

选择 java ，修改project 名称，创建新project，会看到 client 安装指导

*|*![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=bbe5fccc077c1e46b2c886367125a798_8f118824ce50c961_boxk42to87jxqD7hpf78oiAI69b_SwdDz2EcaCxq5lHQCAKwMyMcmOy3zsd3)

client嵌入

按照 client 安装指导进行 操作 并 执行后

*|*![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=ddff04da2914eea9e085ffe312b12464_8f118824ce50c961_boxk4AK5SkMDDEjBiex4Rz2NeHd_RT3JblmepZ6wXrYp87Jsur6oAClKoqig)



demo地址

http://localhost:9000/organizations/sentry/issues/





上报方式

走http或者https



资料引用

[Vue+Docker+Sentry 极速搭建前端异常监控系统 ](https://www.bilibili.com/video/BV1UZ4y1p7MF?from=search&seid=16033700262510061469) 

[业务日志监控工具Sentry介绍](https://zhuanlan.zhihu.com/p/42941286)

[sentry官方文档](https://docs.sentry.io/platforms/java/)
sentry进阶

操作界面介绍

概念

DSN（data source name）

Sentry 服务支持多用户、多团队、多应用管理，每个应用都对应一个 DSN

event

每当项目产生一个错误，sentry服务端日志就会产生一个event，记录此次报错的具体信息。一个错误，对应一个event。

issue

同一类event的集合，一个错误可能会重复产生多次，sentry服务端会将这些错误聚集在一起，那么这个集合就是一个issue。

breadcrumb

记录问题的上下文,能够向前回溯

整体架构

![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=6dd7b7ef6dec5b5e93f619621f0e0fea_8f118824ce50c961_boxk4NULryy60E4fGnpVFf8mytU_Ojgz9nd9w0BsMZyXpWABOH4Av2L475KL)

与现有框架整合

log4j

spring-boot

初始化参数

　　DSN ：项目的地址，用于收集错误信息的 sentry 分配的地址

　　debug ：是否开启 debug 模式，开启debug，就会把信息打印到控制台上面

　　release 版本号，可以确定当前的错误/异常属于哪一个发布的版本

　　environment : 环境名称

　　sampleRate : 是否开启随机发送事件给 sentry ，1为100%，0.1 为 10%几率发送事件

　　beforeSend : 发送前操作

告警的使用

支持邮件告警

第三方集成

http://localhost:9000/settings/sentry/integrations/



生产环境部署

client

引入依赖

```
<dependency>
 <groupId>io.sentry</groupId>
 <artifactId>sentry-log4j2</artifactId>
 <version>${sentry.version}</version>
</dependency>
```

对sentry做配置

service

容器化部署

docker-composed , k8s

用现有的组件

  \- redis

  \- postgres

  \- memcached

  \- kafka

  -sentry web
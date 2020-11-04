nginx

大纲

1. Nginx简介及特点
2. Nginx应用场景
3. Nginx框架模型介绍
4. 反向代理
5. 日常配置
6. 配置301，302

 Nginx简介

**Nginx简介:**

Nginx 是一个高性能的web服务器和反向代理服务器

**Nginx特点：**

- 反向代理，负载均衡
- 高可靠性、单master多worker模式
- 高可扩展性、高度模块化
- 非阻塞，事件驱动
- 低内存消耗
- 热部署

**场景**

- 静态文件服务器
- 反向代理，负载均衡
- 安全防御
- 灰度发布
- 压缩
- 防盗链

**框架模型**

*|*![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=06ba57aaf9224af630136b01a3a0c48b_8f118824ce50c961_boxk4KlnhujPpYBp2VI5exTsE51_5t5qS1Ryj0tB0GQa6laQnKKXLckqSpa1)

*|*![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=ca426d4876d1b0846e487125c96d7cee_8f118824ce50c961_boxk4Y7jmfnx9OCEH0iWb9sz2Pc_MPJOWTX2OvswMBFeAPzszXVurtLHTrgx)

反向代理

什么是反向代理？ 互联网应用基本都基于CS基本结构，即client端和server端。代理其实就是在client端和真正的server端之前增加一层提供特定服务的服务器，即代理服务器。

**正向代理** 反向代理不好理解，**正向代理**大家总有用过，翻墙工具其实就是一个正向代理工具。它会把 们访问墙外服务器server的网页请求，代理到一个可以访问该网站的代理服务器proxy，这个代理服务器proxy把墙外服务器server上的网页内容获取，再转发给客户。具体的流程如下图。

*|*![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=f701bee2b134742adef58a3540ec79be_8f118824ce50c961_boxk4ixU6FuIStMZWtvMl4KpYLf_YPxZWUXsGBYfjTmwOqDcCtsmyXqxn944)

**反向代理** **反向代理**则正好相反，先看流程图

*|*![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=a17bbce129af797c3ff3d5888d514743_8f118824ce50c961_boxk4UeMLvAo58gwbD4EOtb9Bod_LhWPuo0zemQvCh5jtYs3EgIyGGfX1rCt)

代理服务器和真正server服务器可以直接互相访问，属于一个LAN（服务器内网）；代理对用户是**透明**的，即无感知。不论加不加这个反向代理，用户都是通过相同的请求进行的，且不需要任何额外的操作；代理服务器通过**代理内部服务器**接受域外客户端的请求，并将请求发送到对应的内部服务器上。

两个原因： 

安全及权限

负载均衡

日常配置

**快速实现简单的访问限制**

经常会遇到希望网站让某些特定用户的群体（比如只让公司内网）访问，或者控制某个uri不让人访问。Nginx配置如下：

```
location / {
  deny  192.168.1.100;
  allow 192.168.1.10/200;
  allow 10.110.50.16;
  deny  all;
}
```

**解决跨域**

本地程序直接访问远程接口 [www.realApi.com](http://www.realApi.com)， 会遇到跨域问题。为了绕开浏览器的跨域安全限制，现在需要将请求的域名改成[nginxApi.com](http://nginxApi.com)。同时约定一个url规则来表明代理请求的身份，然后Nginx通过匹配该规则，将请求代理回原来的域

```
#请求跨域，这里约定代理请求url path是以/apis/开头
location ^~/apis/ {
  # 这里重写了请求，将正则匹配中的第一个()中$1的path，拼接到真正的请求后面，并用break停止后续匹配
  rewrite ^/apis/(.*)$ /$1 break;
  proxy_pass https://www.realApi.com/;
}  
```

**合并请求**

性能优化中重要一点就是尽量减少http资源请求的数量,通过[nginx-http-concat](https://github.com/alibaba/nginx-http-concat)模块（淘宝开发的第三方模块，需要单独安装）用一种特殊的请求url规则（例子：[example.com/??1.js,2.js,3.js](http://example.com/??1.js,2.js,3.js) ），前端可以将多个资源的请求合并成一个请求，后台Nginx会获取各个资源并拼接成一个结果进行返回。

```
location / {
  concat on;
  concat_max_files 20;
}
```

灰度发布

```
upstream normal {
  server 127.0.0.1:8080;
}
upstream dark {
  server 127.0.0.1:8081;
}
**server** {
  listen    80;
  server_name  localhost;
  set $group normal;
  *#或者使用 if ($cookie_dark ~\* "^true&") 来判断*
  if ($http_cookie ~* "dark=true"){ 
    set $group dark;
  }
  
  location / {
    proxy_pass http://$group;
  }
}
```

配置301，302

rewrite:

redirect – 返回临时重定向的HTTP状态302

permanent – 返回永久重定向的HTTP状态301

301跳转设置：

```
nginx

大纲
1. Nginx简介及特点
2. Nginx应用场景
3. Nginx框架模型介绍
4. 反向代理
5. 日常配置
6. 配置301，302



 Nginx简介

Nginx简介:
Nginx 是一个高性能的web服务器和反向代理服务器

Nginx特点：
- 反向代理，负载均衡
- 高可靠性、单master多worker模式
- 高可扩展性、高度模块化
- 非阻塞，事件驱动
- 低内存消耗
- 热部署


场景
- 静态文件服务器
- 反向代理，负载均衡
- 安全防御
- 灰度发布
- 压缩
- 防盗链


框架模型

|

|




反向代理
什么是反向代理？ 互联网应用基本都基于CS基本结构，即client端和server端。代理其实就是在client端和真正的server端之前增加一层提供特定服务的服务器，即代理服务器。

正向代理 反向代理不好理解，正向代理大家总有用过，翻墙工具其实就是一个正向代理工具。它会把 们访问墙外服务器server的网页请求，代理到一个可以访问该网站的代理服务器proxy，这个代理服务器proxy把墙外服务器server上的网页内容获取，再转发给客户。具体的流程如下图。
|



反向代理 反向代理则正好相反，先看流程图
|

代理服务器和真正server服务器可以直接互相访问，属于一个LAN（服务器内网）；代理对用户是透明的，即无感知。不论加不加这个反向代理，用户都是通过相同的请求进行的，且不需要任何额外的操作；代理服务器通过代理内部服务器接受域外客户端的请求，并将请求发送到对应的内部服务器上。

两个原因： 
安全及权限
负载均衡


日常配置

快速实现简单的访问限制

经常会遇到希望网站让某些特定用户的群体（比如只让公司内网）访问，或者控制某个uri不让人访问。Nginx配置如下：
location / {
    deny  192.168.1.100;
    allow 192.168.1.10/200;
    allow 10.110.50.16;
    deny  all;
}

解决跨域

本地程序直接访问远程接口 www.realApi.com， 会遇到跨域问题。为了绕开浏览器的跨域安全限制，现在需要将请求的域名改成nginxApi.com。同时约定一个url规则来表明代理请求的身份，然后Nginx通过匹配该规则，将请求代理回原来的域

#请求跨域，这里约定代理请求url path是以/apis/开头
location ^~/apis/ {
    # 这里重写了请求，将正则匹配中的第一个()中$1的path，拼接到真正的请求后面，并用break停止后续匹配
    rewrite ^/apis/(.*)$ /$1 break;
    proxy_pass https://www.realApi.com/;
}  



合并请求

性能优化中重要一点就是尽量减少http资源请求的数量,通过nginx-http-concat模块（淘宝开发的第三方模块，需要单独安装）用一种特殊的请求url规则（例子：example.com/??1.js,2.js,3.js ），前端可以将多个资源的请求合并成一个请求，后台Nginx会获取各个资源并拼接成一个结果进行返回。

location / {
    concat on;
    concat_max_files 20;
}


灰度发布
upstream normal {
    server 127.0.0.1:8080;
}
upstream dark {
    server 127.0.0.1:8081;
}
server {
    listen       80;
    server_name  localhost;

    set $group normal;
    #或者使用 if ($cookie_dark ~* "^true&") 来判断
    if ($http_cookie ~* "dark=true"){ 
        set $group dark;
    }
    
    location / {
        proxy_pass http://$group;
    }
}




配置301，302

rewrite:
redirect – 返回临时重定向的HTTP状态302
permanent – 返回永久重定向的HTTP状态301


301跳转设置：
server {
listen 80;
server_name 123.com;
rewrite ^/(.*) http://456.com/$1 permanent;
access_log off;
}




302跳转设置：
server {
listen 80;
server_name 123.com;
rewrite ^/(.*) http://456.com/$1 redirect;
access_log off;
}

server {
listen 80;
server_name 123.com;
rewrite ^/(.*) http://456.com/$1 permanent;
access_log off;
}
```

302跳转设置：

```
server {
listen 80;
server_name 123.com;
rewrite ^/(.*) http://456.com/$1 redirect;
access_log off;
}
```
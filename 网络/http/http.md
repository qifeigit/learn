### http code

- `200 OK` 客户端请求成功
- 206 这种响应是在客户端表明自己只需要目标URL上的部分资源的时候返回的
- `301 Moved Permanently` 请求永久重定向
- `302 Moved Temporarily` 请求临时重定向
- `304 Not Modified` 文件未修改，可以直接使用缓存的文件。
- `400 Bad Request` 由于客户端请求有语法错误，不能被服务器所理解。
- `401 Unauthorized` 请求未经授权。这个状态代码必须和WWW-Authenticate报头域一起使用
- `403 Forbidden` 服务器收到请求，但是拒绝提供服务。服务器通常会在响应正文中给出不提供服务的原因
- `404 Not Found` 请求的资源不存在，例如，输入了错误的URL
- 499  客户端主动断掉连接之后，Nginx 会等待后端服务器处理完(或者*超时*)
- `500 Internal Server Error` 服务器发生不可预期的错误，导致无法完成客户端的请求。
- `503 Service Unavailable` 服务器当前不能够处理客户端的请求，在一段时间之后，服务器可能会恢复正常。





Http1.1 新增内容

**持续连接**

Cache缓存

**增加host字段**









[HTTP的前世今生](https://coolshell.cn/articles/19840.html)


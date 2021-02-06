## 走进HTTP/3

这就是HTTP/3的用武之处：它不使用TCP作为会话的传输层，而是使用[QUIC（一种新的Internet传输协议）](https://blog.cloudflare.com/the-road-to-quic/)，该协议将流作为传输层的一级公民引入



![img](https://blog.cloudflare.com/content/images/2020/01/http-request-over-quic@2x.png)





出现的原因：

然而，这个世界没有完美的解决方案，HTTP/2也不例外，其主要的问题是：若干个HTTP的请求在复用一个TCP的连接，底层的TCP协议是不知道上层有多少个HTTP的请求的，所以，一旦发生丢包，造成的问题就是所有的HTTP请求都必需等待这个丢了的包被重传回来，哪怕丢的那个包不是我这个HTTP请求的。因为TCP底层是没有这个知识了。
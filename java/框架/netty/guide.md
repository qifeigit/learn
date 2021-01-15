

```java
   EventLoopGroup bossGroup = new NioEventLoopGroup(); // (1)
        EventLoopGroup workerGroup = new NioEventLoopGroup();
        try {
            ServerBootstrap b = new ServerBootstrap(); // (2)
            b.group(bossGroup, workerGroup)
             .channel(NioServerSocketChannel.class) // (3)
             .childHandler(new ChannelInitializer<SocketChannel>() { // (4)
                 @Override
                 public void initChannel(SocketChannel ch) throws Exception {
                	 
                	 // 添加ChannelHandler到ChannelPipeline
                     ch.pipeline().addLast(new DiscardServerHandler());
                 }
             })
             .option(ChannelOption.SO_BACKLOG, 128)          // (5)
             .childOption(ChannelOption.SO_KEEPALIVE, true); // (6)

            // 绑定端口，开始接收进来的连接
            ChannelFuture f = b.bind(port).sync(); // (7)

            System.out.println("DiscardServer已启动，端口：" + port);
            
            // 等待服务器  socket 关闭 。
            // 在这个例子中，这不会发生，但你可以优雅地关闭你的服务器。
            f.channel().closeFuture().sync();
        } finally {
            workerGroup.shutdownGracefully();
            bossGroup.shutdownGracefully();
        }
```



1. [`NioEventLoopGroup`](https://netty.io/4.1/api/io/netty/channel/nio/NioEventLoopGroup.html) is a multithreaded event loop that handles I/O operation
2. [`ServerBootstrap`](https://netty.io/4.1/api/io/netty/bootstrap/ServerBootstrap.html) is a helper class that sets up a server. 
3.  we specify to use the [`NioServerSocketChannel`](https://netty.io/4.1/api/io/netty/channel/socket/nio/NioServerSocketChannel.html) class which is used to instantiate a new [`Channel`](https://netty.io/4.1/api/io/netty/channel/Channel.html) to accept incoming connections.
4. The handler specified here will always be evaluated by a newly accepted [`Channel`](https://netty.io/4.1/api/io/netty/channel/Channel.html).

refer

https://netty.io/wiki/user-guide-for-4.x.html
Servlet 本质上是一个接口，实现了 Servlet 接口的业务类也叫 Servlet。Servlet 接口其实是 Servlet 容器跟具体 Servlet 业务类之间的接口。Servlet 接口跟 Servlet 容器这一整套规范叫作 Servlet 规范，而 Servlet 规范使得程序员可以专注业务逻辑的开发，同时 Servlet 规范也给开发者提供了扩展的机制 Filter 和Listener

最后我给你总结一下 Filter 和 Listener 的本质区别:

不Filter 是干预过程的，它是过程的一部分，是基于过程行为的。Listener 是基于状态的，任何行为改变同一个状态，触发的事件是一致的。
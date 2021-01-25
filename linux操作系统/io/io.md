



五种IO模型包括：**阻塞IO、非阻塞IO、IO多路复用、信号驱动IO、异步IO**。

## 阻塞IO模型

![img](https://pic1.zhimg.com/80/v2-dd90b4423d0220a45f66c2880308f464_1440w.jpg)

## **非阻塞IO模型**

## ![img](https://pic1.zhimg.com/80/v2-28c4499246deda788090a027672bb5c4_1440w.jpg)

## IO多路复用模型



![img](https://pic4.zhimg.com/80/v2-22c97570f76d0e6974647bb328c6d17f_1440w.jpg)



## select/poll/epoll之间的区别

|            | select             | poll             | epoll                                             |
| :--------- | :----------------- | :--------------- | :------------------------------------------------ |
| 数据结构   | bitmap             | 数组             | 红黑树                                            |
| 最大连接数 | 1024               | 无上限           | 无上限                                            |
| fd拷贝     | 每次调用select拷贝 | 每次调用poll拷贝 | fd首次调用epoll_ctl拷贝，每次调用epoll_wait不拷贝 |
| 工作效率   | 轮询：O(n)         | 轮询：O(n)       | 回调：O(1)                                        |




## 信号驱动IO模型![img](https://pic1.zhimg.com/80/v2-40dfcff92e8be06b5a6be914c84d8650_1440w.jpg)





## 异步IO模型



![img](https://pic4.zhimg.com/80/v2-1c9e7ded90780eb753352c8d92d41ad7_1440w.jpg)



refer

https://zhuanlan.zhihu.com/p/115912936 

# [Linux IO模式及 select、poll、epoll详解](https://segmentfault.com/a/1190000003063859)
# HashMap








## 扩容
以2的幂扩容

1.7 以前在头部插入会形成循环死链条

1.8 以后改在尾部插入







HashMap put的过程

https://www.cnblogs.com/captainad/p/10905184.html

![img](https://img2018.cnblogs.com/blog/1684605/201905/1684605-20190522150831073-641494049.png)

### 为什么是2得幂

如果既要达到最可能的平均分配hashMap的value的在table的各个index，又要用二进制计算实现存取效率，就要要求hashMap的容量必须为2的幂次方；

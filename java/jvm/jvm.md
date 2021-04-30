6.对象一定分配在堆上么，JIT，分层编译，逃逸分析



不一定，

jit：just in time

收集热点代码，将其转化为机器码



分层编译

分层编译将JVM的执行状态分为了五个层次。五个层级分别是：

1. 解释执行。
2. 执行不带profiling的C1代码。
3. 执行仅带方法调用次数以及循环回边执行次数profiling的C1代码。
4. 执行带所有profiling的C1代码。
5. 执行C2代码。



todoqifei



[基本功 | Java即时编译器原理解析及实践](https://tech.meituan.com/2020/10/22/java-jit-practice-in-meituan.html)
在异常发生之前就去处理

比如 foreach 中remove，在生成迭代器时，迭代器记录了ArrayList此时的`modCount`变量值；在迭代器的迭代过程中，也就是每次调用`next()`方法，都会调用`checkForComodification`判断**modCount变量的值是否在遍历过程中被修改**。



那如果确实有这样多线程同时修改与遍历的应用场景，应该如何操作呢？

1. 读写均加锁，比如使用`Collections.SynchronizedList`
2. 使用Fail-Safe集合，比如，CopyOnWriteArrayList,ConcurrentHashMap



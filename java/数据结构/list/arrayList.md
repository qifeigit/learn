# ArrayList

### 源码扩容过程有什么值得借鉴的地方？

答：有两点：

- 扩容的思想值得学习，通过自动扩容的方式，让使用者不用关心底层数据结构的变化，封装得很好，1.5 倍的扩容速度，可以让扩容速度在前期缓慢上升，在后期增速较快，大部分工作中要求数组的值并不是很大，所以前期增长缓慢有利于节省资源，在后期增速较快时，也可快速扩容。
- 扩容过程中，有数组大小溢出的意识，比如要求扩容后的数组大小，不能小于 0，不能大于 Integer 的最大







## 与LinkedList对比的问题

### 4.1 ArrayList 和 LinkedList 有何不同？

答：可以先从底层数据结构开始说起，然后以某一个方法为突破口深入，比如：

- 最大的不同是两者底层的数据结构不同，ArrayList 底层是数组，LinkedList 底层是双向链表
- 两者的数据结构不同也导致了操作的 API 实现有所差异，拿新增实现来说，ArrayList 会先计算并决定是否扩容，然后把新增的数据直接赋值到数组上，而 LinkedList 仅仅只需要改变插入节点和其前后节点的指向位置关系即可。

### 4.2 ArrayList 和 LinkedList 应用场景有何不同？

答：

- ArrayList 更适合于快速的查找匹配，不适合频繁新增删除，像工作中经常会对元素进行匹配查询的场景比较合适
- LinkedList 更适合于经常新增和删除，对查询反而很少的场景。

### 4.3 ArrayList 和 LinkedList 两者有没有最大容量？

答：

- ArrayList 有最大容量的，为 Integer 的最大值，大于这个值 JVM 是不会为数组分配内存空间的
- LinkedList 底层是双向链表，理论上可以无限大。但源码中，LinkedList 实际大小（size）用的是 int 类型，这也说明了 LinkedList 不能超过 Integer 的最大值，不然会溢出。



 和**vector**的区别

vector is almost identical to arraylist, and the difference is that vector is synchronized. because of this, it has an overhead than arraylist. normally, most java programmers use arraylist instead of vector because they can synchronize explicitly by themselves.



![img](../img/13990723-java-collection-hierarchy.jpeg)

###  如何解决线程安全问题？

答：Java 源码中推荐使用 Collections#synchronizedList 进行解决，Collections#synchronizedList 的返回值是 List 的每个方法都加了 synchronized 锁，保证了在同一时刻，数组和链表只会被一个线程所修改，但是性能大大降低，具体实现源码：

```
public boolean add(E e) {
    synchronized (mutex) {// synchronized 是一种轻量锁，mutex 表示一个当前 SynchronizedList
        return c.add(e);
    }
}
```

另外，还可以采用 JUC 的 CopyOnWriteArrayList 并发 List 来解决。





reference

[集合类源码分析](https://github.com/hpmmp/Java_collections)
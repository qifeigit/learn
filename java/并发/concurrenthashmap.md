ConcurrentHashMap保证线程安全主要有三个地方。

> - 一、使用volatile保证当Node中的值变化时对于其他线程是可见的
> - 二、使用table数组的头结点作为synchronized的锁来保证写操作的安全
> - 三、当头结点为null时，使用CAS操作来保证数据能正确的写入。

#### 通过CAS机制创建头结点

当多个线程进行put操作时，若其中的多个线程要操作的key值相同或者key值对应的数组下标相同，而数组对应下标的Node结点为`null`时，会同时进行链表初始化，若不加同步操作，就可能会产生数据丢失的情况。

这里通过CAS机制进行头结点的创建:

```java
else if ((f = tabAt(tab, i = (n - 1) & hash)) == null) { 
    // 通过CAS操作创建头结点
    if (casTabAt(tab, i, null,
                 new Node<K,V>(hash, key, value, null)))
        break;                   // no lock when adding to empty bin
}

static final <K,V> boolean casTabAt(Node<K,V>[] tab, int i,
                                    Node<K,V> c, Node<K,V> v) {
    // U: Unsafe的实例，compareAndSwapObject: native方法
    return U.compareAndSwapObject(tab, ((long)i << ASHIFT) + ABASE, c, v);
}
```

意思是通过CAS机制对数组`tab`中下标为 `i` 的元素进行赋值操作，当`tab[i] = null`时，才将`tab[i]`赋值为新节点 `new Node<K,V>(hash, key, value, null)`，CAS机制会保证只有一个线程能赋值成功，未成功的线程会重新进入for循环中。

#### 使用synchronized关键字操作Node

当多个线程(key值对应的数组下标一样)获取到的对应下标的Node不为空时，若不进行同步操作，也可能会产生数据丢失的情况，ConcurrentHashMap的数据结构与前面所说[HashMap](http://mp.weixin.qq.com/s?__biz=MzU4ODU0NjEzNw==&mid=2247483679&idx=1&sn=9d21171bd5c5beeb7aea934b692fe5e7&chksm=fdda6829caade13faac5a4c214e8661dcbfde9c15c46a494b9b7231e6ca15c1ff6352e5bf807#rd)的数据结构基本一致，在put时，会对链表进行修改和新增，在链表的数据量到达一定的数据量后，还会涉及到数据结构的变化。

这里采用synchronized锁，只有获取到相应的Node结点的锁，才能对Node结点进行操作，就不会产生数据丢失的情况。这样做的好处是不需要对整个ConcurrentHashMap加锁，多线程进行put操作时，只要key对应的下标不一样，就可以进行并行的put操作，不需要等待整个ConcurrentHashMap的锁释放。
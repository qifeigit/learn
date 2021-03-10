# HashMap源码



```java
/**
 * 找到大于或等于 cap 的最小2的幂
 */
static final int tableSizeFor(int cap) {
    int n = cap - 1;
    n |= n >>> 1;
    n |= n >>> 2;
    n |= n >>> 4;
    n |= n >>> 8;
    n |= n >>> 16;
    return (n < 0) ? 1 : (n >= MAXIMUM_CAPACITY) ? MAXIMUM_CAPACITY : n + 1;
}
```
![img](https://user-gold-cdn.xitu.io/2019/3/18/1698fd6875bc1f04?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



怎么获取一个元素应有的数组下标：

todoqifei



reference :

[源码](https://juejin.cn/post/6844903799748821000)
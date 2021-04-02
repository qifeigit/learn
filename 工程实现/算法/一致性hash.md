设计目标是为了解决因特网中的热点(Hot spot)问题，一致性hash算法提出了在动态变化的Cache环境中，判定哈希算法好坏的四个定义：1、平衡性(Balance) 2、单调性(Monotonicity) 3、分散性(Spread) 4、负载(Load)





treemap可以实现 一致性hash？

可以

以TreeMap为例，TreeMap本身提供了一个tailMap(K fromKey)方法，支持从红黑树中查找比fromKey大的值的集合，但并不需要遍历整个数据结构。



5.一致性hash原理，解决什么问题，数据倾斜，为什么是2的32次方，20次方可以么

为什么redis 的集群没有用一致性hash呢？

todoqifei



reference:

[对一致性Hash算法，Java代码实现的深入研究](https://www.cnblogs.com/xrq730/p/5186728.html)


Future的核心思想是：一个方法f，计算过程可能非常耗时，等待f返回，显然不明智。可以在调用f的时候，立马返回一个Future，可以通过Future这个数据结构去***控制***方法f的计算过程。

这里的***控制***包括：

get方法：获取计算结果（如果还没计算完，也是必须等待的）

cancel方法：还没计算完，可以取消计算过程

isDone方法：判断是否计算完

isCancelled方法：判断计算是否被取消

详见：https://www.cnblogs.com/jpfss/p/10815307.html























# [彻底理解Java的Future模式](https://www.cnblogs.com/cz123/p/7693064.html)
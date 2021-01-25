### JAVA中ABA中解决方案(AtomicStampedReference)

AtomicStampedReference主要维护包含一个对象引用以及一个可以自动更新的整数"stamp"的pair对象来解决ABA问题。

```java
//关键代码
public class AtomicStampedReference<V> {
    private static class Pair<T> {
        final T reference;  //维护对象引用
        final int stamp;  //用于标志版本
        private Pair(T reference, int stamp) {
            this.reference = reference;
            this.stamp = stamp;
        }
        static <T> Pair<T> of(T reference, int stamp) {
            return new Pair<T>(reference, stamp);
        }
    }
    private volatile Pair<V> pair;
    ....
    /**
      * expectedReference ：更新之前的原始值
      * newReference : 将要更新的新值
      * expectedStamp : 期待更新的标志版本
      * newStamp : 将要更新的标志版本
      */
    public boolean compareAndSet(V   expectedReference,
                                 V   newReference,
                                 int expectedStamp,
                                 int newStamp) {
        Pair<V> current = pair; //获取当前pair
        return
            expectedReference == current.reference && //原始值等于当前pair的值引用，说明值未变化
            expectedStamp == current.stamp && // 原始标记版本等于当前pair的标记版本，说明标记未变化
            ((newReference == current.reference &&
              newStamp == current.stamp) || // 将要更新的值和标记都没有变化
             casPair(current, Pair.of(newReference, newStamp))); // cas 更新pair
    }
}    
复制代码
```

### 例子

```java
private static AtomicStampedReference<Integer> atomicStampedRef =
        new AtomicStampedReference<>(1, 0);
public static void main(String[] args){
    Thread main = new Thread(() -> {
        System.out.println("操作线程" + Thread.currentThread() +",初始值 a = " + atomicStampedRef.getReference());
        int stamp = atomicStampedRef.getStamp(); //获取当前标识别
        try {
            Thread.sleep(1000); //等待1秒 ，以便让干扰线程执行
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        boolean isCASSuccess = atomicStampedRef.compareAndSet(1,2,stamp,stamp +1);  //此时expectedReference未发生改变，但是stamp已经被修改了,所以CAS失败
        System.out.println("操作线程" + Thread.currentThread() +",CAS操作结果: " + isCASSuccess);
    },"主操作线程");

    Thread other = new Thread(() -> {
        atomicStampedRef.compareAndSet(1,2,atomicStampedRef.getStamp(),atomicStampedRef.getStamp() +1);
        System.out.println("操作线程" + Thread.currentThread() +",【increment】 ,值 = "+ atomicStampedRef.getReference());
        atomicStampedRef.compareAndSet(2,1,atomicStampedRef.getStamp(),atomicStampedRef.getStamp() +1);
        System.out.println("操作线程" + Thread.currentThread() +",【decrement】 ,值 = "+ atomicStampedRef.getReference());
    },"干扰线程");

    main.start();
    other.start();
}
复制代码
// 输出
> 操作线程Thread[干扰线程,5,main],【increment】 ,值 = 2
> 操作线程Thread[干扰线程,5,main],【decrement】 ,值 = 1
> 操作线程Thread[主操作线程,5,main],初始值 a = 1
> 操作线程Thread[主操作线程,5,main],CAS操作结果: true
复制代码
```

ref

https://juejin.cn/post/6844903558253379597
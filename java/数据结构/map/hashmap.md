## 通过以下代码进行删除，是否可行？

```
HashMap<String,String > map = Maps.newHashMap();
map.put("1","1");
map.put("2","2");
map.forEach((s, s2) -> map.remove("1"));
```

答：不行，会报错误 ConcurrentModificationException，forEach源码如下：

```
public void forEach(BiConsumer<? super K, ? super V> action) {
        Node<K,V>[] tab;
        if (action == null)
            throw new NullPointerException();
        if (size > 0 && (tab = table) != null) {
            int mc = modCount; // 开始循环之前modCount被赋值给mc
            for (int i = 0; i < tab.length; ++i) {
                for (Node<K,V> e = tab[i]; e != null; e = e.next)
                    action.accept(e.key, e.value);
            }
            if (modCount != mc) // 删除时remove方法会修改modCount，但mc没变
                throw new ConcurrentModificationException();
        }
    }
```

建议使用迭代器的方式进行删除，原理同 ArrayList 迭代器原理，
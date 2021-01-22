#### [146. LRU 缓存机制](https://leetcode-cn.com/problems/lru-cache/)

```java
class LRUCache {
  HashMap<Integer,Dnode> hash ;
  class Dnode {
    int key;
    int value;
    Dnode prev;
    Dnode next;
    public Dnode() {}
    public Dnode(int _key, int _value) {key = _key; value = _value;}
  }
  Dnode head;
  Dnode tail;
  int capacity;

  public LRUCache(int capacity) {
    this.hash = new HashMap();
    this.capacity = capacity;
    head = new Dnode();
    tail = new Dnode();
    head.next = tail;
    tail.prev = head;
  }

```


```java
Node node;
class Node{
  char char1;
  boolean isEnd;
  Node[] words;
  Node(){
    words = new Node[26];
    // for(int i= 0;i<25;i++){
    //     words[i-'a'] = null;
    // }
  }
}
/** Initialize your data structure here. */
public Trie() {
  this.node = new Node();
}

/** Inserts a word into the trie. */
public void insert(String word) {
  String sub = word;
  Node cur = this.node;
  while(sub.length() >0){
    int curNum = sub.charAt(0) - 'a';
    if(cur.words[curNum] == null){
      cur.words[curNum] = new Node();
      cur.words[curNum].char1 = sub.charAt(0);
      if(sub.length()==1){
        cur.words[curNum].isEnd = true;
      }
    } else{
      if(sub.length()==1){
        cur.words[curNum].isEnd = true;
      }
    }
    sub = sub.substring(1);
    cur = cur.words[curNum];
  }
}
```


## dfs

https://leetcode-cn.com/problems/word-search/submissions/

单词搜索，采用深度优先，要清空状态



课程表，可以采用深搜







回溯法：

[n皇后](https://leetcode-cn.com/problems/n-queens/)

这题要注意剪枝法，当遍历到第n行时候，要注意第n-1行必须有元素才行







#### [207. 课程表](https://leetcode-cn.com/problems/course-schedule/)

```java
if(dp[i] == 1){
  if(i != start){
    return;
  }
  ans = false;
  return;
} else{
  dp[i] = 1;
}
for(int j =0 ;j<list.get(i).size();j++){
  int cur = list.get(i).get(j);
  dfs(cur,start,dp,list);
}
```


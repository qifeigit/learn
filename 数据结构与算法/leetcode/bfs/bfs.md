## 思路

用队列去保存下一层级的遍历的结果


## 相关问题

岛屿问题

#### [200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

```java
for(int i =0;i<len;i++){
  for(int j =0 ;j<n;j++){
    if(grid[i][j] == '1'){
      count++;
      grid[i][j] ='0';
      bfs(grid,i,j,len,n);
    }
  }
}
```






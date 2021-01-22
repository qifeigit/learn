#### [337. 打家劫舍 III](https://leetcode-cn.com/problems/house-robber-iii/)



```java
ans[0] = left[1] + right[1] + root.val;
ans[1] = Math.max(left[0],left[1]) + Math.max(right[0],right[1]);
return ans;
```


#### [49. 字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)

输入: ["eat", "tea", "tan", "ate", "nat", "bat"]
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]

对每一个元素origin先排序得到sortChar，再去map.put(sortChar,origin);

再把map转化为list


#### [349. 两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

#### [350. 两个数组的交集 II](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/)

思路：

用hash表记录第一个数组 出现的数字及其对应的次数 ，然后遍历第二个数组，如果有该数字则将其插入到结果列表中，并将对应的次数减一





#### [242. 有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/)



通过hash去做，

```java
 public boolean isAnagram(String s, String t) {
         int[] s1 = new int[26];
         int[] t1 = new int[26];
         int lens = s.length();
         int lent = t.length();
         if(lens != lent){
             return false;
         }
         
         for(int i =0;i<lens;i++){
             s1[s.charAt(i) - 'a']++;
             t1[t.charAt(i) - 'a']++;
         }  
         for(int i =0 ;i<26;i++){
             if(s1[i] != t1[i]){
                 return false;
             }
         }
         return true;
    }
```



#### [438. 找到字符串中所有字母异位词](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/)

用滑动窗口的方式去做



示例 1:

输入:
s: "cbaebabacd" p: "abc"

输出:
[0, 6]

解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的字母异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的字母异位词。







#### [438. 找到字符串中所有字母异位词](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/)


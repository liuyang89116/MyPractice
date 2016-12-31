# Problem 340: Longest Substring with At Most K Distinct Characters

> https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/

----------
![](/assets/340.png)

---------
##思路
* 还是利用 HashMap 和 sliding window 的方式进行
* 用 count 来记录不同的元素

---------


```java
public class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        int[] map = new int[128];
        int i = 0, j = 0, count = 0, maxLen = 0;
        while (j < s.length()) {
            if (map[s.charAt(j++)]++ == 0) count++;
            if (count > k) {
                while (--map[s.charAt(i++)] > 0);
                count--;
            }
            maxLen = Math.max(maxLen, j - i);
        }
        
        return maxLen;
    }
}
```

-------
##易错点
1. 表达式的理解
```java
if (map[s.charAt(j++)]++ == 0) count++;
```
需要注意的是，**不管条件是否满足，都要完成条件里面的两次“++”**，因为这是属于条件里面的部分。也就是说，每次扫过一个元素，j 都要递增，被扫过的元素的 count 也要递增。
```java
while (--map[s.charAt(i++)] > 0);
```
同理，这个表达式也是一样，每次都要先减然后 i 递增。
2.最后 j 和 i 的结束时候的情景是：i 是所选单词的开始字母，j 是所选单词的下一个字母

----------


































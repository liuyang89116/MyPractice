# Problem 159: Longest Substring with At Most Two Distinct Characters

> https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/

-------
![](/assets/159.png)

-------
##思路
* 和上一题的思路一样，代码略作改动

----------


```java
public class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        int[] map = new int[128];
        
        int i = 0, j = 0, count = 0, maxLen = 0;
        while (j < s.length()) {
            if (map[s.charAt(j++)]++ == 0) count++;
            
            while (count > 2) {
                if (map[s.charAt(i++)]-- == 1) count--;
            }
            maxLen = Math.max(maxLen, j - i);
        }
        
        return maxLen;
    }
}
```


# Problem 438: Find All Anagrams in a String``

> https://leetcode.com/problems/find-all-anagrams-in-a-string/

------
##思路
* 这道题的思路还是 sliding window 的经典思路：首先用一个 map 把 target 字符串的元素都存进去，接下来就慢慢地滑动窗口，遇到 map 中有的元素就 count--，当 count 为 0 的时候，说明我们的窗口中已经填满了这个元素
* 当窗口的 size 已经大于一个 target 字符串的时候，我们开始移动 left 

------


```java
public class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> rst = new ArrayList<Integer>();
        if (s == null || p == null || s.length() == 0 || p.length() == 0) {
            return rst;
        }
        
        int[] map = new int[128];
        for (char c : p.toCharArray()) {
            map[c]++;
        }
        int left = 0, right = 0, count = p.length();
        while (right < s.length()) {
            if (map[s.charAt(right)] > 0) {
                count--;
            }
            map[s.charAt(right)]--;
            right++;
            
            if (count == 0) {
                rst.add(left);
            }
            
            if (right - left == p.length()) {
                if (map[s.charAt(left)] >= 0) {
                    count++;
                }
                map[s.charAt(left)]++;
                left++;
            }
        }
        
        return rst;
    }
}
```

-----
##易错点
1. 条件判断
```java
if (right - left == p.length()) {
        if (map[s.charAt(left)] >= 0) {
            count++;
        }
        map[s.charAt(left)]++;
        left++;
}
```
其中 `map[s.charAt(left)] >= 0`意味着，原先这个 char 就是在 p 中的，否则经过不断地 --，已经小于 0 了。












# Problem 76: Minimum Window Substring

> https://leetcode.com/problems/minimum-window-substring/

---
##思路
* 这道题非常地经典，甚至衍生出了一个模板，可以处理类似的所有 substring 类的题目。
> https://discuss.leetcode.com/topic/30941/here-is-a-10-line-template-that-can-solve-most-substring-problems/44
* 这道题的思路就是用一个 hashmap (这里用的是 128 长度的 array，间接起到了 map 的作用) 来存储 pattern 元素；用 count 来判断当前的 window 里是否包含了这个 pattern
* 这里的处理问题的顺序是：先移动 j 尾巴，再移动 i head。

---------
##复杂度
* Time: `O(n)`

------


```java
public class Solution {
    public String minWindow(String s, String t) {
        int[] map = new int[128];
        for (char c : t.toCharArray()) {
            map[c]++;
        }
        
        int i = 0, j = 0, start = 0;
        int count = t.length(), minLen = Integer.MAX_VALUE;
        while (j < s.length()) {
            if (map[s.charAt(j++)]-- > 0) count--;
            while (count == 0) { // valid
                if (j - i < minLen) {
                    minLen = j - i;
                    start = i;
                }
                if (map[s.charAt(i++)]++ == 0) count++; 
            }
        }
        
        return minLen == Integer.MAX_VALUE ? "" : s.substring(start, start + minLen);
    }
}

```

-------
##易错点
1. 关键语句的解读
```java
if (map[s.charAt(j++)]-- > 0)
```
这里实际上是，
```java
if (map[s.charAt(j)] > 0) {...}
map[s.charAt(j)]--;
j++;
```
































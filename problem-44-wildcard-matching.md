# Problem 44: Wildcard Matching

> https://leetcode.com/problems/wildcard-matching/\#/description

-------

## 思路

> https://discuss.leetcode.com/topic/3040/linear-runtime-and-constant-space-solution/2

> http://yucoding.blogspot.com/2013/02/leetcode-question-123-wildcard-matching.html

这两篇讲解很好！

* 主要的思路就是：通过几个指针来来不断扫描整个字符串。sIndex 用来 track string 的位置；pIndex 用来 track pattern 的位置；用 match 来 track 之前的 ‘\*’ match 的元素的位置

* 分类讨论：如果是 `？`或者 s , p 对应的元素相同，那么就可以前进；如果是`*`，那么只有 p 可以前进，并且记录 star 的位置；如果都不对应，return false
* 需要注意的是，这里要记录 s 之前是否是 star，因为 star 可以 match 多个元素。

-----

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        int sIndex = 0, pIndex = 0, match = 0, starIndex = -1;
        while (sIndex < s.length()) {
            if (pIndex < p.length() && (s.charAt(sIndex) == p.charAt(pIndex) || p.charAt(pIndex) == '?')) {
                sIndex++;
                pIndex++;
            } else if (pIndex < p.length() && p.charAt(pIndex) == '*') {
                starIndex = pIndex;
                match = sIndex;
                pIndex++;
            } else if (starIndex != -1) {
                pIndex = starIndex + 1;
                match++;
                sIndex = match;
            } else {
                return false;
            }
        }
        
        while (pIndex < p.length() && p.charAt(pIndex) == '*') pIndex++;
        
        return pIndex == p.length();
    }
}
```






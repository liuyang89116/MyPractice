# Problem 14: Longest Common Prefix
>https://leetcode.com/problems/longest-common-prefix/

--------
##思路
* 就是从头到脚扫一遍数组，用 第一个数来和后面的进行对比，然后不停地 update

-------
```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        String prefix = strs[0];
        for (int i = 1; i < strs.length; i++) {
            int j = 0;
            while (j < prefix.length() && j < strs[i].length() && prefix.charAt(j) == strs[i].charAt(j)) {
                j++;
            }
            if (j == 0) {
                return "";
            }
            prefix = prefix.substring(0, j);
        }
        
        return prefix;
    }
}
```

# Problem 58: Length of Last Word


> https://leetcode.com/problems/length-of-last-word/

-------
##思路
* 从后往前慢慢走

---------
```java
public class Solution {
    public int lengthOfLastWord(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }  
        
        int len = s.length(), j = len - 1;
        while (j >= 0 && s.charAt(j) == ' ') j--;
        
        if (j < 0) {
            return 0;
        }
        int count = 0;
        while (j >= 0 && s.charAt(j) != ' ') {
            count++;
            j--;
        }
        
        return count;
    }
}
```

--------
##易错点
1. 注意 space 要留出 space
```java
s.charAt(j) == ' '
```
这里不能写成
```java
s.charAt(j) == ''
```
否则，charAt没法对应一个位置了。

















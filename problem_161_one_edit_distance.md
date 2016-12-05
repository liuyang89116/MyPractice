# Problem 161: One Edit Distance
> https://leetcode.com/problems/one-edit-distance/

-----------------
![](161.png)

-------
##思路
* 这道题其实不难，找准一个切入点就好了：从两个字符串的长度入手。
* s.length() == t.length(), 只要比较char 计算count不同就行
* |s.length() - t.length()| == 1， 找到不同的位数，从这个位开始比较后面的字符串是否相同，长的那个要从 i + 1 开始是相当于删除操作

-------------
```java
public class Solution {
    public boolean isOneEditDistance(String s, String t) {
        int m = s.length();
        int n = t.length();
        if (m > n) {
            return isOneEditDistance(t, s);
        }
        
        if (m == n) {
            int count = 0;
            for (int i = 0; i < m; i++) {
                if (s.charAt(i) != t.charAt(i)) {
                    count++;
                }
            }
            
            return count == 1;
        }
        
        if (n - m == 1) {
            for (int i = 0; i < m; i++) {
                if (s.charAt(i) != t.charAt(i)) {
                    return s.substring(i).equals(t.substring(i + 1));
                }
            }
            
            return true;
        }
        
        return false;
    }
}
```
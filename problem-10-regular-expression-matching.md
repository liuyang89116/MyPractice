# Problem 10: Regular Expression Matching

> https://leetcode.com/problems/regular-expression-matching/

-----
##思路
* `match[i][j]`表示 s 中前 i 个字符能否和 p 中前 j 个字符匹配。
* 初始化
```java
dp[0][0] = true;
for (int j = 2; j <= n; j++) {
        if (p.charAt(j - 1) == '*' && dp[0][j - 2]) {
              dp[0][j] = true;
        }
}
```
* 状态函数  

```
如果p中第j位是“ . ”或者p中第j位和s中第i位相同
match[i][j] = match[i - 1][j - 1]

如果 p 中第 j 位是 “ * ”，则要分情况讨论
1. 如果 p 中第 j-1 位和 s 中第 i 位不想等并且 p 中第 j - 1 位不是 “.”，则不能用 p 中 j - 1 位和 s 中第 i 位匹配，必须将 j - 1 位消掉，因此 “*” 取 0 个之前元素，match[i][j] = match[i][j - 2]
2. 如果 p 中第 j - 1 位和 s 中第 i 位想等或者 p 中第 j - 1 位为 “.”，则 “*” 可以有三种选择
1）“*” 取 0 个之前元素，和 1 中一样，将第 j - 1 位消掉，让 j - 2 位去和i位匹配（“”），match[i][j] = match[i][j -  2]
2）“*” 取 1 个之前元素，让 j - 1  位和i位匹配，match[i][j] = match[i][j-1]
3）“*” 取多个之前元素，因为 i 位一定会被匹配掉，因此看 i - 1  位能否继续匹配，match[i][j] = match[i-1][j]
三种情况有一种为 true 则 match[i][j] 为true
```
-------



```java
public class Solution {
    public boolean isMatch(String s, String p) {
        if (s == null || p == null) {
            return false;
        }
        
        int m = s.length(), n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        for (int j = 2; j <= n; j++) {
            if (p.charAt(j - 1) == '*' && dp[0][j - 2]) {
                dp[0][j] = true;
            }
        }
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p.charAt(j - 1) == '.') {
                    dp[i][j] = dp[i - 1][j - 1];
                }
                if (p.charAt(j - 1) == s.charAt(i - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                }
                if (p.charAt(j - 1) == '*') {
                    if (p.charAt(j - 2) != s.charAt(i - 1) && p.charAt(j - 2) != '.') {
                        dp[i][j] = dp[i][j - 2];
                    } else {
                        dp[i][j] = (dp[i][j - 1] || dp[i][j - 2] || dp[i - 1][j]);
                    }
                }
            }
        }
        
        return dp[m][n];
    }
}

```
----
##易错点
1. 2D 数组有 m + 1 和 n + 1 的大小，再循环的时候要考虑 `<=`
2. 字符串的 index 和 数组的 index 是错一位的。     
因为字符串是从 0 开始的，数组的 0 是一个 base，不具有实际的意义。数组记录的第 1 号位才是字符串的第一个 char 也就是字符串的 0 index。
3. 逻辑不好理清楚，多看几遍。

































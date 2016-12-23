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


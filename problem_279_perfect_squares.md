# Problem 279: Perfect Squares


> https://leetcode.com/problems/perfect-squares/

-----------
##思路
* 如果一个数 x 可以表示为一个任意数 a 加上一个平方数 bｘb，也就是 $$x = a + b ｘ b$$，那么能组成这个数 x 最少的平方数个数，就是能组成a最少的平方数个数加上 1（因为b x b已经是平方数了）。
* 这个完全平方数是多少不重要，重要的是有几个，所以我们把完全平方数的值设为 1,其他的不是完全平方数的设置为最大值，防止被娶到。

--------------
```java
public class Solution {
    public int numSquares(int n) {
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        for (int i = 0; i * i <= n; i++) {
            dp[i * i] = 1;
        }
        
        for (int a = 0; a <= n; a++) {
            for (int b = 0; a + b * b <= n; b++) {
                dp[a + b * b] = Math.min(dp[a] + 1, dp[a + b * b]);
            }
        }
        
        return dp[n];
    }
}
```






















# Problem: Backpack II

> http://www.lintcode.com/en/problem/backpack-ii/

------
##思路
* 和上一个题目的思路类似，看每一个 item 要还是不要。

-----


```java
public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A & V: Given n items with size A[i] and value V[i]
     * @return: The maximum value
     */
    public int backPackII(int m, int[] A, int V[]) {
        // write your code here
        if (m == 0 || A == null || A.length == 0) return 0;
        if (V.length != A.length) return 0;
        
        int n = V.length;
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (i >= A[j - 1]) {
                    dp[i][j] = Math.max(dp[i][j - 1], dp[i - A[j - 1]][j - 1] + V[j - 1]);
                } else {
                    dp[i][j] = dp[i][j - 1];
                }
            }
        }
        
        return dp[m][n];
    }
}
```


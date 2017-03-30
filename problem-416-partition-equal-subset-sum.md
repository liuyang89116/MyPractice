# Problem 416: Partition Equal Subset Sum

> https://leetcode.com/problems/partition-equal-subset-sum/\#/description

------

## 思路

> https://discuss.leetcode.com/topic/67539/0-1-knapsack-detailed-explanation

这个讲解不错！

* 我们首先要明确一点就是，如果存在这样的一种分组，那么他们的 subset 的和肯定是偶数。
* 我们用 dp 来考虑。`dp[i][j]`代表`前 i 个元素，凑成的和为 j`
* 所以很明显，`dp[0][0]`为 true, `dp[i][0]`也为 true （前 i 个元素可以凑成和为 0，他们谁都不取就可以了）；同理`dp[0][j] `为 false，因为一个元素都不取，凑不成 j。

---------

```java
public class Solution {
    public boolean canPartition(int[] nums) {
        if (nums == null || nums.length == 0) return false;
        
        int sum = 0, n = nums.length;
        for (int num : nums) {
            sum += num;
        }
        if ((sum & 1) == 1) return false;
        sum /= 2;
        
        boolean[][] dp = new boolean[n + 1][sum + 1];
        dp[0][0] = true;
        for (int i = 1; i < n + 1; i++) {
            dp[i][0] = true;
        }
        
        for (int i = 1; i < n + 1; i++) {
            for (int j = 1; j < sum + 1; j++) {
                dp[i][j] = dp[i - 1][j];
                if (j >= nums[i - 1]) {
                    dp[i][j] = (dp[i][j] || dp[i - 1][j - nums[i - 1]]);
                }
            }
        }
        
        return dp[n][sum];
    }
}
```




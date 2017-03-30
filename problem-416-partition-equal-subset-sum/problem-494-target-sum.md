# Problem 494: Target Sum

> https://leetcode.com/problems/target-sum/\#/description

-------

## 思路

* 这道题直观的思路就是用 dfs 来遍历，对于每一个数，要么加要么减。有点像排列组合类的 sum 题目。
* 但是这样的话两次递归，每个元素可以加可以减，复杂度是指数级的 $$2^n$$
* 那我们如何来优化呢？可以用 dp 的思想（参考均分两组和的问题）
* 每个数要么取，要么不取，自上而下化归



----------------------

```java
// dp 解法
public class Solution {
    public int findTargetSumWays(int[] nums, int S) {
        if (nums == null || nums.length == 0) return 0;
        
        int sum = 0, n = nums.length;
        for (int num : nums) {
            sum += num;
        }
        if (sum < S) return 0;
        sum += S;
        if ((sum & 1) == 1) return 0;
        sum /= 2;
        
        int[] dp = new int[sum + 1];
        dp[0] = 1;
        for (int num : nums) {
            for (int i = sum; i >= num; i--) {
                dp[i] += dp[i - num];
            }
        }
        
        return dp[sum];
    }
}
```





```java
// dfs 解法
public class Solution {
    int rst = 0;
    public int findTargetSumWays(int[] nums, int S) {
        dfs(0, 0, nums, S);
        
        return rst;
    }
    
    private void dfs(int sum, int count, int[] nums, int target) {
        if (count == nums.length) {
            if (sum == target) {
                rst++;
            }
            return;
        }
        
        dfs(sum + nums[count], count + 1, nums, target);
        dfs(sum - nums[count], count + 1, nums, target);
    }
}
```




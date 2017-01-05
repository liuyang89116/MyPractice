# Problem 377: Combination Sum IV


> https://leetcode.com/problems/combination-sum-iv/

----------
##思路
* 这道题理论上是可以用递归来解决的，但是运行的时候发现超时。所以我们考虑用动规来解。
* 只要 target > nums[i]，我们就可以拆分出更小的 target。
* 开头用 -1 来标记数组，表明没有访问过该元素。

-------------
```java
/*
  递归的解法，超时
*/
public class Solution {
    public int combinationSum4(int[] nums, int target) {
        if (target == 0) {
            return 1;
        }
        
        int res = 0;
        for (int i = 0; i < nums.length; i++) {
            if (target >= nums[i]) {
                res += combinationSum4(nums, target - nums[i]);

            }
        }
        
        return res;
    }
}
```
```java
public class Solution {
    public int combinationSum4(int[] nums, int target) {
        int[] dp = new int[target + 1];
        Arrays.fill(dp, -1);
        dp[0] = 1;
        
        return helper(nums, dp, target);
    }
    
    private int helper(int[] nums, int[] dp, int target) {
        if (dp[target] != -1) {
            return dp[target];
        }
        
        int res = 0;
        for (int i = 0; i < nums.length; i++) {
            if (target >= nums[i]) {
                res += helper(nums, dp, target - nums[i]);
            } 
        }
        dp[target] = res;
        
        return dp[target];
    }
}
```
------
##易错点
1. 每次 helper 结束之前要给```dp[target]```赋值，不能直接返回 res，因为这是个递归方程，下一次别人还要用之前的结果。
```java
dp[target] = res;
```

--------
##Follow Up
> What if negative numbers are allowed in the given array?
How does it change the problem?
What limitation we need to add to the question to allow negative numbers?

* 专门总结一下，这里的讲解不错
> https://discuss.leetcode.com/category/497/combination-sum-iv




























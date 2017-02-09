# Problem 213: House Robber II

> https://leetcode.com/problems/house-robber-ii/

-------
##思路
* 这道题的改变就是，house 变成了圆圈，现在 `0` 和 `num.length - 1`也相邻了，他们之间也可以互相影响了，偷你就不能偷我。
* 那么如何解决这个问题呢？我们可以把它转换为两个线性问题。<br/>
(1) rob: `0` 到 `n - 2`  <br/>
(2) rob: `1` 到 `n - 1`  <br/>
他们俩之间的最大值就是圆形 house 的解
* 在 main function 里注意不要忘了 base case 的 check。没有 house 和 一个 house 的情况。

---------


```java
public class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        if (nums.length == 1) return nums[0];
        
        return Math.max(helper(nums, 0, nums.length - 2), helper(nums, 1, nums.length - 1));
    }
    
    private int helper(int[] nums, int start, int end) {
        int prevNotRobbed = 0;
        int prevRobbed = 0;
        for (int i = start; i <= end; i++) {
            int currNotRobbed = Math.max(prevNotRobbed, prevRobbed);
            int currRobbed = nums[i] + prevNotRobbed;
            
            prevNotRobbed = currNotRobbed;
            prevRobbed = currRobbed;
        }
        
        return Math.max(prevNotRobbed, prevRobbed);
    }
}
```


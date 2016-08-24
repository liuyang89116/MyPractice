# Problem 53: Maximum Subarray


> https://leetcode.com/problems/maximum-subarray/

----------
##思路
* 这道题就是 *Best time to buy and sell stock* 的变种。怎么考虑呢？
* 其实```Subarray(i, j) = sum[j] - sum[i - 1];```，也就是说，找到最小的 sum，然后用当前的 sum[j] 不停地去减这个最小值，然后选最大的那个就是 max

--------
```java
public class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int max = Integer.MIN_VALUE, sum = 0, minSum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(minSum, sum);
        }
        
        return max;
    }
}
```
----------
##易错点

1. 熟悉*Best time to buy and sell stock* ，然后和维护的这三个值对应上：max, sum 和 minSum



















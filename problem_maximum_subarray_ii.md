# Problem: Maximum Subarray II (LintCode)

> http://www.lintcode.com/en/problem/maximum-subarray-ii/

-----
##思路
* 这道题和两次买卖股票的问题是类似的，但是稍有不同，不同点就是股票的价格都是正数但是对于array来说有正有负。
* 这道题原来的数组要分成两段，也就是说，存在一个位置，之前是一段 subarray，之后是另一段 subarray。那么和两次买卖股票题类似，我们可以从左扫一次，从右扫一次，分别代表两次的 maxSum，然后相加。

-----
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: An integer denotes the sum of max two non-overlapping subarrays
     */
    public int maxTwoSubArrays(ArrayList<Integer> nums) {
        if (nums == null || nums.size() == 0) {
            return 0;
        }
        
        int[] left = new int[nums.size()];
        int[] right = new int[nums.size()];
        
        // left to right
        int max = Integer.MIN_VALUE;
        int sum = 0, minSum = 0;
        for (int i = 0; i < nums.size(); i++) {
            sum += nums.get(i);
            max = Math.max(max, sum - minSum);
            minSum = Math.min(minSum, sum);
            left[i] = max;
        }
        
        // right to left
        max = Integer.MIN_VALUE;
        sum = 0; 
        minSum = 0;
        for (int i = nums.size() - 1; i >= 0; i--) {
            sum += nums.get(i);
            max = Math.max(max, sum - minSum);
            minSum = Math.min(minSum, sum);
            right[i] = max;
        }
        
        // update for max
        max = Integer.MIN_VALUE;
        for (int i = 0; i < nums.size() - 1; i++) {
            max = Math.max(max, left[i] + right[i + 1]);
        }
        
        return max;
    }
}
```
-----
##易错点
1. 临界点
```java
max = Math.max(max, left[i] + right[i + 1]);
```


















# Problem 152: Maximum Product Subarray


> https://leetcode.com/problems/maximum-product-subarray/

----------
##思路
* 这里有个和其他 subarray 不同的地方就是，数组里的数是有正有负的，负负得正，正数也可能因为乘以一个负数变得更小
* 所以我们维护两个数组： postiveMax 和 negativeMin 

--------
```java
public class Solution {
    public int maxProduct(int[] nums) {
        int[] posMax = new int[nums.length];
        int[] negMin = new int[nums.length];
        posMax[0] = negMin[0] =  nums[0];
        int result = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > 0) {
                posMax[i] = Math.max(nums[i], nums[i] * posMax[i - 1]);
                negMin[i] = Math.min(nums[i], nums[i] * negMin[i - 1]);
            } else if (nums[i] < 0) {
                posMax[i] = Math.max(nums[i], nums[i] * negMin[i - 1]);
                negMin[i] = Math.min(nums[i], nums[i] * posMax[i - 1]);
            }
            result = Math.max(result, posMax[i]);
        }
        
        return result;
    }
}
```
------
##易错点
1. 正数和负数分类讨论的时候， 注意区分什么时候乘以正数，什么时候乘以负数



























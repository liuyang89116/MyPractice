# Problem 16: 3Sum Closest


> https://leetcode.com/problems/3sum-closest/

-----
##思路
* 和 3sum 实际上没有什么区别，只不过是找最接近的而已
* 用两个 sum 来维护不同的值：sum，bestSum

-----
```java
public class Solution {
    public int threeSumClosest(int[] nums, int target) {
        if (nums == null || nums.length < 3) {
            return -1;
        }
        
        Arrays.sort(nums);
        int bestSum = nums[0] + nums[1] + nums[2];
        for (int i = 0; i < nums.length - 2; i++) {
            int left =  i + 1;
            int right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (Math.abs(target - sum) < Math.abs(target - bestSum)) {
                    bestSum = sum;
                }
                if (sum < target) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        
        return bestSum;
    }
}
```
-----
##易错点
1. 第二次比较的是 sum，不是 bestSum
```java
if (sum < target) {
         left++;
} else {
         right--;
}
```
2. 循环之前 sort 数组














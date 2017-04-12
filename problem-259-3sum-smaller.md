# Problem 259: 3Sum Smaller

> https://leetcode.com/problems/3sum-smaller/\#/description

------------

![](/assets/259.png)

-------

## 思路

* 双指针法：遍历 i 的时候， 用 left 和 right 从两边向中间逼近
* 注意：一定要 sort 原来的 Array

-------

```java
public class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        if (nums == null || nums.length == 0) return 0;
        int count = 0, len = nums.length;
        
        Arrays.sort(nums);
        for (int i = 0; i < len - 2; i++) {
            int left = i + 1, right = len - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum < target) {
                    count += right - left;
                    left++;
                } else {
                    right--;
                }
            }
        }
        
        return count;
    }
}
```




# Problem 18: 4Sum


> https://leetcode.com/problems/4sum/

------
##思路
* 3sum 的变种，相当于是双层循环再套一遍双指针

-------
##复杂度
* Time: `O(n^3)`

---------------

```java
public class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<Integer> tmp = new ArrayList<Integer>();
        List<List<Integer>> result = new ArrayList(tmp);
        if (nums == null || nums.length < 4) {
            return result;
        }
        
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 3; i++) {
            if (i != 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            for (int j = i + 1; j < nums.length - 2; j++) {
                if (j != i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }
                int left = j + 1;
                int right = nums.length - 1;
                while (left < right) {
                    int sum = nums[i] + nums[j] + nums[left] + nums[right];
                    if (sum == target) {
                        tmp = new ArrayList<Integer>();
                        tmp.add(nums[i]);
                        tmp.add(nums[j]);
                        tmp.add(nums[left]);
                        tmp.add(nums[right]);
                        result.add(tmp);
                        left++;
                        right--;
                        while (left < right && nums[left] == nums[left - 1]) {
                            left++;
                        }
                        while (left < right && nums[right] == nums[right + 1]) {
                            right--;
                        }
                    } else if (sum < target) {
                        left++;
                    } else {
                        right--;
                    }
                }
             }
        }
        
        return result;
    }
}
```
--------
##易错点
1. 注意数组的角标，防止越界
2. **Always sort**在处理数组之前























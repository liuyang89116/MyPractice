# Problem 442: Find All Duplicates in an Array

> https://leetcode.com/problems/find-all-duplicates-in-an-array/\#/description

--------

## 思路

* 和上一题的思路一样，遍历数组的时候，把访问过的标记为负数，这样，如果它已经 visited 过，我们可以立马看出来

------

```java
public class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        List<Integer> rst = new ArrayList<>();
        if (nums == null || nums.length == 0) return rst;
        
        for (int i = 0; i < nums.length; i++) {
            int index = Math.abs(nums[i]) - 1;
            if (nums[index] < 0) {
                rst.add(index + 1);
            } else {
                nums[index] = -nums[index];
            }
        }
        
        return rst;
    }
}
```




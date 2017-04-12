# Problem 448: Find All Numbers Disappeared in an Array

> https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/\#/description

--------

## 思路

* 我们用 `nums[nums[i] -1] = -nums[nums[i]-1]`来遍历整个数组，对已有的元素标成负数
* 第二次遍历的时候，把没有被标注的元素挑出来，加进 list

------

```java
public class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> rst = new ArrayList<Integer>();
        if (nums == null || nums.length == 0) return rst;
        
        for (int i = 0; i < nums.length; i++) {
            int index = Math.abs(nums[i]) - 1;
            if (nums[index] > 0) {
                nums[index] = -nums[index];
            }
        }
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 0) {
                rst.add(i + 1);
            }
        }
        
        return rst;
    }
}
```




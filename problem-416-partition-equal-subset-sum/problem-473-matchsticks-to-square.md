# Problem 473: Matchsticks to Square

> https://leetcode.com/problems/matchsticks-to-square/\#/description

-------

# 思路

* 之前的题目是平分成两份，这里升级了以后，相当于是平分成四份。
* 很难用 dp 去解决，这里用了最简单的 dfs 的思路。
* 在 dfs 之前，加入了 sort array 的过程，这样可以优化 dfs 的过程
* 整个 dfs 的过程还是不好理解的。每次在判断的时候，count 加 1，进入下一层去判断；儿判断之后，再把 nums 的元素减去

-------

```java
public class Solution {
    public boolean makesquare(int[] nums) {
        if (nums == null || nums.length < 4) return false;
        
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        if (sum % 4 != 0) return false;
        
        Arrays.sort(nums);
        reverse(nums);
        
        return dfs(nums, new int[4], 0, sum / 4);
    }
    
    private boolean dfs(int[] nums, int[] sums, int count, int target) {
        if (count == nums.length) {
            if (sums[0] == target && sums[1] == target && sums[2] == target) return true;
        }
        
        for (int i = 0; i < 4; i++) {
            if (sums[i] + nums[count] > target) continue;
            sums[i] += nums[count];
            if (dfs(nums, sums, count + 1, target)) return true;
            sums[i] -= nums[count];
        }
        
        return false;
    }
    
    private void reverse(int[] nums) {
        int len = nums.length;
        for (int i = 0; i < len / 2; i++) {
            int tmp = nums[i];
            nums[i] = nums[len - 1 - i];
            nums[len - 1 - i] = tmp;
        }
    }
}
```




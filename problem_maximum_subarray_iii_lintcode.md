# Problem: Maximum Subarray III (LintCode)


> http://www.lintcode.com/en/problem/maximum-subarray-iii/

--------
##思路
* 这是一道划分类的动态规划。选 k 个元素很难再像前面那样一个一个标记划分位置判断了，必须得放在一个二维数组里做判断
* state：
  
  ```localMax[i][j]```表示前 i 个数组当中，取 j 个数组，包含第 i 个数的 Maximum Sum;
  ```globalMax[i][j]```表示前 i 个数组当中，取 j 个数组，可以不包含第 i 个数组
* 状态方程

  ```java
  localMax[i][j] = Math.max(localMax[i][j - 1], globalMax[i - 1][j - 1]) + nums[j - 1];
  globalMax[i][j] = Math.max(globalMax[i][j - 1], localMax[i][j]);
  ```
-----------
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @param k: An integer denote to find k non-overlapping subarrays
     * @return: An integer denote the sum of max k non-overlapping subarrays
     */
    public int maxSubArray(int[] nums, int k) {
        if (nums.length < k) {
            return 0;
        }
        
        int len = nums.length;
        int[][] localMax = new int[k + 1][len + 1];
        int[][] globalMax = new int[k + 1][len + 1];
        
        for (int i = 1; i <= k; i++) {
            localMax[i][i - 1] = Integer.MIN_VALUE;
            for (int j = i; j <= len; j++) {
                localMax[i][j] = Math.max(localMax[i][j - 1], globalMax[i - 1][j - 1]) + nums[j - 1];
                if (i == j) {
                    globalMax[i][j] = localMax[i][j];
                } else {
                    globalMax[i][j] = Math.max(globalMax[i][j - 1], localMax[i][j]);
                }
            }
        }
        
        return globalMax[k][len];
    }
}

```
--------
##易错点

1. 第 j 个元素，在数组中是```nums[j - 1]```

   ```localMax[i][j] = Math.max(localMax[i][j - 1], globalMax[i - 1][j - 1]) + nums[j - 1];```
































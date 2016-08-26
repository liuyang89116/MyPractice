# Problem: Maximum Subarray Difference (LintCode)


> http://www.lintcode.com/en/problem/maximum-subarray-difference/

--------------------
##思路
* 这道题实际上是两次买卖股票的升级版。
* 绝对值之差的最大值的实质是什么？ |A - B| 的最大值，就是**A最大**，B 要非常小，换句话说，就是**(-B)也要最大**。
* 那么思路就很好理解了，找到```left[]```的最小值和最大值，找到```right[]```的最小值和最大值。相当于进行四次 Maximum Subarray

---------------
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: An integer indicate the value of maximum difference between two
     *          Subarrays
     */
    public int maxDiffSubArrays(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int size = nums.length;
        int[] left_min = new int[size];
        int[] left_max = new int[size];
        int[] right_min = new int[size];
        int[] right_max = new int[size];
        int[] copy = new int[size];
        
        for (int i = 0; i < size; i++) {
            copy[i] = -1 * nums[i];
        }
        
        
        // left_max
        int sum = 0, minSum = 0;
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < size; i++) {
            sum += nums[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(minSum, sum);
            left_max[i] = max;
        }
        
        // right_max
        sum = 0;
        minSum = 0;
        max = Integer.MIN_VALUE;
        for (int i = size - 1; i >= 0; i--) {
            sum += nums[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(minSum, sum);
            right_max[i] = max;
        }
        
        // left_min
        sum = 0;
        minSum = 0;
        max = Integer.MIN_VALUE;
        for (int i = 0; i < size; i++) {
            sum += copy[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(minSum, sum);
            left_min[i] = -1 * max;
        }
        
        //right_min
        sum = 0;
        minSum = 0;
        max = Integer.MIN_VALUE;
        for (int i = size - 1; i >= 0; i--) {
            sum += copy[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(minSum, sum);
            right_min[i] = -1 * max;
        }
        
        int diff = 0;
        int left = Integer.MIN_VALUE, right = Integer.MIN_VALUE;
        for (int i = 0; i < size - 1; i++) {
            diff = Math.max(diff, Math.abs(left_max[i] - right_min[i + 1]));
            diff = Math.max(diff, Math.abs(left_min[i] - right_max[i + 1]));
        }
        
        return diff;
    }
}
```
-------------
##思路
1. 最后求最大值
```java
int diff = 0;
int left = Integer.MIN_VALUE, right = Integer.MIN_VALUE;
for (int i = 0; i < size - 1; i++) {
          diff = Math.max(diff, Math.abs(left_max[i] - right_min[i + 1]));
          diff = Math.max(diff, Math.abs(left_min[i] - right_max[i + 1]));
}
```
方法一定是：**左边的最小 - 右边的最大；左边的最大 - 右边的最小**。之前犯错的原因是：左边的最小 - 右边的最大；右边的最大 - 左边的最小。结果看似是两行语句，实际上办的是一件事儿！所以永远从左边出发，这样不容易错。

2. Maximum Subarray 的核心一定要熟练
```java
// left_max
int sum = 0, minSum = 0;
int max = Integer.MIN_VALUE;
for (int i = 0; i < size; i++) {
        sum += nums[i];
        max = Math.max(max, sum - minSum);
        minSum = Math.min(minSum, sum);
        left_max[i] = max;
}
```
3. 求最小值的时候，最后给 max 乘 -1再变回最小
```java
sum = 0;
minSum = 0;
max = Integer.MIN_VALUE;
for (int i = 0; i < size; i++) {
        sum += copy[i];
        max = Math.max(max, sum - minSum);
        minSum = Math.min(minSum, sum);
        left_min[i] = -1 * max;
}
```

































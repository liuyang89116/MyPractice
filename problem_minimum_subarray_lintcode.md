# Problem: Minimum Subarray (LintCode)

> http://www.lintcode.com/en/problem/minimum-subarray/

-----------
##思路
* 这道题可以直接转变为 Maximum Subarray 的题目。关键点就是两个，首先把所有的值都变为负数，最后再给找到的最大值变号

---------------
```java
public class Solution {
    /**
     * @param nums: a list of integers
     * @return: A integer indicate the sum of minimum subarray
     */
    public int minSubArray(ArrayList<Integer> nums) {
        if (nums == null || nums.size() == 0) {
            return 0;
        }
        
        int sum = 0, minSum = 0;
        int max = Integer.MIN_VALUE;
        int[] copy = new int[nums.size()];
        for (int i = 0; i < nums.size(); i++) {
            copy[i] = -1 * nums.get(i);
        }
        
        for (int i = 0; i < copy.length; i++) {
            sum += copy[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(minSum, sum);
        }
        
        return -1 * max;
    }
}
```
-----
##易错点
1. 最大最小值赋值的时候不要赋值为0
```java
int max = Integer.MIN_VALUE;
int min = Integer.MAX_VALUE;
```
最大值赋值最小，最小值赋值最大。当初赋值为0，最后出错
```java
int max = 0;
```

























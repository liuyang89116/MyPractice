# Problem 360: Sort Transformed Array

> https://leetcode.com/problems/sort-transformed-array/

-----------
![](/assets/360.png)

--------
##思路
* 这道题考察的是二次函数，用双指针来优化。
* 当 `a > 0` 的时候，二次函数开口向上，两边的元素最大，中间的元素最小。那么我们排序的时候，从两边往中间扫最先遇到的肯定是大数。
* 当 `a < 0` 的时候，二次函数开口向下，两边的元素最小，中间的元素最大，那么我们从两边往中间扫的时候，先遇到的时候是小数。

---------
##复杂度
* Time: `O(n)`

-------


```java
public class Solution {
    public int[] sortTransformedArray(int[] nums, int a, int b, int c) {
        int[] rst = new int[nums.length];
        int index = (a >= 0 ? nums.length - 1 : 0);
        int i = 0, j = nums.length - 1;
        while (i <= j) {
            if (a >= 0) {
                rst[index--] = helper(nums[i], a, b, c) >= helper(nums[j], a, b, c) ? helper(nums[i++], a, b, c) : helper(nums[j--], a, b, c); 
            } else {
                rst[index++] = helper(nums[i], a, b, c) <= helper(nums[j], a, b, c) ? helper(nums[i++], a, b, c) : helper(nums[j--], a, b, c);
            }
        }
        
        return rst;
    
    }
    
    private int helper(int x, int a, int b, int c) {
        return a * x * x + b * x + c;
    }
}
```
-----
##Follow Up
> 对一个 sorted array 平方后排序


























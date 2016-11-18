# Problem 334: Increasing Triplet Subsequence


>https://leetcode.com/problems/increasing-triplet-subsequence/

------------------
##思路
* 要想有一个递增的数列，至少前面有两个数字（最小的，第二小的），来判断第三个数字
* 可以维护两个值：最小值和倒数第二小的值；但是怎么满足，最小，第二小，最大这个顺序呢？我们可以用 if - else if - else 这个条件判断来实现

----------
```java
public class Solution {
    public boolean increasingTriplet(int[] nums) {
        if (nums == null || nums.length < 3) {
            return false;
        } 
        
        int smallest = Integer.MAX_VALUE;
        int smaller = Integer.MAX_VALUE;
        for (Integer num : nums) {
            if (num <= smallest) {
                smallest = num;
            } else if (num <= smaller) {
                smaller = num;
            } else {
                return true;
            }
        }
        
        return false;
    }
}
```
------------
##易错点
1. 维护那两个元素的时候，要把他们事先设置为最大。




















# Problem 80: Remove Duplicates from Sorted Array II


> https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/

---------
##思路
* 用 count 作为指针来标记总的元素的个数
* 两个指针 i 和 j 用来控制最后不超过两个相同元素

--------
```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int count = 0;
        int i, j;
        for (i = 0; i < nums.length;) {
            int cur = nums[i];
            for (j = i; j < nums.length; j++) {
                if (nums[j] != cur) {
                    break;
                }
                if (j - i < 2) {
                    nums[count] = cur;
                    count++;
                }
            }
            i = j;
        }
        
        return count;
    }
}
```
-------
##易错点

1. for 循环的改进
```java
for (int i = 0; i < nums.length;) {
    for (int j = i; j < nums.length; j++) {
        执行语句1;
    }
    执行语句2;
    i = j;
}
```
通过```i = j```来控制循环的 step
2. 每次标定当前元素
```int cur = nums[i];```
3. 当前元素赋值给```count```元素
```java
if (j - i < 2) {
         nums[count] = cur;
         count++;
}
```
4. 是上一个题目的变种，盯着看没有用，可以试着口头编译一个小例子： ```[1, 1, 2, 2, 2, 5]```，i, j 如影随形的两个指标，来控制他们之间的距离小于 2

























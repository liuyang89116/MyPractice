# Problem 283: Move Zeroes

> https://leetcode.com/problems/move-zeroes/

----------
##思路
* 很经典的题目，最开始的时候一直没打开思路，老想用 swap 去做。但是一旦 swap，顺序就会乱的
* 这个思路的新奇之处就是，通过赋值而不是 swap 来“移动”元素。
* count 用来计数，做过多少个非零的数字，最后再把剩下的数字用 0 走完

-----------
```java
public class Solution {
    public void moveZeroes(int[] nums) {
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                nums[count++] = nums[i];
            }
        }
        while (count < nums.length) {
            nums[count++] = 0;
        }
    }
}
```



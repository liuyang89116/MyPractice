# Problem 268: Missing Number


> https://leetcode.com/problems/missing-number/

----------
##思路
* 异或运算的考察
* 因为 index i 和 nums[i] 的值应该是对应的，少了的那个通过异或运算找出来
* a ^ a = 0; a ^ 0 = a. 其他的 index i 和 nums[i] 都配对成功了，然后都抵消为 0 了，最后剩下的那个 a 就是 missing 掉的。

--------
```java
public class Solution {
    public int missingNumber(int[] nums) {
        int xor = 0;
        int i = 0;
        for (; i < nums.length; i++) {
            xor = xor ^ i ^ nums[i];
        }
        
        return xor ^ i;
    }
}
```
# Problem 137: Single Number II


> https://leetcode.com/problems/single-number-ii/

-------------
##思路
* 这道题的思路和上一道题类似，就是利用三个元素进行抵消，所以我们考虑使用三进制
* 位运算我还没有搞懂，先把这题留着，下次再搞定

----------
```java
public class Solution {
    public int singleNumber(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int result = 0;
        int[] bits = new int[32];
        for (int i = 0; i < 32; i++) {
            for (int j = 0; j < nums.length; j++) {
                bits[i] += nums[j] >> i & 1;
                bits[i] %= 3;
            }
            result |= (bits[i] << i);
        }
        return result;
    }
}
```


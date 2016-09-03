# Problem 66: Plus One


> https://leetcode.com/problems/plus-one/

--------------
##思路
* 逐位加法。有两种情况：第一就是进位进到某个位置停住了，carriers == 0；还有一种情况是一直进位，加到最高位，这时候需要扩大数组的大小，并且最高位为0

-------------
```java
public class Solution {
    public int[] plusOne(int[] digits) {
        int carriers = 1;
        for (int i = digits.length - 1; i >= 0 && carriers > 0; i--) {
            int sum = digits[i] + carriers; 
            digits[i] = sum % 10;
            carriers = sum / 10;
        }
        
        if (carriers == 0) {
            return digits;
        }
        int[] rst = new int[digits.length + 1];
        rst[0] = 1;
        for (int i = 1; i < rst.length; i++) {
            rst[i] = digits[i - 1];
        }
        
        return rst;
    }
}
```

-------
##易错点
1. 从最后一位往前面加
2. 新数组和原数组大小不一样的时候，注意 index
```java
for (int i = 1; i < rst.length; i++) {
         rst[i] = digits[i - 1];
}
```



































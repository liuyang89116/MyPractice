# Problem 29: Divide Two Integers

> https://leetcode.com/problems/divide-two-integers/

----------
##思路
* 这道题可以看做是二分法的应用，每次用除数来翻倍（这里用 shift），然后和被除数比较
* 当除数翻倍到比被除数大了以后，我们就后退一位
* 这道题的 corner cases 要注意

-------------
```java
public class Solution {
    public int divide(int dividend, int divisor) {
        if (dividend == 0) {
            return 0;
        }
        if (divisor == 0) {
            return dividend >= 0 ? Integer.MAX_VALUE : Integer.MIN_VALUE; 
        }
        if (dividend == Integer.MIN_VALUE && divisor == -1) {
            return Integer.MAX_VALUE;
        }
        
        boolean isNegative = (dividend > 0 && divisor < 0) || (dividend < 0 && divisor > 0);
        long a = Math.abs((long) dividend);
        long b = Math.abs((long) divisor);
        int rst = 0;
        while (a >= b) {
            int shift = 0;
            while (a >= (b << shift)) {
                shift++;
            }
            a -= b << (shift - 1);
            rst += 1 << (shift - 1);
            
        }
        
        return isNegative ? -rst : rst;
        
    }
}
```
-------
##易错点
1. corner cases  
(1) 被除数为 0  
(2) 除数为 0  
这时候有可能是极大值，同时也有可能是极小值  
2. 极大值和极小值
```java
Integer.MAX_VALUE;  // 2^31 - 1; 2147483647
Integer.MIN_VALUE;  // -2^31; -2147483648
```
所以当被除数是极小值，除数是 -1 的时候会溢出
3. 数字翻倍的时候有可能溢出，转为 long 类型
```java
long a = Math.abs((long) dividend);
long b = Math.abs((long) divisor);
```



















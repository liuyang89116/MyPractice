# Problem 372: Super Pow


> https://leetcode.com/problems/super-pow/

----------
##思路
* 基本手段还是 fastPower 的思想，不同的是，加入了一个逐位取数的过程
* 比如： 2^32 = (2^10) * (2^3) * (2^2)
-----
```java
public class Solution {
    public int superPow(int a, int[] b) {
       int result = 1;
       for (int i = 0; i < b.length; i++) {
           result = fastPow(result, 10) * fastPow(a, b[i]) % 1337;
       }
       return result;
    } 
    
    public int fastPow(int a, int n) {
        if (n == 1) {
            return a % 1337;
        }
        if (n == 0) {
            return 1 % 1337;
        }
        
        long product = fastPow(a, n / 2);
        product = (product * product) % 1337;
        if (n % 2 == 1) {
            product = (product * a) % 1337;
        }
        
        return (int) product;
    }
}
```
----
##思路
1. 逐位取数
```java
for (int i = 0; i < b.length; i++) {
      result = fastPow(result, 10) * fastPow(a, b[i]) % 1337;
}
```
每一位，相当于是**在原来的 result 的基础上，再 pow 10**。
2. result 初始化
```java
int result = 1;
```




















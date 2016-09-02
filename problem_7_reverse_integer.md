# Problem 7: Reverse Integer


> https://leetcode.com/problems/reverse-integer/

-----
##思路
* 数学类的翻转通常都不是为了转化成 String 数组，而是通过数学的公式得出翻转的结果
* 公式 
```
reverseNum = reverseNum * 10 + x % 10;
x = x / 10;
```
-----
```java
public class Solution {
    public int reverse(int x) {
        if (x == 0) {
            return 0;
        }
        
        int reverseNum = 0;
        while (x != 0) {
            int temp = reverseNum * 10 + x % 10;
            x /= 10;
            if (temp /10 != reverseNum) {
                return 0;
            }
            reverseNum = temp;
        }
        return reverseNum;
    }
}
```
------
##易错点

1. 数据溢出
```java
if (temp /10 != reverseNum) {
            return 0;
}
```
当 reverseNum 足够大的时候，再乘以 10 就会数据溢出。所以在这里需要 check











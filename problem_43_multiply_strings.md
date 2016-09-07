# Problem 43: Multiply Strings

> https://leetcode.com/problems/multiply-strings/

----------
##思路
* 这道题不允许先转成 Integer 然后再计算。还有一点是直接乘的话数据会溢出。
* 直接乘会溢出，所以每次都要两个single digit相乘，最大81，不会溢出。
* 比如385 * 97, 就是个位 = 5 * 7，十位 = 8 * 7 + 5 * 9 ，百位 = 3 * 7 + 8 * 9 …
* 可以每一位用一个 Int 表示，存在一个int[]里面。
这个数组最大长度是num1.len + num2.len，比如99 * 99，最大不会超过10000，所以4位就够了。
* num1 的第 i 位和 num2 的第 j 位乘，结果在 num[i + j + 1] 位
* 最后结果前面的0要清掉。

------------
```java
public class Solution {
    public String multiply(String num1, String num2) {
        int len1 = num1.length(), len2 = num2.length();
        int[] num3 = new int[len1 + len2];
        int i, j, product, carrier;
        
        for (i = len1 - 1; i >= 0; i--) {
            carrier = 0;
            for (j = len2 - 1; j >= 0; j--) {
                product = carrier + num3[i + j + 1] + Character.getNumericValue(num1.charAt(i)) * Character.getNumericValue(num2.charAt(j));
                num3[i + j + 1] = product % 10;
                carrier = product / 10;
            }
            num3[i + j + 1] = carrier;
        }
        
        StringBuilder sb = new StringBuilder();
        i = 0;
        while (i < num3.length - 1 && num3[i] == 0) {
            i++;
        }
        while (i < num3.length) {
            sb.append(num3[i]);
            i++;
        }
        
        return sb.toString();
        
    }
}
```
---
##易错点
1. 和加法不一样，乘法要把之前的结果也加上 ```num3[i + j + 1]```
```java
product = carrier + num3[i + j + 1] + Character.getNumericValue(num1.charAt(i)) * Character.getNumericValue(num2.charAt(j));
```
原因很简单就是，乘法一位一位地要不停地往前面乘。而加法每位数只“见一次面”
2. 把剩下的进位进到下一位去
```java
num3[i + j + 1] = carrier;
```
这时候的 num3[i + j + 1] 和之前的 num3[i + j + 1] 是不一样的，以为这时候，j = -1
3. 把没用的 0 都去掉
```java
i = 0;
while (i < num3.length - 1 && num3[i] == 0) {
        i++;
}
```





















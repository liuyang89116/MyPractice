# Problem: Fast Power (LintCode)


> http://www.lintcode.com/en/problem/fast-power/

-----------
##思路
* 对时间复杂度有要求 O(logn)，所以要考虑对半分
* 取 mod 的分配率：(a * b) % c = [(a % c) * (b % c)] % c;

-----------
```java
class Solution {
    /*
     * @param a, b, n: 32bit integers
     * @return: An integer
     */
    public int fastPower(int a, int b, int n) {
        if (n == 1) {
            return a % b;
        }
        if (n == 0) {
            return 1 % b;
        }
        
        long product = fastPower(a, b, n / 2);
        product = product * product % b;
        if (n % 2 == 1) {
            product = (product * a) % b;
        }
        
        return (int) product;
    }
};
```
----------
##易错点

1. n == 0 的情况
```java
if (n == 0) {
       return 1 % b;
}
```
当时错写成 ```return b;```
2. 中间的计算结果用 long 存储，最后再转成 int 类型
```java
long product = fastPower(a, b, n / 2);
```
```java
return (int) product;
```
3. 如果 power n 是奇数的话，记得再多乘一次 a
```java
if (n % 2 == 1) {
        product = (product * a) % b;
}
```




























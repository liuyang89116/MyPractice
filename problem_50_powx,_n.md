# Problem 50: Pow(x, n)


> https://leetcode.com/problems/powx-n/

---------
##思路
* 这道题用二分法做。
* 简而言之就是```x^n = x^(n/2) * x^(n/2) * x^(n%2)```，如果写成表达式应该是```pow(x, n) = pow(x, n / 2) * pow(x, n / 2) * pow(x, n - n / 2 * n / 2)```

-------------
```java
public class Solution {
    public double myPow(double x, int n) {
        if (n == 0) {
            return 1;
        }
        
        if (n == 1) {
            return x;
        }
        
        boolean isNegative = false;
        if (n < 0) {
            isNegative = true;
            n = -1 * n;
        }
        int k = n / 2;
        int l = n - 2 * k;
        double t1 = myPow(x, k);
        double t2 = myPow(x, l);
        double ans = t1 * t1 * t2;
        
        // overflow
        if (ans == 0 && n != 0) {
            return 0;
        }
        
        if (isNegative) {
            return 1 / ans;
        } else {
            return ans;
        }

    }
}
```
----
##易错点

1. 分类讨论：n == 0, n == 1, n 的正负
2. 考虑越界的情况！
```java
// overflow
if (ans == 0 && n != 0) {
         return 0;
}
```
当 pow(x, n)，n = Integer.MAX_VALUE 的时候，x 为正数，那么结果越界，为 0 ；x 为负数，1/0 是无穷小，也为 0 





























# Fibonacci numbers

> Write a function int fib(int n) that returns Fn. For example, if n = 0, then fib() should return 0. If n = 1, then it should return 1. For n > 1, it should return F(n-1) + F(n-2), like: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ……..

--------
##思路
* 可以用 recursion 做，但是复杂度很大 `T(n) = T(n-1) + T(n-2)` 指数级别
* 第二种方法是 dp 做，`O(n)` 时间解决，空间可以优化

---------


```java
/**
 * Created by yang on 1/1/17.
 */
public class Solution2 {
    // method1: recusion
    public static int fib1(int n) {
        if (n <= 1) return n;
        return fib1(n - 1) + fib1(n - 2);
    }

    // method2: dp
    public static int fib2(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;


        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }

    // method 3: optimize space
    public static int fib3(int n) {
        int[] dp = new int[2];
        dp[0] = 0;
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            int tmp = dp[0] + dp[1];
            dp[0] = dp[1];
            dp[1] = tmp;
        }

        return dp[1];
    }


    public static void main(String[] args) {
        System.out.println(fib3(9));
    }
}

```


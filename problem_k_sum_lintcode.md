# Problem: k Sum (LintCode)


> http://www.lintcode.com/en/problem/k-sum/

--------------------
##思路
可以把```f[i][j][t]```看作表示从前```i```个元素中取```j```个元素，使其和为```t```。

-------------------------------

```java
public class Solution {
    /**
     * @param A: an integer array.
     * @param k: a positive integer (k <= length(A))
     * @param target: a integer
     * @return an integer
     */
    public int kSum(int A[], int k, int target) {
       int n = A.length;
       int[][][] f = new int[n + 1][k + 1][target + 1];
      
       for (int i = 0; i <= n; i++) {
           f[i][0][0] = 1;
       }
       
       for (int i = 1; i <= n; i++) {
           for (int j = 1; j <= k && j <= i; j++) {
               for (int t = 1; t <= target; t++) {
                   f[i][j][t] = 0;
                   if (t >= A[i - 1]) {
                       f[i][j][t] = f[i - 1][j - 1][t - A[i - 1]];
                   }
                   f[i][j][t] += f[i - 1][j][t]; 
               }
           }
       }
       
       return f[n][k][target];
    }
}
```
-------------------------
##易错点

1. 初始条件
```java
int[][][] f = new int[n + 1][k + 1][target + 1];      
for (int i = 0; i <= n; i++) {
     f[i][0][0] = 1;
}
```
从```i```个元素里取0个元素，使其和为0的方法就是一种：不取。

2. 核心部分
```java
if (t >= A[i - 1]) {
     f[i][j][t] = f[i - 1][j - 1][t - A[i - 1]];
}
f[i][j][t] += f[i - 1][j][t]; 
```
3. 先赋值，再update
```java
f[i][j][t] = 0;
```
忘掉了先赋值


































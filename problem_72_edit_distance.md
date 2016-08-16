# Problem 72: Edit Distance


> https://leetcode.com/problems/edit-distance/

-----------------------
##思路

其实insert和delete就是一个操作，所以无非两种操作，要么删要么改（replace）。

如果前 i - 1 和 j - 1 个元素正好相同了，那么不需要进行额外的操作，直接沿用前边的就可以了。如果不同，那就要在三种操作里选一种并加1。

------------------------------------
```java
public class Solution {
    public int minDistance(String word1, String word2) {
        int n = word1.length();
        int m = word2.length();
        
        int[][] f = new int[n + 1][m + 1];
        for (int i = 0; i <= n; i++) {
            f[i][0] = i;
        }
        for (int j = 0; j <= m; j++) {
            f[0][j] = j;
        }
        
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    f[i][j] = f[i - 1][j - 1];
                } else {
                    f[i][j] = Math.min(f[i - 1][j], Math.min(f[i][j - 1], f[i - 1][j - 1])) + 1;
                }
            }
        }
        
        return f[n][m];
    }
}
```
-------------------
##易错点

1. 如何在三个数当中取最小。
```java
Math.Min(int a, int b)
```
只能允许有两个元素进行比较，但我们可以做一个小小的修改，就是吧```int b```的位置用另外一个min函数来代替
```java
Math.Min(int a, Math.min(int b, int c))
```
2. 三种形式代表三种操作
```f[i - 1][j]```,```f[i][j - 1]```,```f[i - 1][j - 1]```代表了不同的增删改，而且他们的额外操作都耗费1，所以最后加 1


























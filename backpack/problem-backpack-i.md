# Problem: Backpack I

> http://www.lintcode.com/en/problem/backpack/

------
##思路
* 这道题考虑的方向可以是针对单个的 item，要还是要。要会怎么样，不要又会怎么样。
* `dp[i][j]`代表重量为`i`的 pack，取`j`件物品的最大值。
* 这里`dp[i][j]`和`A[j]`是有错位的，对于 dp 的第`j`件物品，在 A 中是第`j - 1` 

------


```java
public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    public int backPack(int m, int[] A) {
        // write your code here
        if (m == 0 || A == null || A.length == 0) return 0;
        
        int n = A.length;
        int[][] pack = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (i >= A[j - 1]) {
                    pack[i][j] = Math.max(pack[i][j - 1], pack[i - A[j - 1]][j - 1] + A[j - 1]);
                } else {
                    pack[i][j] = pack[i][j - 1];
                }
            }
        }
        
        return pack[m][n];
    }
}
```

-----
* 优化：用滚动数组来优化。这里有一个易错点，就是要把**滚动的那部分放在外层循环**。


```java
public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    public int backPack(int m, int[] A) {
        // write your code here
        if (m == 0 || A == null || A.length == 0) return 0;
        
        int n = A.length;
        int[][] pack = new int[m + 1][2];
        for (int j = 1; j <= n; j++) {
            for (int i = 1; i <= m; i++) {
                if (i >= A[j - 1]) {
                    pack[i][j % 2] = Math.max(pack[i][(j - 1) % 2], pack[i - A[j - 1]][(j - 1) % 2] + A[j - 1]);
                } else {
                    pack[i][j % 2] = pack[i][(j - 1) % 2];
                }
            }
        }
        
        return Math.max(pack[m][1], pack[m][0]);
    }
}
```































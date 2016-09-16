# Problem 59: Spiral Matrix II


> https://leetcode.com/problems/spiral-matrix-ii/

------
##思路
* 和上一题目的思路如出一辙
* 其中最后判断 n 为奇偶的原因就是对应上一题当中的 n = 1, m = 1 的单独情况

--------------------
```java
public class Solution {
    public int[][] generateMatrix(int n) {
        int[][] matrix  = new int[n][n];
        int x = 0, y = 0;
        int k = n;
        int val = 1;
        
        while (k > 0) {
            // left to right
            for (int i = 0; i < k - 1; i++) {
                matrix[x][y++] = val++; 
            }
            // to bottom
            for (int i = 0; i < k - 1; i++) {
                matrix[x++][y] = val++; 
            }
            // to left
            for (int i = 0; i < k - 1; i++) {
                matrix[x][y--] = val++;
            }
            // to top
            for (int i = 0; i < k - 1; i++) {
                matrix[x--][y] = val++;
            }
            
            // to next
            x++;
            y++;
            k -= 2;
        }
        
        if (n % 2 != 0) {
            matrix[n / 2][n / 2] = val;
        } 
        
        return matrix;
    }
}
```
------
##易错点
1. 判断中点的位置
```java
matrix[n / 2][n / 2] = val;
```





















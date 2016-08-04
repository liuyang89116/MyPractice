# Problem 63: Unique Paths II

> https://leetcode.com/problems/unique-paths-ii/

-------------------------------
##思路
在上一题的基础上引入条件的判断

-----------------
```java
public class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid == null || obstacleGrid.length == 0 || obstacleGrid[0].length == 0) {
            return 0;
        }
        
        //state
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] f = new int[m][n];
        
        //initiate
        for (int i = 0; i < m; i++) {
            if (obstacleGrid[i][0] != 1) {
                f[i][0] = 1;
            } else {
                break;
            }
        }
        for (int i = 0; i < n; i++) {
            if (obstacleGrid[0][i] != 1) {
                f[0][i] = 1;
            } else {
                break;
            }
        }
        
        //function
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (obstacleGrid[i][j] != 1) {
                    f[i][j] = f[i - 1][j] + f[i][j - 1];
                } else {
                    f[i][j] = 0;
                }
            }
        }
        //answer
        return f[m - 1][n - 1];
        
    }
}
```
-------------------------------
##易错点

1. corner cases要考虑全面
   ```java
   if (obstacleGrid == null || obstacleGrid.length == 0 || obstacleGrid[0].length == 0) {
         return 0;
   }
   ```
2. 初始化的时候，有障碍的跳过，记得要break
   ```java
   for (int i = 0; i < m; i++) {
        if (obstacleGrid[i][0] != 1) {
             f[i][0] = 1;
        } else {
             break;
        }
   }
   ```
3. 有障碍的跳过，剩下的如果到不了这个点，那么方法总数应该是0
   ```java
   if (obstacleGrid[i][j] != 1) {
        f[i][j] = f[i - 1][j] + f[i][j - 1];
   } else {
        f[i][j] = 0;
   }
   ```




























# Problem 221: Maximal Square

> https://leetcode.com/problems/maximal-square/

---------
##思路
* 决定一个正方形的是四个顶点。如果这四个顶点能向外延伸，正方形就增大 1
* 我们设置一个 matrix（比原来那个大 1），然后由右下角的点 traverse 整个 matrix

----------


```java
public class Solution {
    public int maximalSquare(char[][] matrix) {
        if (matrix == null || matrix.length == 0) {
            return 0;
        }
        
        int m = matrix.length, n = matrix[0].length;
        int len = 0;
        int[][] square = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (matrix[i - 1][j - 1] == '1') {
                    square[i][j] = Math.min(Math.min(square[i - 1][j], square[i][j - 1]), square[i - 1][j - 1]) + 1;
                    len = Math.max(len, square[i][j]);
                }
            }
        }
        
        return len * len;
    }
}
```

-------
##易错点
* Math.min() 函数只能比两个数的大小，如果有两个以上的数比较，可以进行嵌套。
```java
Math.min(Math.min(square[i - 1][j], square[i][j - 1]), square[i - 1][j - 1])
```


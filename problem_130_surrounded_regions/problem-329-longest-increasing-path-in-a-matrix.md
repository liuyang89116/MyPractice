# Problem 329: Longest Increasing Path in a Matrix

> https://leetcode.com/problems/longest-increasing-path-in-a-matrix/\#/description

--------

## 思路

* 用一个 `cache[i][j]`来记录每个点可以对应的最长步数。同时，在 dfs 方程里，他还起到了 `visited[i][j]`的作用-

-----

```java
public class Solution {
    public static final int[][] directions = new int[][] {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    
    public int longestIncreasingPath(int[][] matrix) {
        if (matrix == null || matrix.length == 0) return 0;
        
        int m = matrix.length, n = matrix[0].length;
        int[][] cache = new int[m][n];
        int max = 1;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int len = dfs(matrix, i, j, m, n, cache);
                max = Math.max(max, len);
            }
        }
        
        return max;
    }
    
    private int dfs(int[][] matrix, int i, int j, int m, int n, int[][] cache) {
        if (cache[i][j] != 0) return cache[i][j];
        
        int max = 1;
        for (int[] dir : directions) {
             int x = i + dir[0];
             int y = j + dir[1];
             
             if (x < 0 || x >= m || y < 0 || y >= n || matrix[x][y] <= matrix[i][j]) continue;
             int len = 1 + dfs(matrix, x, y, m, n, cache);
             max = Math.max(max, len);
        }
        cache[i][j] = max;
        
        return max;
    }
}


```




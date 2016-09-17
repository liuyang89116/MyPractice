# Problem 79: Word Search


> https://leetcode.com/problems/word-search/

---------
##思路
* 记录路径，看每个结点是否被访问过
* 递归方程中的四个条件：  
（1） 返回条件，就是找到了 word  
（2） row，col 的 index 条件  
（3） 被访问过的排除  
（4） 和 word 对不上的排除
* 上下左右四个方向分别 check

--------
```java
public class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length;
        int n = board[0].length;
        boolean[][] visited = new boolean[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (dfs(board, word, 0, i, j, visited)) {
                    return true;
                }
            }
        }
        return false;
    }
    
    private boolean dfs(char[][] board, String word, int index, int rowIndex, int colIndex, boolean[][] visited) {
        if (index == word.length()) {
            return true;
        }
        if (rowIndex < 0 || colIndex < 0 || rowIndex >= board.length || colIndex >= board[0].length) {
            return false;
        }
        if (visited[rowIndex][colIndex]) {
            return false;
        }
        if (board[rowIndex][colIndex] != word.charAt(index)) {
            return false;
        }
        
        visited[rowIndex][colIndex] = true;
        boolean res = dfs(board, word, index + 1, rowIndex - 1, colIndex, visited) ||
                      dfs(board, word, index + 1, rowIndex + 1, colIndex, visited) ||
                      dfs(board, word, index + 1, rowIndex, colIndex - 1, visited) ||
                      dfs(board, word, index + 1, rowIndex, colIndex + 1, visited);
        visited[rowIndex][colIndex] = false;
        
        return res;
    }
}
```
---
##易错点
1. 递归完 reset visited 数组
```java
visited[rowIndex][colIndex] = false;
```






















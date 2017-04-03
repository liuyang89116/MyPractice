# Problem 37: Sudoku Solver

> https://leetcode.com/problems/sudoku-solver/\#/description

--------

## 思路

* 首先遍历整个 matrix，然后尝试填入 1 - 9 这些数字。
* 每次填入一个数字，立马进行 check，如果 valid，就继续往下一层递归；反之退出。所以基于这样的考虑，可以把 dfs 设置成 boolean type，这样可以一层一层地判断
* 最后判断每一个 3 \* 3 的 block 的时候，注意如何定位每一个元素

-------

```java
public class Solution {
    public void solveSudoku(char[][] board) {
        if (board == null || board.length == 0) return;
        
        dfs(board);
    }
    
    private boolean dfs(char[][] board) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] == '.') {
                    for (char c = '1'; c <= '9'; c++) { // 尝试填入 1 - 9
                        if (validate(board, i, j, c)) {
                            board[i][j] = c;
                            
                            if (dfs(board)) {
                                return true;
                            } else {
                                board[i][j] = '.';
                            }
                        }
                    }
                    
                    return false;
                }
            }
        }
        
        return true;
    }
    
    private boolean validate(char[][] board, int row, int col, char c) {
        for (int i = 0; i < 9; i++) {
            if (board[i][col] == c) return false;
            if (board[row][i] == c) return false;
            if (board[3 * (row / 3) + i / 3][3 * (col / 3) + i % 3] == c) return false;
        }
        
        return true;
    }
    
}
```




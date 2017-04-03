# Problem 51: N-Queens

> https://leetcode.com/problems/n-queens/\#/description

-------

## 思路

* “N - 皇后” 问题在于，每行，每列，每个斜线都不能有其他的皇后。我们可以安装 column 来填，从左往右。
* 由于是按 column 填的，所以每一列不用担心有重复；对于每一行，check 一下即可；斜线的情况比较复杂：可以用斜率来判断。
* 对于两个点 `(x, y）`和`(i, j)`判断$$(y - j)/(x - i) = 1$$ 或者 $$(y - j)/(x - i) = -1$$

* 另外，判断 column的时候只需要 check 左边的元素，原因如上

-------

```java
public class Solution {
    public List<List<String>> solveNQueens(int n) {
        char[][] board = new char[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] = '.';
            }
        }
        
        List<List<String>> rst = new ArrayList<>();
        dfs(board, 0, rst);
        
        return rst;
    }
    
    private void dfs(char[][] board, int colIndex, List<List<String>> rst) {
        if (colIndex == board.length) {
            rst.add(construct(board));
            return;
        }
        
        for (int i = 0; i < board.length; i++) {
            if (validate(board, i, colIndex)) {
                board[i][colIndex] = 'Q';
                dfs(board, colIndex + 1, rst);
                board[i][colIndex] = '.';
            }
        }
    }
    
    private boolean validate(char[][] board, int x, int y) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < y; j++) {
                if (board[i][j] == 'Q' && (y - j == x - i || y - j == i - x || i == x)) return false;
            }
        }
        
        return true;
    }
    
    private List<String> construct(char[][] board) {
        List<String> level = new ArrayList<>();
        for (int i = 0; i < board.length; i++) {
            String s = new String(board[i]);
            level.add(s);
        }
        
        return level;
    }
}


```




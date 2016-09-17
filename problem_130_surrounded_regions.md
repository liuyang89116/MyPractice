# Problem 130: Surrounded Regions


> https://leetcode.com/problems/surrounded-regions/

---------
##思路
* 只要边界有 'O' 是肯定没有办法被 'X' 吃掉的，所以我们首先 check 第一行，最后一行，第一列和最后一列
* 紧接着，我们以这写边角的 'O' 为起点，用 bfs 进行搜寻，看看前后左右是否还有 'O'
* 边角的 'O' 先标记成 '#'， 最后的时候，把 'O' 都标记成 'X'，因为他们都会被吃掉；再把 '#' 恢复成 'O'

-------
```java
public class Solution {
    public void solve(char[][] board) {
        if (board == null || board.length == 0 || board[0].length == 0) {
            return;
        }
        
        // check first row and last row
        for (int i = 0; i < board[0].length; i++) {
            bfs(board, 0, i);
            bfs(board, board.length - 1, i);
        }
        // check first col and last col
        for (int i = 0; i < board.length; i++) {
            bfs(board, i, 0);
            bfs(board, i, board[0].length - 1);
        }
        
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                } else if (board[i][j] == '#') {
                    board[i][j] = 'O';
                }
            }
        }
    }
    
    private void bfs(char[][] board, int i, int j) {
        if (board[i][j] != 'O') {
            return;
        }
        
        board[i][j] = '#';
        Queue<Integer> queue = new LinkedList<Integer>();
        // encode the location
        int code = i * board[0].length + j;
        queue.add(code);
        while (!queue.isEmpty()) {
            code = queue.poll();
            int row = code / board[0].length;
            int col = code % board[0].length;
            
            // check above
            if (row >= 1 && board[row - 1][col] == 'O') {
                queue.add((row - 1) * board[0].length + col);
                board[row - 1][col] = '#';
            }
            // check below
            if (row <= board.length - 2 && board[row + 1][col] == 'O') {
                queue.add((row + 1) * board[0].length + col);
                board[row + 1][col] = '#';
            }
            // check left
            if (col >= 1 && board[row][col - 1] == 'O') {
                queue.add(row * board[0].length + col - 1);
                board[row][col - 1] = '#';
            }
            // check right
            if (col <= board[0].length - 2 && board[row][col + 1] == 'O') {
                queue.add(row * board[0].length + col + 1);
                board[row][col + 1] = '#';
            }
        }
    }
}
```
-----
##易错点
1. 给每个入 queue 的元素加密以及解密
```java
// encode the location
int code = i * board[0].length + j;
// decode
int row = code / board[0].length;
int col = code % board[0].length;
```
2. 上下左右 check 完了之后，记得把元素入 queue
























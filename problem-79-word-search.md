# Problem 79: Word Search

> [https://leetcode.com/problems/word-search/\#/description](https://leetcode.com/problems/word-search/#/description)

---

## 思路

* 这道题的主要思路就是，遍历每一个点，然后从这个点出发，探索周围的每一个点，上下左右。
* 在 dfs 递归的过程中，可以用 `*`来标记每一个 visited 过的点。结束遍历之后，再把这个点改回来。

---

```java
public class Solution {
    public boolean exist(char[][] board, String word) {
        if (board == null || board.length == 0) return false;

        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (dfs(board, i, j, 0, word)) return true;
            }
        }

        return false;
    }

    private boolean dfs(char[][] board, int i, int j, int index, String word) {
        if (index == word.length()) return true;

        if (i < 0 || i > board.length - 1 || j < 0 || j > board[0].length - 1 || word.charAt(index) != board[i][j]) return false;

        board[i][j] = '*';
        boolean flag =  dfs(board, i - 1, j, index + 1, word) ||
                        dfs(board, i + 1, j, index + 1, word) ||
                        dfs(board, i, j - 1, index + 1, word) ||
                        dfs(board, i, j + 1, index + 1, word);
        board[i][j] = word.charAt(index);

        return flag;
    }
}
```




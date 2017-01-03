# Print Char Board

> Print all possible paths from top left to bottom right of a m x n `char[][]` board

-------
##思路
* 毫无疑问，这是要使用 DFS 遍历来实现的。关键在于寻找退出条件
* 从上往下走，只能有两种选择：要么向右，要么向下。所以退出条件就是，当走到最后一行或者最后一列的时候，停住，然后向下或者向右把唯一方向的元素都遍历完。
* 这里用了 StringBuilder 节省了空间，适用与元素较多的情况。

--------


```java
import java.util.ArrayList;

/**
 * Created by yang on 1/2/17.
 */
public class Solution {
    public static ArrayList<String> printCharBoard(char[][] board) {
        ArrayList<String> rst = new ArrayList<>();
        if (board == null || board.length == 0) {
            return rst;
        }
        StringBuilder sb = new StringBuilder();

        dfs(board, 0, 0, sb, rst);
        return rst;
    }

    private static void dfs(char[][] board, int row, int col, StringBuilder sb, ArrayList<String> rst) {
        if (row == board.length - 1) {
            for (int i = col; i < board[0].length; i++) {
                sb.append(board[row][i]);
            }
            rst.add(sb.toString());
            return;
        }

        if (col == board[0].length - 1) {
            for (int i = row; i < board.length; i++) {
                sb.append(board[i][col]);
            }
            rst.add(sb.toString());
            return;
        }

        sb.append(board[row][col]);
        int len = sb.length();
        dfs(board, row + 1, col, sb, rst);
        sb.setLength(len); // 非常重要，用来保留上一次的分叉口
        dfs(board, row, col + 1, sb, rst);
        sb.setLength(len); // 非常重要，用来保留上一次的分叉口
    }

    public static void main(String[] args) {
        char[] arr1 = new char[]{'a', 'b', 'c'};
        char[] arr2 = new char[]{'d', 'e', 'f'};
        char[] arr3 = new char[]{'g', 'h', 'i'};
        char[][] board = new char[][]{arr1, arr2, arr3};

        ArrayList<String> rst = printCharBoard(board);
        for (String s : rst) {
            System.out.println(s);
        }
    }
}

```


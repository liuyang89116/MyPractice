# Problem 73: Set Matrix Zeroes


> https://leetcode.com/problems/set-matrix-zeroes/

-----------
##思路
* 这道题主要考察了对数组操作的熟练程度
* 先 check 第一行和第一列里面有没有 0；再 check 剩余的元素 matrix[i][j]， 如果有 0 ，则把这元素所在的第一行第一列设为 0 

-----------
```java
public class Solution {
    public void setZeroes(int[][] matrix) {
        if (matrix == null || matrix.length == 0) {
            return;
        }
        
        int row = matrix.length;
        int col = matrix[0].length;
        boolean isEmptyRow0 = false;
        boolean isEmptyCol0 = false;
        
        // check row0 and col 0
        for (int i = 0; i < col; i++) {
            if (matrix[0][i] == 0) {
                isEmptyRow0 = true;
                break;
            }
        }
        
        for (int i = 0; i < row; i++) {
            if (matrix[i][0] == 0) {
                isEmptyCol0 = true;
                break;
            }
        }
        
        // check rest entries
        for (int i = 1; i < row; i++) {
            for (int j = 1; j < col; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        
        // set zeros
        for (int i = 1; i < row; i++) {
            for (int j = 1; j < col; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }
        
        for (int i = 0; i < col; i++) {
            if (isEmptyRow0) {
                matrix[0][i] = 0;
            }
        }
        
        for (int i = 0; i < row; i++) {
            if (isEmptyCol0) {
                matrix[i][0] = 0;
            }
        }
    }
}
```
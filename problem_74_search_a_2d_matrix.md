
# Problem 74: Search a 2D Matrix


> https://leetcode.com/problems/search-a-2d-matrix/

---------------------------------------------------------
##思路
就是用两次二分法，先找row，再找column

-----------------------------------------------------------

```java
public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0) {
            return false;
        }

        int row, column;

        //find row index
        int start = 0;
        int end = matrix.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (target == matrix[mid][0]) {
                return true;
            } else if (target < matrix[mid][0]) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (target == matrix[start][0] || target == matrix[end][0]) {
            return true;
        } else if (target > matrix[start][0] && target < matrix[end][0]) {
            row = start;
        } else if (target > matrix[end][0]) {
            row = end;
        } else {
            return false;
        }

        //find column
        start = 0;
        end = matrix[row].length - 1;
        while (start + 1 < end) {
            int mid  = start + (end - start) / 2;
            if (target == matrix[row][mid]) {
                return true;
            } else if (target < matrix[row][mid]) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (target == matrix[row][start]) {
            return true;
        }
        if (target == matrix[row][end]) {
            return true;
        }
        return false;
    }
}
```
------------------------------------
##易错点

1. 画数轴，用target作为点，start， end作为标记，来标定区间
2. 思路保持清晰
3. 最后判断的时候，比的是target和matrix[start]的值，而不是target和start比


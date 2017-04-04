# Problem 52: N-Queens II

> https://leetcode.com/problems/n-queens-ii/\#/description

--------

## 思路

* 这道题问的是一共有多少组解，而没有要求存解的结果。这样的话，我们可以进行一些优化，用三个 set 来维护 row 和两个对角线。
* 这里判断 diagonal 的方式比较方便。还是假设我们之前有一个 queen 在 \(a, b\) 点，现在我们要在 \(x, y\) 上放第二个点。$$(y - b) / (x - a) = 1 (-1)$$  也就是说，$$y - x = b - a$$ 或者  $$y + x = b + a$$



--------------

```java
public class Solution {
    Set<Integer> rowSet = new HashSet<Integer>();
    Set<Integer> diag1Set = new HashSet<Integer>();
    Set<Integer> diag2Set = new HashSet<Integer>();
     
    public int totalNQueens(int n) {
        return dfs(0, 0, n);   
    }
    
    private int dfs(int col, int count, int n) {
        for (int row = 0; row < n; row++) {
            if (rowSet.contains(row)) continue;
            int diag1 = col - row;
            if (diag1Set.contains(diag1)) continue;
            int diag2 = col + row;
            if (diag2Set.contains(diag2)) continue;
            
            if (col == n - 1) {
                count++;
            } else {
                rowSet.add(row);
                diag1Set.add(diag1);
                diag2Set.add(diag2);
                
                count = dfs(col + 1, count, n);
                
                rowSet.remove(row);
                diag1Set.remove(diag1);
                diag2Set.remove(diag2);
            }
        }
        
        return count;
    }
}
```



 


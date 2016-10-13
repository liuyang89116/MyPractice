# Problem 200: Number of Islands

> https://leetcode.com/problems/number-of-islands/

---------
##思路
* 首先定位每一个 island，也就是 “1”， 然后用 dfs 递归
* 这里有个问题就是如果访问过一次以后，我们需要标记，于是我们把访问过的 “1” 标记为 “2”

------
```java
public class Solution {
    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }
        
        int count = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1') {
                    count++;
                    dfs(grid, i, j);
                }
            }
        }
        
        return count;
    }
    
    private void dfs(char[][] grid, int i, int j) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] != '1') return;
        grid[i][j] = '2';
        
        dfs(grid, i - 1, j);
        dfs(grid, i + 1, j);
        dfs(grid, i, j - 1);
        dfs(grid, i, j + 1);
    }
    
}
```
------
##易错点

1. 注意退出条件
```java
if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] != '1') return;
```
注意最后一个条件```grid[i][j] != '1'```，岛的身边如果还是岛，我们就退出，不管他了就。
2. 边界条件
```i >= grid.length```平时没留意这个 ```=```























# Problem 417: Pacific Atlantic Water Flow

> https://leetcode.com/problems/pacific-atlantic-water-flow/\#/description

------------

## 思路

* 刚开始我以为标记括号的点是一条路径。但仔细一看并不是，题目理解有误。**实际的意思是：用括号标记的每一个点，都存在一条联通太平洋和大西洋的路径**。
* 那我们于是可以考虑：从边界出发，遍历每一个点。对于每一个点，判断他是否可以流向其他角落。
* 如果判断最后那些点可以收入结果呢？同时存在于大西洋和太平洋的访问轨迹上的点。



---------

```java
public class Solution {
    int[][] direction = new int[][] {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
    
    public List<int[]> pacificAtlantic(int[][] matrix) {  
        List<int[]> rst = new ArrayList<int[]>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return rst;
        
        int m = matrix.length, n = matrix[0].length;
        Queue<int[]> pQueue = new LinkedList<int[]>();
        Queue<int[]> aQueue = new LinkedList<int[]>();
        boolean[][] pacific = new boolean[m][n];
        boolean[][] atlantic = new boolean[m][n];
        
        for (int i = 0; i < n; i++) {
            pQueue.offer(new int[] {0, i});
            aQueue.offer(new int[] {m - 1, i});
            pacific[0][i] = true;
            atlantic[m - 1][i] = true;
        }
        for (int i = 0; i < m; i++) {
            pQueue.offer(new int[] {i, 0});
            aQueue.offer(new int[] {i, n - 1});
            pacific[i][0] = true;
            atlantic[i][n - 1] = true;
        }
        
        bfs(matrix, pQueue, pacific);
        bfs(matrix, aQueue, atlantic);
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (pacific[i][j] && atlantic[i][j]) {
                    rst.add(new int[] {i, j});
                }
            }
        }
        
        return rst;
    }
    
    private void bfs(int[][] matrix, Queue<int[]> queue, boolean[][] visited) {
        int m = matrix.length, n = matrix[0].length;
        while (!queue.isEmpty()) {
            int[] cur = queue.poll();
            for (int[] dir : direction) {
                int x = cur[0] + dir[0];
                int y = cur[1] + dir[1];
                if (x < 0 || x >= m || y < 0 || y >= n || visited[x][y] || matrix[x][y] < matrix[cur[0]][cur[1]]) continue;
                visited[x][y] = true;
                queue.offer(new int[] {x, y});
            }
        }
    }
}





```

---------

## 易错点

1. `matrix[x][y] < matrix[cur[0]][cur[1]`为什么是 `<` ？

**因为这里是面向每一个点考虑的。判断他能否流向其他地方。**




# Problem 289: Game of Life

> https://leetcode.com/problems/game-of-life/

--------
##思路
* 这道题没那么简单啊。count 完周围的八个点之后，不能立即更新 ```board[i][j]```的状态，否则会影响后面的点的判断
* 为了既能及时更新，又能 “in place”，所以就要赋值。
* 诀窍在于更新每一个 ```board[i][j]``` 的时候用新的数字2， 3进行表示， 2表示之前是1但是以后要 dead 的点，3表示之前是0但是以后要 live 的点

--------
```java
public class Solution {
    public void gameOfLife(int[][] board) {
        int m = board.length, n = board[0].length;
        int[] dx = {-1, -1, -1, 0, 0, 1, 1, 1};
        int[] dy = {-1, 0, 1, -1, 1, -1, 0, 1};
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int count = 0;
                for (int k = 0; k < 8; k++) {
                    int x = i + dx[k];
                    int y = j + dy[k];
                    if (x < 0 || x >= m || y < 0 || y >= n) {
                        continue;
                    }
                    if (board[x][y] == 1 || board[x][y] == 2) {
                        count++;
                    }
                }
                
                if (board[i][j] == 0 && count == 3) {
                    board[i][j] = 3;
                }
                if (board[i][j] == 1 && (count < 2 || count > 3)) {
                    board[i][j] = 2;
                }
            }
        }
    
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] %= 2;
            }
        }
    }
}
```
-----
##易错点
1. 定位八个点的坐标
```java
int[] dx = {-1, -1, -1, 0, 0, 1, 1, 1};
int[] dy = {-1, 0, 1, -1, 1, -1, 0, 1};
int x = i + dx[k];
int y = j + dy[k];
```
2. 通过不同的赋值，来防止之前更改过的影响下一步的选择。同时，还有留心之前改过的东西，现在要不要接着使用。
```java
if (board[x][y] == 1 || board[x][y] == 2) {
       count++;
}
```






















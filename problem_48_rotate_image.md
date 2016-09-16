# Problem 48: Rotate Image


> https://leetcode.com/problems/rotate-image/

-----------
##思路
![](rotateImage.png)

* 首先沿对角线对称变换，再沿 x 做镜面变换
* 所以我们可以知道 ```matrix[i][j]``` 的变换过程：  
列的变换：就是上一个的行（y = x 做对称，相当于把 x，y 对调）；
行的变换：用总的长度 len - 1 减去 之前的列的坐标 (之所以是之前列的坐标不是行的坐标是因为已经做了对角线的对称变换，现在的行就是之前的列)

--------------
```java
public class Solution {
    public void rotate(int[][] matrix) {
        if (matrix == null || matrix.length == 0) {
            return;
        }
        
        int len = matrix.length;
        for (int i = 0; i < len / 2; i++) {
            for (int j = 0; j < (len + 1) / 2; j++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[len - 1 - j][i];
                matrix[len - 1 - j][i] = matrix[len - 1 - i][len - 1 - j];
                matrix[len - 1 - i][len - 1 - j] = matrix[j][len - 1 - i];
                matrix[j][len - 1 - i] = tmp;
            }
        }
    }
}
```
------------
##易错点

1. j 的界限
```java
 for (int j = 0; j < (len + 1) / 2; j++)
```
先记着吧，挺 tricky 的






















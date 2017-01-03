# Calculate Crossing

> 矩阵中由 1 构成的一横一竖的连续的 1，并且这一横一竖有一个交叉点的，是一条十字路。总的来说对每一个 1：  和他在同一列上，与他相连的的连续的1的数量 + 和同他在同一行上，与他相连的连续的1的数量 的和就是以当前1为交叉点的十字路的长度。找出矩阵中最长的十字路。 

```
举几个例子吧：
0 0 0
1 1 1
1 0 0   
最长的十字路长度是4

0 0 1 0 0 0
0 0 1 1 1 1
1 1 1 0 1 0
0 0 1 0 0 1
最长的十字路长度是7
```

--------
##思路
* 参考 Bomb Enemy 的思路。我们维持一个 row 和一个 col[]。当之前的元素为 0 的时候，我们需要对 row 和 col[] 进行重新计算，遍历整个数组，得到最大值。
* 记得减去一，因为交叉点计算了两次。

----------
##复杂度
* Time: `O(m * n)`
* Space: `O(n)`，只维持了 col[] 

----------


```java
package com.yang;

/**
 * Created by yang on 1/2/17.
 */
public class Solution4 {
    // calculate crossing
    public static int maxCrossing(int[][] roads) {
        if (roads == null || roads.length == 0) {
            return 0;
        }

        int max = 0;
        int row = 0;
        int[] col = new int[roads[0].length];
        for (int i = 0; i < roads.length; i++) {
            for (int j = 0; j < roads[0].length; j++) {
                if (roads[i][j] == 0) continue;

                if (j == 0 || roads[i][j - 1] == 0) {
                    row = calculateRow(roads, i, j);
                }
                if (i == 0 || roads[i - 1][j] == 0) {
                    col[j] = calculateCol(roads, i, j);
                }

                max = Integer.max(max, row + col[j] - 1);
            }
        }

        return max;
    }

    // calculate row
    private static int calculateRow(int[][] roads, int row, int col) {
        int count = 0;
        for (int i = col; i < roads[row].length; i++) {
            if (roads[row][i] == 0) break;
            count++;
        }

        return count;
    }

    // calculate col
    private static int calculateCol(int[][] roads, int row, int col) {
        int count = 0;
        for (int i = row; i < roads.length; i++) {
            if (roads[i][col] == 0) break;
            count++;
        }

        return count;
    }

    // main function, test
    public static void main(String[] args) {
        /*int[] arr1 = new int[]{0, 0, 0};
        int[] arr2 = new int[]{1, 1, 1};
        int[] arr3 = new int[]{1, 0, 0};
        int[][] arr = new int[][]{arr1, arr2, arr3};*/

        int[] arr1 = new int[]{0, 0, 1, 0, 0, 0};
        int[] arr2 = new int[]{0, 0, 1, 1, 1, 1};
        int[] arr3 = new int[]{1, 1, 1, 0, 1, 0};
        int[] arr4 = new int[]{0, 0, 1, 0, 0, 1};
        int[][] arr = new int[][]{arr1, arr2, arr3, arr4};

        System.out.println(maxCrossing(arr));
    }
}

```


# Problem 463: Island Perimeter

> [https://leetcode.com/problems/island-perimeter/](https://leetcode.com/problems/island-perimeter/)

---

## 思路:

* 如果从上往下，从左往右遍历，对于每一个“岛”，我们要算出他下面和右边是否也是岛。如果是的话，相当于共用了一个边界。

* `岛的总周长 = 4 * 岛 - 2 * 邻居`

---

## 复杂度

`O(n*m)`

---

```java
class Solution {
    public int islandPerimeter(int[][] grid) {
        int islands = 0;
        int neighbors = 0;

        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 0) continue;

                islands++;
                if (i < grid.length - 1 && grid[i + 1][j] == 1) neighbors++;
                if (j < grid[i].length - 1 && grid[i][j + 1] == 1) neighbors++;
            }
        }

        return islands * 4 - neighbors * 2; 
    }
}
```

---

## 易错点

1. `2 * 邻居`： **只要有共用，就不是周长了，两个岛都得把这条边减去**




# Problem 305: Number of Islands II

> [https://leetcode.com/problems/number-of-islands-ii/\#/description](https://leetcode.com/problems/number-of-islands-ii/#/description)

---

## 思路

> https://discuss.leetcode.com/topic/29518/java-python-clear-solution-with-unionfind-class-weighting-and-path-compression

这个答案不错

> [https://www.cs.princeton.edu/~rs/AlgsDS07/01UnionFind.pdf](https://www.cs.princeton.edu/~rs/AlgsDS07/01UnionFind.pdf)

Princeton 讲义

* Union Find 经典题目。首先标注一个 2D map 每个 element 的 index ： `index = x * n + y + 1`，这样的话，每个 element 的 index 都是唯一的。
* size \(或者 count\) 来控制 islands  的个数

---------

## 复杂度

* 时间复杂度：$$ O(m * alpha(n)) $$ , $$ alpha(n) <= 4$$







---

```java
public class Solution {
    private int[][] dir = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};

    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        UnionFind2D islands = new UnionFind2D(m, n);
        List<Integer> rst = new ArrayList<>();
        for (int[] pos : positions) {
            int x = pos[0], y = pos[1];
            int cur = islands.add(x, y);
            for (int[] d : dir) {
                int next = islands.getId(x + d[0], y + d[1]);
                if (next > 0 && !islands.find(cur, next)) islands.unite(cur, next);
            }
            rst.add(islands.getSize());
        }

        return rst;
    }
}

class UnionFind2D {
    private int[] id;
    private int[] size;
    private int m, n, count;

    public UnionFind2D(int m, int n) {
        this.count = 0;
        this.m = m;
        this.n = n;
        this.id = new int[m * n + 1];
        this.size = new int[m * n + 1];
    }

    public int getIndex(int x, int y) {
        return x * n + y + 1;
    }

    public int getSize() {
        return this.count;
    }

    public int getId(int x, int y) {
        if (x >= 0 && x < m && y >= 0 && y < n) {
            return id[getIndex(x, y)];
        }
        return 0;
    }

    public int add(int x, int y) {
        int index = getIndex(x, y);
        id[index] = index;
        size[index] = 1;
        count++;
        return index;
    }

    public boolean find(int p, int q) {
        return getRoot(p) == getRoot(q);
    }

    public void unite(int p, int q) {
        int i = getRoot(p), j = getRoot(q);
        if (size[i] < size[j]) { // weighted quick union
            id[i] = j;
            size[j] += size[i];
        } else {
            id[j] = i;
            size[i] += size[j];
        }
        count--;
    }

    private int getRoot(int i) {
        while (i != id[i]) {
            i = id[i];           // path compression
            id[i] = id[id[i]];  
        }
        return i;
    }

}
```




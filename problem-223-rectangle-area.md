# Problem 223: Rectangle Area

> https://leetcode.com/problems/rectangle-area/\#/description

-------

## 思路

* 不去考虑各种 overlap 的情况，而是直接 narrow down 可能发生 overlap 的条件
* 如果没有 overlap，那么计算 overlap 面积的时候，直接就是 0

------

```java
public class Solution {
    public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        int left = Math.max(A, E);
        int right = Math.max(left, Math.min(C, G));
        int bottom = Math.max(B, F);
        int top = Math.max(bottom, Math.min(D, H));
        
        return (C - A) * (D - B) + (G - E) * (H - F) - (right - left) * (top - bottom);
    }
}
```




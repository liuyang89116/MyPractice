# Overlap Rectangle



```java
package OverlapRectangle;

import java.awt.*;

/**
 * Created by yang on 1/17/17.
 */
public class Solution {
    // Overlap Rectangle : 计算总共的面积
    // Rect 1: top-left(A, B), bottom-right(C, D)
    // Rect 2: top-left(E, F), bottom-right(G, H)
    public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        int left = Math.max(A, E);
        int right = Math.max(left, Math.min(C, G));
        int top = Math.max(B, F);
        int bottom = Math.max(top, Math.min(D, H));

        int area = (C - A) * (B - D) + (G - E) * (F - H)
                - (right - left) * (top - bottom);
        return area;
    }

    // 判断两个长方形是否重叠
    // Returns true if two rectangles (l1, r1) and (l2, r2) overlap
    public boolean isOverlap(Point l1, Point r1, Point l2, Point r2) {
        if (l1.x > r2.x || l2.x > r1.x) {
            return false;
        }

        if (l1.y < r2.y || l2.y < r1.y) {
            return false;
        }

        return true;
    }
}

```


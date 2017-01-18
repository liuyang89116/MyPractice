# Find K Nearest Point



```java
package KNearestPoint;

import java.awt.*;
import java.util.Comparator;
import java.util.PriorityQueue;

/**
 * Created by yang on 1/17/17.
 */
public class Solution {
    public static Point[] kNearestPoint(Point[] array, Point origin, int k) {
        Point[] rst = new Point[k];
        int count = 0;
        PriorityQueue<Point> pq = new PriorityQueue<>(k, new Comparator<Point>() {
            @Override
            public int compare(Point p1, Point p2) {
                return calDistance(p1, origin) - calDistance(p2, origin);
            }
        });

        for (int i = 0; i < array.length; i++) {
            pq.offer(array[i]);
            if (pq.size() > k) {
                pq.poll();
            }
        }

        while (!pq.isEmpty()) {
            rst[count++] = pq.poll();
        }

        return rst;

    }

    public static int calDistance(Point a, Point origin) {
        return (a.x - origin.x) * (a.x - origin.x) + (a.y - origin.y) * (a.y - origin.y);
    }
}

```


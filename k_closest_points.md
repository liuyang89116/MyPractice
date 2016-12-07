# K closest points

> Find the K closest points to the origin in a 2D plane, given an array containing N points.

---------
##思路
* 用 Heap 做，也就是最小堆

---------
##复杂度
* $$O(nlogn)$$

---------
```java
package yang_03;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.PriorityQueue;

/*
 * Find the K closest points to the origin in a 2D plane, 
 * given an array containing N points.
 */
public class KClosestPoints {
	class Point {
		int x;
		int y;

		public Point(int x, int y) {
			this.x = x;
			this.y = y;
		}
	}

	public List<Point> findKClosestPoint(Point[] p, int k) {
		PriorityQueue<Point> pq = new PriorityQueue<Point>(k,
				new Comparator<Point>() {
					public int compare(Point p1, Point p2) {
						return (p2.x * p2.x + p2.y * p2.y)
								- (p1.x * p1.x + p1.y * p1.y);
					}
				});

		for (int i = 0; i < p.length; i++) {
			if (i < k) {
				pq.offer(p[i]);
			} else {
				Point curr = pq.peek();
				int d = p[i].x * p[i].x + p[i].y * p[i].y;
				int dCurr = curr.x * curr.x + curr.y * curr.y;
				if (d < dCurr) {
					pq.poll();
					pq.offer(p[i]);
				}
			}
		}

		List<Point> rst = new ArrayList<Point>();
		while (!pq.isEmpty()) {
			rst.add(pq.poll());
		}

		return rst;
	}

}

```
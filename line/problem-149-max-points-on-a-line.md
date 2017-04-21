# Problem 149: Max Points on a Line

> https://leetcode.com/problems/max-points-on-a-line/\#/description

-----

## 思路

> https://discuss.leetcode.com/topic/2979/a-java-solution-with-notes

这个讲解不错！

* 这道题，用一个 map 来存这样的关系：`x - (y, count)`, 这里的 x 和 y 为了方便，直接都是用最大公约数除过的
* 这样被最大公约数除过之后，斜率 `k = y / x`可以说是固定的了
* 不要忘了重合的点用 dup 来表示，然后加上自己本身 1



-------

```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
public class Solution {
    public int maxPoints(Point[] points) {
        if (points == null) return 0;
        if (points.length <= 2) return points.length;
        
        HashMap<Integer, HashMap<Integer, Integer>> map = new HashMap<>();
        int max = 0;
        for (int i = 0; i < points.length; i++) {
            map.clear();
            int dup = 0, count = 0;
            for (int j = i + 1; j < points.length; j++) {
                int x = points[j].x - points[i].x;
                int y = points[j].y - points[i].y;
                if (x == 0 && y == 0) {
                    dup++;
                    continue;
                }
                int gcd = calculateGCD(x, y);
                if (gcd != 0) {
                    x /= gcd;
                    y /= gcd;
                }
                
                if (map.containsKey(x)) {
                    if (map.get(x).containsKey(y)) {
                        map.get(x).put(y, map.get(x).get(y) + 1);
                    } else {
                        map.get(x).put(y, 1);
                    }
                } else {
                    HashMap<Integer, Integer> innerMap = new HashMap<>();
                    innerMap.put(y, 1);
                    map.put(x, innerMap);
                }
                count = Math.max(count, map.get(x).get(y));
            }
            
            max = Math.max(max, count + dup + 1);
        }
        
        return max;
    }
    
    private int calculateGCD(int a, int b) {
        if (b == 0) return a;
        return calculateGCD(b, a % b);
    }
}

```






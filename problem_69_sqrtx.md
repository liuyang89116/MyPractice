# Problem 69: Sqrt(x)

> https://leetcode.com/problems/sqrtx/

----------
##思路
* 二分法逼近

--------
```java
public class Solution {
    public int mySqrt(int x) {
        long start = 1;
        long end = x;
        while (start + 1 < end) {
            long mid = start + (end - start) / 2;
            if (mid * mid <= x) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (end * end <= x) {
            return (int) end;
        }
        
        return (int) start;
    }
}
```

--------
##易错点
1. 注意 start 和 end 这些中间计算的量用 long 存储，最后再转回来成 int

# Problem 278: First Bad Version


> https://leetcode.com/problems/first-bad-version/

---------------------
##思路
* 就是黑箱法测电路断路的一个应用

------------------
```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int start = 1;
        int end = n;
        int mid;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (isBadVersion(mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (isBadVersion(start)) {
            return start;
        }
        if (isBadVersion(end)) {
            return end;
        }
        return 0;
    }
}
```

----------
##易错点

1. 学会看代码注释，比如本题当中的```isBadVersion()```方法的调用































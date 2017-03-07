# Problem 342: Power of Four

> https://leetcode.com/problems/power-of-four/?tab=Description

-------------

## 思路

* `(num >= 0) && ((num & (num - 1)) == 0)` 这两句判断的是“是否是平方”
* $$\(n\)^4 - 1 = \(n - 1\) \(n + 1\) \(n^2 + 1\)$$

------------

```java
public class Solution {
    public boolean isPowerOfFour(int num) {
        return (num >= 0) && ((num & (num - 1)) == 0) && ((num - 1) % 3 == 0);
    }
}
```




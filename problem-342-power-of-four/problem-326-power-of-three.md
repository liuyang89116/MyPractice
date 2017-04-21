# Problem 326: Power of Three

> https://leetcode.com/problems/power-of-three/\#/description

----------

## 思路

* $$n = 3 ^ m$$ 等价于 $$log(n) = m * log(3)$$



-----

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        return (Math.log10(n) / Math.log10(3)) % 1 == 0; 
    }
}
```




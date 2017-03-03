# Problem 201: Bitwise AND of Numbers Range

> [https://leetcode.com/problems/bitwise-and-of-numbers-range/?tab=Description](https://leetcode.com/problems/bitwise-and-of-numbers-range/?tab=Description)

---

## 思路

> https://discuss.leetcode.com/topic/28538/java-python-easy-solution-with-explanation

这个讲解不错

* 我们要找的其实是前几位相同的部分，这些高位相同的部分都一样，我们放着不管
* 后面不同的位数，有多少个，就有多少种组合的可能

------------

```java
public class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        if (m == 0) return 0;
        
        int count = 0;
        while (m != n) {
            m >>= 1;
            n >>= 1;
            count++;
        }
        
        return m << count;
    }
}
```






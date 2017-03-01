# Problem 191: Number of 1 Bits

> [https://leetcode.com/problems/number-of-1-bits/?tab=Description](https://leetcode.com/problems/number-of-1-bits/?tab=Description)

---

## 思路

> [https://discuss.leetcode.com/topic/11385/simple-java-solution-bit-shifting](https://discuss.leetcode.com/topic/11385/simple-java-solution-bit-shifting)

这篇讲解不错！

* 我们通过 `n & 1` 来判断 n 的最后一个 bit 是否为 1。这里 1 可以看做是 `0000000001`

* 接下来我们就右移一位，判断下面的一个 bit。之所以用 `>>>`，是因为 `>>` 会收到符号的影响

----------

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int count = 0;
        while (n != 0) {
            count += (n & 1);
            n = n >>> 1;
        }
        
        return count;
    }
}
```




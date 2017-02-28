# Problem 461: Hamming Distance

> [https://leetcode.com/problems/hamming-distance/?tab=Description](https://leetcode.com/problems/hamming-distance/?tab=Description)

---

## 思路

* 我们用异或 xor 来判断每一位上的 bit 是否相同。如果是 1，我们就给 count 加 1
* 然后对 xor 进行右移

---

```java
public class Solution {
    public int hammingDistance(int x, int y) {
        int xor = x ^ y;
        int count = 0;
        while (xor != 0) {
            count += (xor & 1);
            xor = xor >> 1;
        }

        return count;
    }
}
```




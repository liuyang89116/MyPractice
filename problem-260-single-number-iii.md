# Problem 260: Single Number III

> [https://leetcode.com/problems/single-number-iii/?tab=Description](https://leetcode.com/problems/single-number-iii/?tab=Description)

---

## 思路

这个讲解不错！

> https://discuss.leetcode.com/topic/21605/accepted-c-java-o-n-time-o-1-space-easy-solution-with-detail-explanations

* 之前的问题里只有一个单独的元素，xor 一遍就可以找出落单的那个。那这道题怎么办呢？
* **分组**！通过分组把这两个落单的元素跳出来。

---

```java
public class Solution {
    public int[] singleNumber(int[] nums) {
        if (nums == null || nums.length < 2) return null;

        int xor = 0;
        for (int num : nums) {
            xor ^= num;
        }

        int[] rst = new int[] {0, 0};
        xor &= -xor;
        for (int num : nums) {
            if ((xor & num) == 0) {
                rst[0] ^= num;
            } else {
                rst[1] ^= num;
            }
        }

        return rst;
    }
}
```




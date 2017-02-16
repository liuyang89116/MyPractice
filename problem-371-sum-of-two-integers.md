# Problem 371: Sum of Two Integers

> https://leetcode.com/problems/sum-of-two-integers/

------
##思路
> https://discuss.leetcode.com/topic/49771/java-simple-easy-understand-solution-with-explanation 

> https://discuss.leetcode.com/topic/50315/a-summary-how-to-use-bit-manipulation-to-solve-problems-easily-and-efficiently

这两篇对于 bit manipulation 的总结非常好！

* 首先用 `a & b` 来得到进位，并且循环的退出条件是什么时候没有进位了，什么时候就退出。
* 然后用 `a ^ b` 来得到不同的 bit
* 最后把 carrier shift，以此类推

------


```java
public class Solution {
    public int getSum(int a, int b) {
        if (a == 0) return b;
        if (b == 0) return a;
        
        while (b != 0) {
            int carrier = a & b;
            a = a ^ b;
            b = (carrier << 1);
        }
        
        return a;
    }
}
```



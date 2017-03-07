# Problem 190: Reverse Bits

> https://leetcode.com/problems/reverse-bits/?tab=Description

---------

## 思路

* 这道题的思路就是首先保留原先的 bit，同时 reverse bit 的顺序
* 保留原先 bit ： `n & 1`，这样 0 还是 0 ，1 还是 1

* 然后用 shift 的形式连接 bit，原来是从右向左，现在一连接就相当于 “reverse” 了 bits

------------

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int rst = 0;
        for (int i = 0; i < 32; i++) {
            rst += (n & 1);
            n >>>= 1;
            if (i < 31) rst <<= 1;
        }
        
        return rst;
    }
}
```



--------

## Follow Up

> If this function is called many times, how would you optimize it?

* 这个回答不错。 https://discuss.leetcode.com/topic/9764/java-solution-and-optimization




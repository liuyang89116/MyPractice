# Problem 172: Factorial Trailing Zeroes


> https://leetcode.com/problems/factorial-trailing-zeroes/

-----------
##思路
* 在排列数 n！ 当中，有几个 0 其实取决有几个 5。因为只要是偶数，就会有 2。
* 先用 n 除以 5，得出有几个 5；然后再除以 25；再除以 125……

-----------
```java
public class Solution {
    public int trailingZeroes(int n) {
        int count = 0;
        while (n != 0) {
            count += n / 5;
            n /= 5;
        }
        
        return count;
    }
}
```


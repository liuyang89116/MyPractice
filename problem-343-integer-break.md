# Problem 343: Integer Break

> https://leetcode.com/problems/integer-break/

------
##思路
> https://discuss.leetcode.com/topic/45341/a-simple-explanation-of-the-math-part-and-a-o-n-solution

这就是一个数学题，其实没啥意思
* 如果想要使最后的 product 最大，那么就要**让被分解的这些数字尽可能相等**！
* 对于不同的 factor，当 n 是偶数时， $$(n/2)*(n/2)$$ 最大；当 n 是奇数的时候，$$(n - 1)/2 * (n + 1) / 2$$ 最大。
* 当 $$n >= 4$$ 的时候, $$(n/2)*(n/2)>=n$$； 当 $$n>=5$$ 的时候，$$(n-1)/2 *(n+1)/2>=n$$，也就是说，备选的 factor 只可能是 1, 2，3， 而这三个数，越大的最后乘积越大。**所以我们尽可能多选 3**。

---------


```java
public class Solution {
    public int integerBreak(int n) {
        if (n == 2) return 1;
        if (n == 3) return 2;
        
        int product = 1;
        while (n > 4) {
            product *= 3;
            n -= 3;
        }
        product *= n;
        
        return product;
    }
}
```


# Problem 319: Bulb Switcher

> https://leetcode.com/problems/bulb-switcher/\#/description

-------

## 思路

> https://discuss.leetcode.com/topic/39558/share-my-o-1-solution-with-explanation

这道题就是脑筋急转弯。

* 简单讲，就是找小于 n 的完全平方数的个数（因为他们的 factor 的个数是奇数）
* 而这样又直接等于 n 开方

---------

```java
public class Solution {
    public int bulbSwitch(int n) {
        return (int) Math.sqrt(n);
    }
}
```




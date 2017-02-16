# Problem 322: Coin Change

> https://leetcode.com/problems/coin-change/

----------
##思路
* 最优解的一个思路就是，针对每一个元素，“取”或者“不取”。如果取这个元素，那么相当于把问题的 size 缩小了，然后继续“分解”剩下的 subproblem；如果不取这个元素，那么维持现状，move on
* 这里把初始值都设成最大值，可以有效地**标记**。

-------
##复杂度
* Time: $$O(n^j)$$

-----


```java
public class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0) return 0;
        
        int[] count = new int[amount + 1];
        for (int i = 1; i <= amount; i++) {
            count[i] = Integer.MAX_VALUE;
            for (int j = 0; j < coins.length; j++) {
                if (i >= coins[j] && count[i - coins[j]] != Integer.MAX_VALUE) {
                    count[i] = Math.min(count[i], 1 + count[i - coins[j]]);
                }
            }
        }
        
        if (count[amount] == Integer.MAX_VALUE) return -1;
        
        return count[amount];
    }
}
```


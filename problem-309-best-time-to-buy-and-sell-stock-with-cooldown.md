# Problem 309: Best Time to Buy and Sell Stock with Cooldown

> https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/

-------
##思路
> https://discuss.leetcode.com/topic/30421/share-my-thinking-process

这个讲解实在是太棒了！
* 首先对于一个 dp 问题，我们首先应该考虑 state，然后根据不同的 state，得出 transition function。这里应该有三个不同的 state：`buy`，`sell`，`rest`，其中 `rest` 就是买完股票被冷冻的状态。
* 根据这三个状态我们可以得出转移方程：</br>
`buy[i]`：在第 i 天，买股票所能得到的最大收益；</br>
`sell[i]`：在第 i 天，卖股票所能得到的最大收益；</br>
`rest[i]`：在第 i 天，被冷冻所能得到的最大收益；</br>
```
buy[i] = max(rest[i - 1] - price, buy[i - 1])
sell[i] = max(buy[i - 1] + price, sell[i - 1])
rest[i] = max(sell[i - 1], buy[i - 1], rest[i - 1])
```
* 一个简单的逻辑就是：**buy 之前必须是 rest 的状态； 只有先 buy，才能 sell**</br>
* 易错点：如果出现`[buy, rest, buy]` 怎么办？用 `buy[i] <= rest[i]` 可以限制，它等价于 `rest[i] = max(sell[i - 1], rest[i - 1])`。由此还可以推出另一个关系：`rest[i] = sell[i - 1]`
* 结合这两个关系式，代入最上面，可以得出：</br>
```
buy[i] = max(sell[i - 2] - price, buy[i - 1])
sell[i] = max(buy[i - 1] + price, sell[i - 1])
```
因为第 i 天只和第 i - 1 天和第 i - 2 天有关，所以可以进一步简化为 `O(1)` 的 space

---------


```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) return 0;
        
        int sell = 0, prevSell = 0, buy = Integer.MIN_VALUE, prevBuy;
        for (Integer price : prices) {
            prevBuy = buy;
            buy = Math.max(prevSell - price, prevBuy);
            prevSell = sell;
            sell = Math.max(prevBuy + price, prevSell);
        }
        
        return sell;
    }
}
```



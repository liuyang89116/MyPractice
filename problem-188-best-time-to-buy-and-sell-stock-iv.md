# Problem 188: Best Time to Buy and Sell Stock IV

> https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/

-----------
##思路
* 对于一次交易来说,永远是先 buy 后 sell。对于 buy 来说，对于 profit 的影响永远是负数，因为是要花钱的。
* 当前`sell[j]`的大小，取决于当前的 `prices[i]` 和当前的 `buy[j]`；而当前 `buy[j]` 的大小，取决于上一次的 `sell[j - 1]`
* 这里有一个 trick：当 `k >= len / 2` 的时候，说明**最多每次都可以进行交易，想交易几次交易几次**，也就是化归成了 `Best Time to Buy and Sell Stock II`

---------


```java
public class Solution {
    public int maxProfit(int k, int[] prices) {
        if (k < 1) return 0;
        if (prices == null || prices.length <= 1) return 0;
        
        int len = prices.length;
        if (k >= len / 2) {
            return helper(prices);
        }
        
        int[] buy = new int[k + 1];
        int[] sell = new int[k + 1];
        Arrays.fill(buy, Integer.MIN_VALUE);
        for (int i = 0; i < prices.length; i++) {
            for (int j = k; j > 0; j--) {
                sell[j] = Math.max(sell[j], prices[i] + buy[j]);
                buy[j] = Math.max(buy[j], sell[j - 1] - prices[i]);
            }
        }
        
        return sell[k];
    }
    
    private int helper(int[] prices) {
        int profit = 0;
        for (int i = 0; i < prices.length - 1; i++) {
            int diff = prices[i + 1] - prices[i];
            if (diff > 0) {
                profit += diff;
            }
        }
        
        return profit;
    }
}


```



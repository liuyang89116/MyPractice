# Problem 121: Best Time to Buy and Sell Stock


> https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

---------
##思路
* 维护两个值：一个是股票的最低值，一个是总利润。因为股票的特殊性，只有后面的价格比前面的价格高才是挣钱了，反之是不行的，是赔钱了。

-----------
```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }
        
        int min = Integer.MAX_VALUE;
        int profit = 0;
        for (Integer value : prices) {
            min = (value < min ? value : min);
            profit = ((value - min) > profit ? (value - min) : profit);
        }
        
        return profit;
    }
}
```
----------
##易错点
1. 合理地使用三目运算，并且在加括号的基础上赋值
2. 维护最小值
```java
int min = Integer.MAX_VALUE;
```
这句话的意义是随便标记一下 min，以后只要有比他小的就可以代替他























# Problem 123: Best Time to Buy and Sell Stock III


> https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/

-----------------------
##思路
* 两次买卖，并且一个时间点只能进行一次交易（不能同时既买进又卖出），那么肯定存在一个时间点（并且是卖出点），在这之前进行的是第一次交易，在这之后进行的是第二次交易
![](buyStock_02.jpg)
* 那么如何在 O(n) 的时间内扫完这些点呢？我们可以设置两个数组 left[] 和 right[]。left[] 代表从左往右扫；right[] 代表从右往左扫。左边是第一次交易的最大值，右边是第二次交易的最大值，他们的和就是总的最大 profit
* 扫左边的时候，我们主要的任务是找最小值**min**，然后我们用当前的prices[i]一减就是第一次的利润；扫右边的时候呢，我们关注的是最大值**max**，用这个max值减去当前的prices[i]，这样就是第二次的最大利润。

-------------
```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length <= 1) {
            return 0;
        }
        
        int[] left = new int[prices.length];
        int[] right = new int[prices.length];
        
        // left to right
        left[0] = 0;
        int min = prices[0];
        for (int i = 1; i < prices.length; i++) {
            min = Math.min(prices[i], min);
            left[i] = Math.max(left[i - 1], prices[i] - min);
        }
        
        // right to left
        right[prices.length - 1] = 0;
        int max = prices[prices.length - 1];
        for (int i = prices.length - 2; i >= 0; i--) {
            max = Math.max(prices[i], max);
            right[i] = Math.max(right[i + 1], max - prices[i]);
        }
        
        int profit = 0;
        for (int i = 0; i < prices.length; i++) {
            profit = Math.max(profit, left[i] + right[i]);
        }
        
        return profit;
    }
}
```
--------
##易错点

1. 循环的次数，下标很容易出错
left to right
```java
left[0] = 0;
int min = prices[0];
for (int i = 1; i < prices.length; i++) {
          min = Math.min(prices[i], min);
          left[i] = Math.max(left[i - 1], prices[i] - min);
}
```
这是一个动归，先确定最小值min，然后考虑每一个点的最大利润；
right to left
```java
right[prices.length - 1] = 0;
int max = prices[prices.length - 1];
for (int i = prices.length - 2; i >= 0; i--) {
          max = Math.max(prices[i], max);
          right[i] = Math.max(right[i + 1], max - prices[i]);
}
```
先确定最大值，然后考虑每一个点的最大利润。**可以发现，不管是往左还是往右，都是先确定边界点（```int min = prices[0;]```or```int max = prices[prices.length - 1];```）**
2. 保持清醒，什么时候考虑的是数组prices，什么时候考虑的是数组left or right




























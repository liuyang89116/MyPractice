# Problem 42: Trapping Rain Water

> https://leetcode.com/problems/trapping-rain-water/

----------
##思路
* 这道题和上一题还有些不一样，上一题中，两面都是 bar，是看两个 bar 之间最多能存多少水。这道题是每个 height 相当于不同的台阶，看台阶的低洼处能存多少水。
![](/assets/TrappingRainWater.png)
* 首先维护两个指针 left，right，让他们从两边逼近。然后用 leftMax 和 rightMax 来记录两边的最高点，**只有低的地方才有可能确定地存有水**。所以我们不断地更新和判断 leftMax 和 rightMax。

---------


```java
public class Solution {
    public int trap(int[] height) {
        int left = 0, right = height.length - 1;
        int leftMax = 0, rightMax = 0;
        int sum = 0;
        while (left < right) {
            leftMax = Math.max(leftMax, height[left]);
            rightMax = Math.max(rightMax, height[right]);
            if (leftMax < rightMax) {
                sum += leftMax - height[left];
                left++;
            } else {
                sum += rightMax - height[right];
                right--;
            }
        }
        
        return sum;
    }
}
```


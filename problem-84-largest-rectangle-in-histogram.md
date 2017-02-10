# Problem 84: Largest Rectangle in Histogram

> https://leetcode.com/problems/largest-rectangle-in-histogram/

----------
##思路
这篇文章写得很好。
> http://www.geeksforgeeks.org/largest-rectangle-under-histogram/

* We need to know index of the first smaller (smaller than ‘x’) bar on left of ‘x’ and index of first smaller bar on right of ‘x’. Let us call these indexes as ‘left index’ and ‘right index’ respectively.
* We traverse all bars from left to right, maintain a stack of bars. Every bar is pushed to stack once. A bar is popped from stack when a bar of smaller height is seen. When a bar is popped, we calculate the area with the popped bar as smallest bar.
* How do we get left and right indexes of the popped bar – the current index tells us the ‘right index’ and index of previous item in stack is the ‘left index’. Following is the complete algorithm.

![](/assets/largestRanctangle.png)



----------
##复杂度
* Time: `O(n)`

-----------
```java
public class Solution {
    public int largestRectangleArea(int[] heights) {
        if (heights == null || heights.length == 0) {
            return 0;
        }
        
        int i = 0, n = heights.length;
        int maxArea = 0;
        Stack<Integer> stack = new Stack<Integer>();
        while (i <= n) {
            int h = (i == n ? 0 : heights[i]);
            if (stack.isEmpty() || h >= heights[stack.peek()]) {
                stack.push(i);
                i++;
            } else {
                int tp = stack.pop();
                maxArea = Math.max(maxArea, heights[tp] * (stack.isEmpty() ? i : i - 1 - stack.peek()));
            }
        }
        
        return maxArea;
    }
}
```
----------
##易错点
1. 循环边界
```java
while (i <= n)
```
为什么是 `<=` 而不是 `<` 呢？这是因为我们要统一单个的 bar。当单个的 bar 入 stack 的时候，会直接进栈而不计算面积，这时候，我需要配合引入，
```java
int h = (i == n ? 0 : heights[i]);
```
这样单个 bar 的时候也会计算面积
2. 更新面积
```
heights[tp] * (stack.isEmpty() ? i : i - 1 - stack.peek())
```
(1) 为什么是 `i - 1 - stack.peek()`？  
因为此时第 i 个元素还没有进栈，它算的是之前 i - 1 个元素所形成的最大面积。  </br>
(2) 为什么 stack 为空的时候，结果为 i ？  
因为它相当于比之前所有的 bar 都小，才能把 stack 搬空。
![](/assets/largestRanctangle.png)


































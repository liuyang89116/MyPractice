# Problem 85: Maximal Rectangle

> https://leetcode.com/problems/maximal-rectangle/

------
##思路
* 这道题的思路基于上一道题目，bar 的高度是递增的，我们就一直可以往 stack 里面 push；反之，我们就开始计算最大面积。
* 我们如何转换为上一道题目呢？我们可以 maitain 一个 height 数组，也就是 `1` 的高度；这样不同的 height 就可以放到 stack 里进行比较。

--------


```java
public class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix == null || matrix.length == 0) return 0;
        
        int m = matrix.length;
        int n = matrix[0].length;
        int maxArea = 0;
        int[] height = new int[n];
        Stack<Integer> stack = new Stack<Integer>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '1') {
                    height[j]++;
                } else {
                    height[j] = 0;
                }
                
                while (!stack.isEmpty() && height[j] <= height[stack.peek()]) {
                    int top = stack.pop();
                    maxArea = Math.max(maxArea, height[top] * (stack.isEmpty() ? j : j - 1 - stack.peek()));
                }
                stack.push(j);
            }
            while (!stack.isEmpty()) {
                int top = stack.pop();
                maxArea = Math.max(maxArea, height[top] * (stack.isEmpty() ? n : n - 1 - stack.peek()));
            }
        }
        
        return maxArea;
    }
}
```


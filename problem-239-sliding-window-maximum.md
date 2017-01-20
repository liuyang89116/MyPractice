# Problem 239: Sliding Window Maximum

> https://leetcode.com/problems/sliding-window-maximum/

-------
##思路
* Sliding Window 类题目，一类是之前的那种 window size 可以改变的，可以用两根指针 left, right 来不断调整；还有一类题目就是这道题，window size 固定，这时候就需要额外的数据结构来优化，比如这里的 deque
* deque 其实就是 double ended queue 可以两头进行添加或删除。
* 我们要维持一段 window size 的 index 范围，这里用 `i - k + 1` 来表示 window 的开头元素。整个 deque 维护的是 nums 的 index
* 如果超过了 window 范围，我们把元素 poll() 出去；如果新来的元素比上一次来的元素大，我们把最后的元素 poll() 出去。

------


```java
public class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return new int[] {};
        }
        int len = nums.length, index = 0;
        int[] rst = new int[len - k + 1];
        Deque<Integer> dq = new ArrayDeque<Integer>();
        for (int i = 0; i < nums.length; i++) {
            if (!dq.isEmpty() && dq.peek() < i - k + 1) {
                dq.poll();
            }
            while (!dq.isEmpty() && nums[i] > nums[dq.peekLast()) {
                dq.pollLast();
            }
            dq.offer(i);
            
            if (i - k + 1 >= 0) {
                rst[index++] = nums[dq.peek()];
            }
        }
        
        return rst;
    }
}
```

-------
##易错点
1. 注意什么时候 poll() 开头，什么时候 poll() 尾巴
2. 如果新来的元素比较大，要连续 poll()，用 while 循环实现，不能用 if


```java
while (!dq.isEmpty() && nums[i] > nums[dq.peekLast()) {
    dq.pollLast();
}
```





















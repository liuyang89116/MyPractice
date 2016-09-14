# Problem 155: Min Stack


> https://leetcode.com/problems/min-stack/

-----------
##思路
* 我开始想的是用一个 minValue 来维护一个最小值。但这样做是不符合条件的，因为这样只能记录最后一次的最小值，因为一旦把当前的最小值 pop 出去以后，后面的值就不知道了。
* 所以我们可以用两个 stack 来实现：stack 和 minStack。minStack 专门用来维护当前的最小值，只 push 最小值进去！而 stack 当作一个备用元素，他的作用是记录 top 元素。两者分工明确。

-----------
```java
public class MinStack {

    private Stack<Integer> stack;
    private Stack<Integer> minStack;
    
    public MinStack() {
        stack = new Stack<Integer>();
        minStack = new Stack<Integer>();
    }
    
    public void push(int x) {
        stack.push(x);
        if (minStack.isEmpty()) {
            minStack.push(x);
        } else {
            minStack.push(Math.min(x, minStack.peek()));
        }
    }
    
    public void pop() {
        stack.pop();
        minStack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return minStack.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```
--------
##易错点

1. 考虑清楚什么时候是 pop()，什么时候是 peek()
```java
public int getMin() {
       return minStack.peek();
}
```
当时错写成了 pop()，这样当 stack 为空的时候，会出现错误。





















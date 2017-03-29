# Problem 439: Ternary Expression Parser

> [https://leetcode.com/problems/ternary-expression-parser/\#/description](https://leetcode.com/problems/ternary-expression-parser/#/description)

---

![](/assets/439_0.png)![](/assets/439_1.png)

---

## 思路

* 分析的时候从右向左，每次只要遇到 `?`就停下来。
* 用 stack 来维护第一个值和第二个值。

----------

```java
public class Solution {
    public String parseTernary(String expression) {
        if (expression == null || expression.length() == 0) return null;
        
        Stack<Character> stack = new Stack<Character>();
        for (int i = expression.length() - 1; i >= 0; i--) {
            char c = expression.charAt(i);
            if (!stack.isEmpty() && stack.peek() == '?') {
                stack.pop(); // pop '?'
                char firstValue = stack.pop();
                stack.pop(); // pop ':'
                char secondValue = stack.pop();
                
                if (c == 'T') {
                    stack.push(firstValue);
                } else {
                    stack.push(secondValue);
                }
            } else {
                stack.push(c);
            }
        }
        
        return String.valueOf(stack.peek());
    }
}
```































